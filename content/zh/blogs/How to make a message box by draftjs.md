---
title: '玩转 draftjs 之制作留言框'
tag: 'draftjs, 留言框, 页面设计, 前端, 低代码'
keywords: 'draftjs, 留言框, 页面设计, 前端, 低代码, low-code'
description: 'draftjs 是用于 react 的富文本编辑器框架，它并不能开箱即用，但是它提供了很多用于开发富文本的 API。基于此，开发者能够搭建出定制化的富文本编辑器。draftjs 有几个重要的概念：EditorState、Entity、SelectionState、CompositeDecorator。'
createTime: '2022-02-18'
author: '谭杰'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/How%20to%20make%20a%20message%20box%20by%20draftjs/cover.png'
---

# draftjs 简介

[draftjs](https://draftjs.org/) 是用于 react 的富文本编辑器框架，它并不能开箱即用，但是它提供了很多用于开发富文本的 API。基于此，开发者能够搭建出定制化的富文本编辑器。draftjs 有几个重要的概念：EditorState、Entity、SelectionState、CompositeDecorator。

### EditorState

EditorState 是编辑器的顶级状态对象。它是一个不可变数据，表示 Draft 编辑器的整个状态，包括:

   - 当前文本内容状态（ContentState）
   - 当前选择状态（SelectionState）
   - 内容的装饰器（Decorator）
   - 撤销/重做堆栈
   - 对内容所做的最新类型的更改（EditorChangeType）

draftjs 基于不可变（immutable）数据，因此对编辑器的修改都需要新生成一个 EditorState 对象传入编辑器，以实现数据更新。

### Entity

Entity 用来描述带有元数据的文本，使一段文本可以携带任意类型的数据，提供了更加丰富的功能，链接、提及和嵌入的内容都可以通过 Entity 来实现。

**Entity的结构**

   ```jsx
   {
       type: 'string', 
       // 表示Entity的类型; eg:'LINK', 'TOKEN', 'PHOTO', 'IMAGE'
       mutability: 'MUTABLE' | 'IMMUTABLE' | 'SEGMENTED', 
       // 此属性表示在编辑器中编辑文本范围时使用此实体对象注释的文本范围的行为。
       data: 'object', 
       // Entity的元数据; 用于存储你想要存储在该Entity里的任何信息
   }
   ```

其中 Mutability 这条属性三个值的含义分别是：

   - Immutable：此 Entity 作为一个整体，一删则整体都删除，无法更改文本;
   - Mutable：Entity 在编辑器中的文字可以自由修改，比如链接文本;
   - Segmented：于 Immutable 类似，区别是可以删除部分文字;

### SelectionState

SelectionState 表示编辑器中的选择范围。一个选择范围有两点：锚点（起点）和焦点（终点）。

   - 锚点位置 === 焦点位置，没有选择文本；
   - 锚点位置 > 焦点位置，从右至左选择文本;
   - 锚点位置 < 焦点位置，从左至右选择文本;

### CompositeDecorator 

Decorator 概念的基础是扫描给定 ContentBlock 的内容，根据定义的策略定位到匹配位置，然后用指定的 React 组件呈现它们。



# 实现一个留言框

首先明确需求:

1. 有长度限制，暂定 200 个字；
2. 提及（@）时高亮，当用户输入 @ 符号后将 @ 符号后面的文字高亮；
3. 插入链接；



先实现一个基础的编辑器：

```jsx
import React from 'react'
import { Editor, EditorState } from 'draft-js';
import 'draft-js/dist/Draft.css';

import './App.css';

function MyEditor() {
  const [editorState, setEditorState] = React.useState(
    () => EditorState.createEmpty(),
  );

  const handleEditorChange = (newEditorState) => {
    setEditorState(newEditorState);
  }

  return (
    <div className='box'>
      <Editor editorState={editorState} onChange={handleEditorChange} />
      <button className='btn'>提交</button>
    </div>
  );
}

export default MyEditor;

```

可以看到并没有出现一个带工具栏的文本框，而是生成一个可编辑区域，接下来我们将赋予他独特的功能。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/How%20to%20make%20a%20message%20box%20by%20draftjs/4.jpg" width = 60%/>
</div>


### 需求一：限制留言长度

编辑器的输入形式有两种：键盘录入和粘贴，一般的 input 输入框我们可以通过 maxLength 来限制，draftjs 没有这个属性，不过提供了 **handleBeforeInput** 和 **handlePastedText** 这两种方法。

#### handleBeforeInput

```jsx
handleBeforeInput?: (
  chars: string, // 输入的内容
  editorState: EditorState, // 编辑器的文本内容状态
  eventTimeStamp: number,
) => 'handled' | 'not-handled'
```

当 handleBeforeInput 返回 handled 的时候输入的默认行为会被阻止，handlePastedText 同理。

#### handlePastedText

```jsx
handlePastedText?: (
  text: string,
  html?: string,
  editorState: EditorState,
) => 'handled' | 'not-handled'
```

接下来修改我们的代码：

```jsx
const MAX_LENGTH = 200;

function MyEditor() {
  const [editorState, setEditorState] = React.useState(
    () => EditorState.createEmpty(),
  );

  const handleEditorChange = (newEditorState) => {
    setEditorState(newEditorState);
  }

  const handleBeforeInput = (_, editorState) => {
    // 获取编辑器的文本内容状态
    const currentContent = editorState.getCurrentContent(); 
    // 获取编辑器文本长度，getPlainText返回当前编辑器的文本内容，字符串类型
    const currentContentLength = currentContent.getPlainText('').length;
    if (currentContentLength > MAX_LENGTH - 1) {
     // 当前文本长度大于最大长度的时候阻止输入，反之允许输入
      return 'handled';
    }

    return 'not-handled';
  }

  return (
    <div className='box'>
      <Editor
        editorState={editorState}
        onChange={handleEditorChange}
        handleBeforeInput={handleBeforeInput}
      />
      <button className='btn'>提交</button>
    </div>
  );
}
```

这里可能有个疑惑：MAX_LENGTH 为什么要减一？

原因是 handleBeforeInput 触发在输入之前，所以 getPlainText 返回的是编辑器内容变化之前的内容。**之前的内容长度+输入的内容长度<最大长度**，因为是键盘输入，所以输入的内容长度始终为1。这还没完，还有选择文本内容后再输入的情况没有处理。这就需要用到SelectionState了。

添加 **getLengthOfSelectedText** 函数：

```JSX
  const getLengthOfSelectedText = () => {
    // 获取编辑器的选择状态
    const currentSelection = editorState.getSelection();
    // 返回选择状态，锚点和焦点的偏移量相同（没有选择）和锚点和焦点的block_key相同时返回true
    const isCollapsed = currentSelection.isCollapsed();
    let length = 0;
    if (!isCollapsed) {
      const currentContent = editorState.getCurrentContent();
      // 获取选择范围的起始位置block_key
      const startKey = currentSelection.getStartKey();
      // 获取选择范围的结束位置block_key
      const endKey = currentSelection.getEndKey();
      if (startKey === endKey) {
        // 选择范围在同一个block，那么选择长度=终点偏移量-起点偏移量
        length += currentSelection.getEndOffset() - currentSelection.getStartOffset();
      } else {
        const startBlockTextLength = currentContent.getBlockForKey(startKey).getLength();
        // 起始block的选择长度 = 起始block的长度-起点偏移量
        const startSelectedTextLength = startBlockTextLength -                                   currentSelection.getStartOffset();
        // 终点在结束block中的偏移量
        const endSelectedTextLength = currentSelection.getEndOffset();
        // getKeyAfter返回指定key的block后面一个block的key
        const keyAfterEnd = currentContent.getKeyAfter(endKey);
        let currentKey = startKey;
        // 累加起始block到结束block中间的block的选择长度
        while (currentKey && currentKey !== keyAfterEnd) {
          if (currentKey === startKey) {
            length += startSelectedTextLength + 1;
          } else if (currentKey === endKey) {
            length += endSelectedTextLength;
          } else {
            length += currentContent.getBlockForKey(currentKey).getLength() + 1;
          }

          currentKey = currentContent.getKeyAfter(currentKey);
        }
      }
    }

    return length;
  };
```

这个方法有些长，又涉及到 draftjs 的几个 api 和 block 的概念，稍微复杂点，不过用途很简单，就是获取选择的长度。现在我们来改造下 handleBeforeInput：

```jsx
    const handleBeforeInput = (_, editorState) => {
    const currentContent = editorState.getCurrentContent();
    const currentContentLength = currentContent.getPlainText('').length;
    // 实际长度 = 当前内容的长度-选择的长度（被替换的长度）
    if (currentContentLength - getLengthOfSelectedText() > MAX_LENGTH - 1) {
      return 'handled';
    }

    return 'not-handled';
  }
```

依葫芦画瓢，现在我们来添加 handlePastedText，如果是粘贴情况下，则多了个 pastedText（被粘贴的文本）参数。

```jsx
  const handlePastedText = (pastedText) => {
    const currentContent = editorState.getCurrentContent();
    const currentContentLength = currentContent.getPlainText('').length;
    const selectedTextLength = getLengthOfSelectedText();
    if (currentContentLength + pastedText.length - selectedTextLength > maxLength - 1) {
      return 'handled';
    }

    return 'not-handled';
  };
```

为了有更好的使用体验，可以在编辑器右下角加一个当前内容长度/最大长度的提示。改造一下 handleEditorChange 方法，把当前文本长度用 state 存储起来。

```jsx
  const handleEditorChange = (newEditorState) => {
    const currentContent = newEditorState.getCurrentContent();
    const currentContentLength = currentContent.getPlainText('').length;
    setLength(currentContentLength);
    setEditorState(newEditorState);
  }
```

调整一下样式，看下效果：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/How%20to%20make%20a%20message%20box%20by%20draftjs/1.jpg" width = 60%/>
</div>

至此我们就完成了第一个需求。



### 需求二：提及（@）时高亮

一般提及都会有把 @ 符号后面的文字改变颜色以示区别，我们可以用一个正则表达式来匹配 @ 符号和后面的文本，然后在替换成我们自定义的 ReactNode，就可以实现高亮，这正是 Decorator 的用武之地。

我们只需要创建一个 CompositeDecorator 实例，在编辑器初始化的时候传入 createEmpty 中就可以了。

```jsx
  const HANDLE_REGEX = /@[\w]+/g;
  const compositeDecorator = new CompositeDecorator([
    {
      strategy: (contentBlock, callback) => {
        // 编辑器每次change都会触发此函数，得到内容文本。
        const text = contentBlock.getText();
        let matchArr, start;
        while ((matchArr = HANDLE_REGEX.exec(text)) !== null) {
          // 得到匹配值的起始位置和偏移量，callback之后就会被此decorator的component替换
          start = matchArr.index;
          callback(start, start + matchArr[0].length);
        }
      },
      component: (props) => {
        return (
          <span
            className='mention'
            data-offset-key={props.offsetKey}
          >
            {props.children}
          </span>
        );
      },
    },
  ]);

  const [editorState, setEditorState] = React.useState(
    () => EditorState.createEmpty(compositeDecorator),
  );
```

看下效果：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/How%20to%20make%20a%20message%20box%20by%20draftjs/2.jpg" width = 60%/>
</div>



### 需求三：插入链接

链接显示文字，鼠标移入提示 url。纯文本已经无法描述这段信息了，这就需要用到 Entity。添加 insertEntity 函数：

```jsx
  const insertEntity = (entityData) => {
    let contentState = editorState.getCurrentContent();
      // 创建实体
    contentState = contentState.createEntity('LINK', 'IMMUTABLE', entityData);
    const entityKey = contentState.getLastCreatedEntityKey();
    let selection = editorState.getSelection();
      // 判断是替换还是插入
    if (selection.isCollapsed()) {
      contentState = Modifier.insertText(
        contentState, selection, entityData.name + ' ', undefined, entityKey,
      );
    } else {
      contentState = Modifier.replaceText(
        contentState, selection, entityData.name + ' ', undefined, entityKey,
      );
    }

    let end;
      // 获取实体在编辑器中显示的范围，目的是让光标在插入实体后停留在实体尾部
    contentState.getFirstBlock().findEntityRanges(
      (character) => character.getEntity() === entityKey,
      (_, _end) => {
        end = _end;
      });

    let newEditorState = EditorState.set(editorState, { currentContent: contentState });
    selection = selection.merge({
      anchorOffset: end,
      focusOffset: end,
    });
    newEditorState = EditorState.forceSelection(newEditorState, selection);
    handleEditorChange(newEditorState);
  };
```

看下效果：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/How%20to%20make%20a%20message%20box%20by%20draftjs/3.jpg" width = 60%/>
</div>

完成！

### 引用内容
>draftjs：https://draftjs.org/

# 完整代码

```jsx
import React, { useState } from 'react'
import { Editor, EditorState, CompositeDecorator, Modifier, convertToRaw } from 'draft-js';
import 'draft-js/dist/Draft.css';

import './App.css';

const MAX_LENGTH = 200;
const HANDLE_REGEX = /@[\w]+/g;
const URL_LIST = [
  {
    url: 'https://www.baidu.com/',
    name: '百度'
  }, {
    url: 'https://www.google.com.hk/',
    name: '谷歌'
  }, {
    url: 'https://developer.mozilla.org/zh-CN/',
    name: 'MDN'
  },
]

function MyEditor() {
  const compositeDecorator = new CompositeDecorator([
    {
      strategy: (contentBlock, callback) => {
        const text = contentBlock.getText();
        let matchArr, start;
        while ((matchArr = HANDLE_REGEX.exec(text)) !== null) {
          start = matchArr.index;
          callback(start, start + matchArr[0].length);
        }
      },
      component: (props) => {
        return (
          <span
            className='mention'
            data-offset-key={props.offsetKey}
          >
            {props.children}
          </span>
        );
      },
    },
    {
      strategy: (contentBlock, callback, contentState) => {
        contentBlock.findEntityRanges(
          (character) => {
            const entityKey = character.getEntity();
            if (entityKey === null) {
              return false;
            }
            return contentState.getEntity(entityKey).getType() === 'LINK';
          },
          callback
        );
      },
      component: (props) => {
        return (
          <span title={props.contentState.getEntity(props.entityKey).data.url} data-offset-key={props.offsetkey} className='url'>
            {props.children}
          </span>
        )
      },
    },
  ]);
  const [value, setValue] = useState('');
  const [textLength, setLength] = useState(0);
  const [editorState, setEditorState] = React.useState(
    () => EditorState.createEmpty(compositeDecorator),
  );

  const handleEditorChange = (newEditorState) => {
    const currentContent = newEditorState.getCurrentContent();
    const currentContentLength = currentContent.getPlainText('').length;
    setLength(currentContentLength);
    setEditorState(newEditorState);
  }

  const submit = () => {
    const content = editorState.getCurrentContent();
    const { blocks, entityMap } = convertToRaw(content);
    const v = blocks.map((block) => {
      let text = block.text;
      block.entityRanges.forEach(({ key }) => {
        text = text.replace(entityMap[key].data.name, `${entityMap[key].data.name}:${entityMap[key].data.url}`);
      });
      return text;
    }).join(' ');
    setValue(v);
  }

  const insertEntity = (entityData) => {
    let contentState = editorState.getCurrentContent();
    contentState = contentState.createEntity('LINK', 'IMMUTABLE', entityData);
    const entityKey = contentState.getLastCreatedEntityKey();
    let selection = editorState.getSelection();
    if (selection.isCollapsed()) {
      contentState = Modifier.insertText(
        contentState, selection, entityData.name + ' ', undefined, entityKey,
      );
    } else {
      contentState = Modifier.replaceText(
        contentState, selection, entityData.name + ' ', undefined, entityKey,
      );
    }

    let end;
    contentState.getFirstBlock().findEntityRanges(
      (character) => character.getEntity() === entityKey,
      (_, _end) => {
        end = _end;
      });

    let newEditorState = EditorState.set(editorState, { currentContent: contentState });
    selection = selection.merge({
      anchorOffset: end,
      focusOffset: end,
    });
    newEditorState = EditorState.forceSelection(newEditorState, selection);
    handleEditorChange(newEditorState);
  };

  const getLengthOfSelectedText = () => {
    const currentSelection = editorState.getSelection();
    const isCollapsed = currentSelection.isCollapsed();
    let length = 0;
    if (!isCollapsed) {
      const currentContent = editorState.getCurrentContent();
      const startKey = currentSelection.getStartKey();
      const endKey = currentSelection.getEndKey();
      if (startKey === endKey) {
        length += currentSelection.getEndOffset() - currentSelection.getStartOffset();
      } else {
        const startBlockTextLength = currentContent.getBlockForKey(startKey).getLength();
        const startSelectedTextLength = startBlockTextLength - currentSelection.getStartOffset();
        const endSelectedTextLength = currentSelection.getEndOffset();
        const keyAfterEnd = currentContent.getKeyAfter(endKey);
        let currentKey = startKey;
        while (currentKey && currentKey !== keyAfterEnd) {
          if (currentKey === startKey) {
            length += startSelectedTextLength + 1;
          } else if (currentKey === endKey) {
            length += endSelectedTextLength;
          } else {
            length += currentContent.getBlockForKey(currentKey).getLength() + 1;
          }

          currentKey = currentContent.getKeyAfter(currentKey);
        }
      }
    }

    return length;
  };

  const handleBeforeInput = () => {
    const selectedTextLength = getLengthOfSelectedText();
    if (textLength - selectedTextLength > MAX_LENGTH - 1) {
      return 'handled';
    }

    return 'not-handled';
  }

  const handlePastedText = (pastedText) => {
    const selectedTextLength = getLengthOfSelectedText();
    if (textLength + pastedText.length - selectedTextLength > MAX_LENGTH - 1) {
      return 'handled';
    }

    return 'not-handled';
  };

  return (
    <div className='box'>
      <div className='urlBox'>
        {URL_LIST.map((urlObj) => (
          <span onClick={() => insertEntity(urlObj)} className='urlSpan' key={urlObj.url}>{urlObj.name}</span>
        ))}
      </div>
      <div className='editor'>
        <Editor
          editorState={editorState}
          onChange={handleEditorChange}
          handlePastedText={handlePastedText}
          handleBeforeInput={handleBeforeInput}
        />
        <div className='tips'>{textLength}/{MAX_LENGTH}</div>
      </div>
      <button onClick={submit} className='btn'>提交</button>
      <div style={{marginTop: '15px'}}>
        {value}
      </div>
    </div>
  );
}

export default MyEditor;
```

