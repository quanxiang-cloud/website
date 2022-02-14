---
title: '如何实现一个满足业务需求的流程设计器'
tag: '流程设计, 前端, 表单, 低代码, 工作流'
keywords: '流程设计, 前端, 表单, 低代码, 工作流, 低代码, low-code'
description: '在低代码场景中，流程是一个必不可少的能力。流程的能力就是给予用户通过一个表单触发一个在不同时间节点流转的异步任务。最常见的就是请假申请，用户提交一个请假申请表单，提交成功之后流程开始运行，直到下一个节点被对应的人员所处理，流程的状态才会向后续步骤行进。那么如何将我们所构思的流程设计器付诸实现呢？'
createTime: '2021-12-31'
author: '马梨胜'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/How%20to%20implement%20a%20process%20designer%20that%20meets%20business%20needs/cover.png'
---

## 背景

在低代码场景中，流程是一个必不可少的能力。流程的能力就是给予用户通过一个表单触发一个在不同时间节点流转的异步任务。最常见的就是请假申请，用户提交一个请假申请表单，提交成功之后流程开始运行，直到下一个节点被对应的人员所处理，流程的状态才会向后续步骤行进。那么如何将我们所构思的流程设计器付诸实现呢？今天便来手把手教大家！

## 流程设计

首先需要进行流程设计，对于前端来说, 流程设计器有这么几个点需要满足：
1. 用户根据某个表单创建一个流程
2. 可以定义流程的节点
3. 可以定义流程的节点所对应的配置

其中定义流程的节点就是定义异步任务的各个环节以及它们之间的关系。流程节点的配置对于实现来说就是一个表单，这个表单可以对当前步骤所需的能力进行配置，例如流程触发的表单字段，审批人等。

据此我们可以确定流程的基本数据模型，第一直觉可能会考虑用一个有向无环图来表示整个流程，图中的节点对应了流程的节点，节点之间的连线表示流程之间的前置关系。但图处理起来过于复杂，这里考虑使用数组描述，数组的元素包括节点和边，每个节点都有一个节点名称及 id，节点之间的边包含了节点的 id 信息。

### 数据接口定义

以下是使用 typescript 定义的数据模型接口：

```typescript
export interface Node<T = any> {
  id: ElementId;
  position: XYPosition;
  type?: string;
  __rf?: any;
  data?: T;
  style?: CSSProperties;
  className?: string;
  targetPosition?: Position;
  sourcePosition?: Position;
  isHidden?: boolean;
  draggable?: boolean;
  selectable?: boolean;
  connectable?: boolean;
  dragHandle?: string;
}
export interface Edge<T = any> {
  id: ElementId;
  type?: string;
  source: ElementId;
  target: ElementId;
  sourceHandle?: ElementId | null;
  targetHandle?: ElementId | null;
  label?: string | ReactNode;
  labelStyle?: CSSProperties;
  labelShowBg?: boolean;
  labelBgStyle?: CSSProperties;
  labelBgPadding?: [number, number];
  labelBgBorderRadius?: number;
  style?: CSSProperties;
  animated?: boolean;
  arrowHeadType?: ArrowHeadType;
  isHidden?: boolean;
  data?: T;
  className?: string;
}
export type FlowElement<T = any> = Node<T> | Edge<T>;
export interface Data {
  nodeData: Record<string, any>;
  businessData: Record<string, any>;
}
export interface WorkFlow {
  version: string;
  shapes: FlowElement<Data>[];
}
```

整个数据模型的定义很清晰，整体的结构是一个 WorkFlow，其中包含的 version 即版本，shapes 为边以及节点的数组集合。其中 FlowElement 可以是 Node（节点）也可以是 Edge（边），对于 Node 而言其中会存有数据，数据可以通过节点的 data 属性访问。并且数据分为了两部分，一部分是节点的元数据我们称之为 nodeData，一部分是节点所对应的业务数据我们称之为 businessData，元数据主要用于绘制流程图时使用，业务数据主要用于流程引擎执行时使用。

## 流程实现

对于流程设计器的实现我们使用 `react-flow-renderer`  这个开源库，它的优点主要有以下三点：

1. 轻松实现自定义节点
2. 自定义边
3. 预置小地图等图形控件

`react-flow-renderer` 只需要传入 shapes 数组即可渲染出整个流程图，在传入之前需要对 elements 做布局处理，对于布局我们将使用 dagre 这个图形布局库，以下是布局实现。

### 流程图布局

``` tsx
import store from './store';

import useObservable from '@lib/hooks/observable';

function App() {
  const { elements } = useObservable(store);
  const [dagreGraph, setDagreGraph] = useState(() => new dagre.graphlib.Graph());
  dagreGraph.setDefaultEdgeLabel(() => ({}));
  dagreGraph.setGraph({ rankdir: 'TB', ranksep: 90 });

  elements?.forEach((el) => {
    if (isNode(el)) {
      return dagreGraph.setNode(el.id, {
        width: el.data?.nodeData.width,
        height: el.data?.nodeData.height,
      });
    }
    dagreGraph.setEdge(el.source, el.target);
  });
  dagre.layout(dagreGraph);
  const layoutedElements = elements?.map((ele) => {
    const el = deepClone(ele);
    if (isNode(el)) {
      const nodeWithPosition = dagreGraph.node(el.id);
      el.targetPosition = Position.Top;
      el.sourcePosition = Position.Bottom;
      el.position = {
        x: nodeWithPosition.x - ((el.data?.nodeData.width || 0) / 2),
        y: nodeWithPosition.y,
      };
    }
    return el;
  });

  return (
    <>
      <ReactFlow
        className="cursor-move"
        elements={layoutedElements}
      />
    </>
  )
}
```

在使用 dagre 时首先需要调用 dagre.graphlib.Graph 生成一个实例，setDefaultEdgeLabel 用于设置 label，由于这里不需要，故将其置为空。setGraph 用于配置图形属性，通过指定 rankdir 为 TB 意味着布局从 top 到 bottom 也就是从上到下的布局方式，ranksep 表示节点之间的距离。接下来只需要循环元素将节点通过 setNode，边通过 setEdge 设置到 dagre，然后调用 dagre.layout 即可。在设置节点时需要指定节点 id 及节点的宽高，设置边时仅需指定边的起始以及结束点的 id 即可。最后还需要对节点的位置进行微调，因为 dagre 默认的布局方式是垂直左对齐的，我们需要让其垂直居中对齐，因此需要减去其宽度的一半。

### 自定义节点

对于节点这部分，由于默认的节点类型不能满足要求，我们需要自定义节点，这里就拿结束节点进行举例：

```tsx
import React from 'react';
import { Handle, Position } from 'react-flow-renderer';

import Icon from '@c/icon';

import type { Data } from '../type';

function EndNodeComponent({ data }: { data: Data }): JSX.Element {
  return (
    <div
      className="shadow-flow-header rounded-tl-8 rounded-tr-8 rounded-br-0 rounded-bl-8
        bg-white w-100 h-28 flex items-center cursor-default"
    >
      <section className="flex items-center p-4 w-full h-full justify-center">
        <Icon name="stop_circle" className="mr-4 text-red-600" />
        <span className="text-caption-no-color-weight font-medium text-gray-600">
          {data.nodeData.name}
        </span>
      </section>
    </div>
  );
}

function End(props: any): JSX.Element {
  return (
    <>
      <Handle
        type="target"
        position={Position.Top}
        isConnectable={false}
      />
      <EndNodeComponent {...props} />
    </>
  );
}

export const nodeTypes = { end: EndNode };

function App() {
  // 省略部分内容
  return (
    <>
      <ReactFlow
        className="cursor-move"
        elements={layoutedElements}
        nodeTypes={nodeTypes}
      />
    </>
  )
}
```

自定义节点通过 nodeTypes 指定，我们这里指定了自定义结束节点，节点的具体实现在于 EndNode 这个函数组件。我们只需要在创建节点的时候指定节点的 type 为 end 即可使用 EndNode 渲染，创建节点的逻辑如下：

```tsx
function nodeBuilder(id: string, type: string, name: string, options: Record<string, any>) {
  return {
    id,
    type,
    data: {
      nodeData: { name },
      businessData: getNodeInitialData(type)
    }
  }
}
const endNode = nodeBuilder(endID, 'end', '结束', {
  width: 100,
  height: 28,
  parentID: [startID],
  childrenID: [],
})
elements.push(endNode);
```

### 自定义边

自定义边与自定义节点类似，通过指定 edgeTypes 完成，下面是实现自定义边的举例代码：

```tsx
import React, { DragEvent, useState, MouseEvent } from 'react';
import { getSmoothStepPath, getMarkerEnd, EdgeText, getEdgeCenter } from 'react-flow-renderer';
import cs from 'classnames';

import ToolTip from '@c/tooltip/tip';

import type { EdgeProps, FormDataData } from '../type';

import './style.scss';

export default function CustomEdge({
  id,
  sourceX,
  sourceY,
  targetX,
  targetY,
  sourcePosition,
  targetPosition,
  style = {},
  label,
  arrowHeadType,
  markerEndId,
  source,
  target,
}: EdgeProps): JSX.Element {
  const edgePath = getSmoothStepPath({
    sourceX,
    sourceY,
    sourcePosition,
    targetX,
    targetY,
    targetPosition,
    borderRadius: 0,
  });
  const markerEnd = getMarkerEnd(arrowHeadType, markerEndId);
  const [centerX, centerY] = getEdgeCenter({
    sourceX,
    sourceY,
    targetX,
    targetY,
    sourcePosition,
    targetPosition,
  });

  const formDataElement = elements.find(({ type }) => type === 'formData');
  const hasForm = !!(formDataElement?.data?.businessData as FormDataData)?.form.name;
  const cursorClassName = cs({ 'cursor-not-allowed': !hasForm });

  return (
    <>
      <g
        className={cs(cursorClassName, { 'opacity-50': !hasForm })}
      >
        <path
          id={id}
          style={{ ...style, borderRadius: '50%' }}
          className={cs('react-flow__edge-path cursor-pointer pointer-events-none', cursorClassName)}
          d={edgePath}
          markerEnd={markerEnd}
        />
        {status === 'DISABLE' && (
          <EdgeText
            className={cursorClassName}
            style={{
              filter: 'drop-shadow(0px 8px 24px rgba(55, 95, 243, 1))',
              pointerEvents: 'all',
            }}
            x={centerX}
            y={centerY}
            label={label}
          />
        )}
      </g>
      {!hasForm && (
        <foreignObject
          className="overflow-visible workflow-node--tooltip"
          x={centerX + 20}
          y={centerY - 10}
          width="220"
          height="20"
        >
          <ToolTip
            label="请为开始节点选择一张工作表"
            style={{
              transform: 'none',
              backgroundColor: 'transparent',
              alignItems: 'center',
            }}
            labelClassName="whitespace-nowrap text-12 bg-gray-700 rounded-8 text-white pl-5"
          >
            <span></span>
          </ToolTip>
        </foreignObject>
      )}
    </>
  );
}

export const edgeTypes = {
  plus: CustomEdge,
};

function App() {
  // 省略部分内容
  return (
    <>
      <ReactFlow
        className="cursor-move"
        elements={layoutedElements}
        nodeTypes={nodeTypes}
        edgeTypes={edgeTypes}
      />
    </>
  )
}
```

边的具体实现在于 CustomEdge 这个函数组件，这里我们通过使用 `react-flow-renderer` 提供的 EdgeText 组件，在边的中间显示一个加号，以便后续可以添加点击加号时的处理事件。EdgeText 需要传入一个 label 作为显示的内容，然后需要指定内容显示的坐标，我们这里让文本显示在边的中间，边的中间位置通过调用 getEdgeCenter 来计算得到，计算的时候需传入起点与终点的坐标位置。

关于起始点的锚点，锚点有四种，分别是 Left、Top、Right、Bottom，分别表示一个节点的左侧、顶部、右侧、下面的边的中间位置，节点与节点之间的边的起始位置都与锚点相连。此外这里还需判断 type 为 formData 的元素是否配置了表单，如果没有配置则通过设置 cursor-not-allow 这个 className 来禁用用户交互，并提示用户需要选择一张工作表才能继续，这是因为我们的流程需要指定一个触发表单才有意义。

接下来，我们只需要在创建边的时候指定边的 type 为 plus 即可使用 CustomEdge 渲染，创建边的逻辑如下：

```tsx
export function edgeBuilder(
  startID?: string,
  endID?: string,
  type = 'plus',
  label = '+',
): Edge {
  return {
    id: `e${startID}-${endID}`,
    type,
    source: startID as string,
    target: endID as string,
    label,
    arrowHeadType: ArrowHeadType.ArrowClosed,
  };
}

const edge = edgeBuilder('startNodeId', 'end');
elements.push(edge);
```

以上即创建了一个类型为 plus 的边，其中 startNodeId 与 end 分别为边的起始节点与结束节点。如果没有指定类型则默认为 plus 类型，label 默认显示一个加号。

### 添加节点

有了自定义节点和自定义边之后，就可以新增节点了。新增节点有多种方式，可以拖拽也可以点击，这里使用较直观的拖拽来实现。

首先给边添加点击事件的处理，在用户点击加号之后，显示可用的节点供用户拖拽。

```tsx
import store, { updateStore } from './store';

export type CurrentConnection = {
  source?: string;
  target?: string;
  position?: XYPosition;
}
export default function CustomEdge(props: EdgeProps): JSX.Element {
  function switcher(currentConnection: CurrentConnection) {
    updateStore((s) => ({ ...s, currentConnection, nodeIdForDrawerForm: 'components' }));
  }

  function onShowComponentSelector(e: MouseEvent<SVGElement>): void {
    e.stopPropagation();
    if (!hasForm) {
      return;
    }
    switcher({ source, target, position: { x: centerX, y: centerY } });
  }

  return (
    <EdgeText
      // ... 省略部分内容
      onClick={onShowComponentSelector}
      // ... 省略部分内容
    />
  )
}
```

在用户点击加号之后，我们首先阻止事件冒泡，防止触发 `react-flow-renderer` 默认的事件处理机制。然后判断用户是否已配置了工作表，如果没有配置，则什么也不做；否则需将当前边所对应的起始节点与结束节点的 id 与边的中点位置记录到状态 store 中。在更改状态的时候指定 nodeIdForDrawerForm 为 components，那么在状态的消费端就会触发节点选择侧边栏的显示，显示节点选择器的代码如下：

```tsx
import React from 'react';

import useObservable from '@lib/hooks/use-observable';
import Drawer from '@c/drawer';

import store, { toggleNodeForm } from '../store';

function DragNode({
  text, type, width, height, iconName, iconClassName
}: RenderProps): JSX.Element {
  function onDragStart(event: DragEvent, nodeType: string, width: number, height: number): void {
    event.dataTransfer.setData('application/reactflow', JSON.stringify({
      nodeType,
      nodeName: text,
      width,
      height,
    }));
    event.dataTransfer.effectAllowed = 'move';
  }

  return (
    <div
      className="bg-gray-100 rounded-8 cursor-move flex items-center overflow-hidden
       border-dashed hover:border-blue-600 border transition"
      draggable
      onDragStart={(e) => onDragStart(e, type, width, height)}
    >
      <Icon name={iconName} size={40} className={cs('mr-4 text-white', iconClassName)} />
      <span className="ml-16 text-body2">{text}</span>
    </div>
  );
}

const nodeLists = [{
  text: '自定义节点1',
  type: 'type1',
  iconName: 'icon1',
  iconClassName: 'bg-teal-500',
}, {
  text: '自定义节点2',
  type: 'type2',
  iconName: 'icon2',
  iconClassName: 'bg-teal-1000',
}];

export default function Components(): JSX.Element {
  const { nodeIdForDrawerForm } = useObservable(store);

  return (
    <>
      {nodeIdForDrawerForm === 'components' && (
        <Drawer
          title={(
            <div>
              <span className="text-h5 mr-16">选择一个组件</span>
              <span className="text-caption text-underline">💡 了解组件</span>
            </div>
          )}
          distanceTop={0}
          onCancel={() => toggleNodeForm('')}
          className="flow-editor-drawer"
        >
          <div>
            <div className="text-caption-no-color text-gray-400 my-12">人工处理</div>
            <div className="grid grid-cols-2 gap-16">
              {nodeLists.map((node) => (
                <DragNode
                  {...node}
                  key={node.text}
                  width={200}
                  height={72}
                />
              ))}
            </div>
          </div>
        </Drawer>
      )}
    </>
  );
}

function App() {
  // 省略部分内容

  return (
    <>
      {/* 省略部分内容 */}
      <Components />
    </>
  )
}
```

这里在 App 中引入 Components 组件，节点选择器由 Components 组件具体实现。其实现过程也很简单，通过 Drawer 组件循环渲染每个 DragNode，DragNode 根据 nodeLists 渲染每一个节点信息。当然，Components 是否渲染取决于 `nodeIdForDrawerForm === 'components'`  是否成立。最后在每个节点开始拖拽时，通过 onDragStart 将节点名称、节点类型以及节点宽高通过 dataTransfer 存储起来。

当用户将节点拖拽到连线中间时，我们做以下处理即可：

```tsx
import { nanoid } from 'nanoid';
import { XYPosition } from 'react-flow-renderer';

import { updateStore } from './store';
import { nodeBuilder } from './utils';

function setElements(eles: Elements): void {
  updateStore((s) => ({ ...s, elements: eles }));
}

function getCenterPosition(position: XYPosition, width: number, height: number): XYPosition {
  return { x: position.x - (width / 2), y: position.y - (height / 2) };
}

function onDrop(e: DragEvent): Promise<void> {
  e.preventDefault();
  if (!e?.dataTransfer) {
    return;
  }
  const { nodeType, width, height, nodeName } = JSON.parse(
    e.dataTransfer.getData('application/reactflow'),
  );
  const { source, target, position } = currentConnection;
  if (!source || !target || !position) {
    return;
  }
  addNewNode({ nodeType, width, height, nodeName, source, target, position });
  updateStore((s) => ({ ...s, currentConnection: {} }));
}

function App() {
  const { elements } = useObservable(store);
  // 省略部分内容

  function addNewNode({ nodeType, width, height, nodeName, source, target, position }) {
    const id = nodeType + nanoid();
    const newNode = nodeBuilder(id, nodeType, nodeName, {
      width,
      height,
      parentID: [source],
      childrenID: [target],
      position: getCenterPosition(position, width, height),
    });
    let newElements = elements.concat([newNode, edgeBuilder(source, id), edgeBuilder(id, target)];
    newElements = removeEdge(newElements, source, target);
    setElements(newElements);
  }

  return (
    <>
      {/* 省略部分内容 */}
      <ReactFlow
        onDrop={onDrop}
      />
    </>
  )
}
```

当拖拽放下的时候执行 onDrop，调用 preventDefault 防止触发 `react-flow-renderer` 的默认行为，然后判断是否存在 dataTransfer，否则返回。接下来通过 nodeType、width、height、nodeName 分别获取节点类型、节点宽度、节点高度、节点名称，再调用 addNewNode 执行新增节点的操作。

完成之后我们需要将 currentConnection 重置为初始值。其中 addNewNode 的过程给节点生成了一个 id，并使用 nodeType 作为前缀，然后调用 nodeBuilder 生成新节点。需要注意我们这里将 source 和 target 记录在了 childrenID 和 parentID 中，以便后续节点的操作。getCenterPosition 用于获取节点的位置，由于需要将节点放在连线中点，节点的起点应该是原始起点减去节点宽高的各一半。

需要的节点准备好之后，接下来需要为新节点生成两条边，并将之前的起始与结束节点之间的连线删除。这里则是分别通过 edgeBuilder 与 removeEdge 实现，removeEdge 由 `react-flow-renderer` 提供，其接收三个参数：第一个是元素的数组；第二个是起始节点的 id；第三个是结束节点的 id。最终返回的是删除起始节点到结束节点之间连线的新的元素数组。最后通过 setElements 将新的元素数组更新到 store 状态中即可更新画布。

### 删除节点

有了添加节点的能力，接下来需要的是删除节点的功能。首先需要在节点的右上角渲染一个删除按钮，当用户点击删除按钮之后，则将当前节点以及与当前节点关联的边一并删除。下面是删除节点组件的实现：

```tsx
import { FlowElement, removeElements } from 'react-flow-renderer';

import Icon from '@c/icon';
import useObservable from '@lib/util/observable';

import store, { updateStore } from './store';

function onRemoveNode(nodeID: string, elements: FlowElement<Data>[]): FlowElement<Data>[] {
  const elementToRemove = elements.find((element) => element.id === nodeID);
  const { parentID, childrenID } = elementToRemove?.data?.nodeData || {};
  const edge = edgeBuilder(parentID, childrenID);
  const newElements = removeElements([elementToRemove], elements);
  return newElements.concat(edge);
}

interface Props {
  id: string;
}

export function NodeRemover({ id }: Props) {
  const { elements } = useObservable(store);

  function onRemove() {
    const newElements = onRemoveNode(id, elements);
    updateStore((s) => ({ ...s, elements: newElements }));
  }

  return (
    <Icon
      name="close"
      onClick={onRemove}
    />
  )
}

function CustomNode({ id }: Props) {
  // 省略部分内容
  return (
    <>
      <NodeRemover id={id}>
    </>
  )
}
```

当点击删除按钮之后，通过当前节点的 id 找到当前节点元素，然后调用 `react-flow-renderer` 提供的 removeElements 方法将当前节点从 elements 中删除即可。之后还需要新增一条前置节点与后续节点的一条连线，保证图是连通的。最后只需在自定义节点中引入 NodeRemover 组件即可。

### 节点配置

节点配置的逻辑类似于添加节点，只不过这里侧边栏组件中渲染的不是供拖拽的节点列表，而是当前对应节点的配置表单。首先需要实现的是点击当前节点展示配置表单，以下是节点点击事件处理的实现：

```tsx
function CustomNode({ id }: Props) {
  // 省略部分内容
  function handleConfig() {
    updateStore((s) => ({
      ...s,
      nodeIdForDrawerForm: id,
    }));
  }

  return (
    <>
      <div onClick={handleConfig}>
        <NodeRemover id={id}>
      </div>
    </>
  )
}
```

当点击节点之后，将 nodeIdForDrawerForm 即当前节点的 id 记录在状态中。接下来实现 ConfigForm 表单：

```tsx
import store, { updateStore } from './store';

import Form from './form';

function ConfigForm() {
  const { nodeIdForDrawerForm, id, name, elements } = useObservable(store);
  const currentNodeElement = elements.find(({ id }) => id === nodeIdForDrawerForm);

  const defaultValue = currentNodeElement?.data?.businessData;

  function onSubmit(data: BusinessData): void {
    const newElements = elements.map(element => {
      if (element.id === nodeIdForDrawerForm) {
        element.data.businessData = data;
      }
      return element;
    })
    updateStore((s) => ({ ...s, elements }))
  }

  function closePanel() {
    updateStore((s) => ({
      ...s,
      nodeIdForDrawerForm: '',
    }));
  }

  return (
    <Form
      defaultValue={defaultValue}
      onSubmit={onSubmit}
      onCancel={closePanel}
    />>
  )
}
```

这里根据 nodeIdForDrawerForm 获取当前节点元素，将它的 businessData 作为默认值传给表单，然后在表单提交的时候将值写回到元素状态中即可。最后如果在点击取消的时候需要关闭侧边栏表单，则只需将 nodeIdForDrawerForm 重置为空即可。

接下来将 ConfigForm 组件引入 App 即可实现点击显示配置表单，关闭侧边栏时不渲染表单的功能：

```tsx
import store from './store';

function App() {
  // 省略部分内容
  const { nodeIdForDrawerForm } = useObservable(store);

  return (
    <>
      {/* 省略部分内容 */}
      <Components />
      {nodeIdForDrawerForm && (
        <ConfigForm />
      )}
    </>
  )
}
```

这里通过判断 nodeIdForDrawerForm 是否存在决定是否渲染表单，当 nodeIdForDrawerForm 被重置为空的时候，表单不会被渲染。

## 问题与难点

目前已知有两个问题：
1. 连线会被节点覆盖，导致连线看不到。
2. 连线与连线之间会有交叉。

对于第一种情况，`react-flow-renderer` 本身并没有提供解决方案，只能靠自己实现 path find 算法。第二种情况则很难解决，当图形很复杂的时候很难避免连线交叉的产生。

## 总结

本文我们从流程设计器的需求，到设计器的数据接口定义，最终实现了一个满足基本要求的流程设计器。不过还有很多需要根据不同业务需求具体进行分析的场景，需要大家在实际业务中去进一步提炼。

### 开源库
>react-flow-renderer:
https://github.com/prahladinala/reactflowrenderer

