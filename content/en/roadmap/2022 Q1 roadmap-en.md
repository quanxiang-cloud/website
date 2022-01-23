---
title: 'QuanXiang 2022 Q1 open source roadmap'
tag: 'open source, Form, Workflow, Process Design, low-code'
keywords: 'open source, Form, Workflow, Process Design, low-code'
description: 'Hello everyone, 2021 is already gone and we are starting a brand new year. At the beginning of this year, members of the QuanXiang Open Source community will announce QuanXiang's goals and plans for 2022 Q1!'
createTime: '2021-01-21'
author: 'QuanXiang'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/roadmap/cover.png'
---

Hello everyone, 2021 is already gone and we are starting a brand new year. At the beginning of this year, members of the QuanXiang Open Source community will announce QuanXiang's goals and plans for 2022 Q1!

# QuanXiang
First, please allow me to introduce QuanXiang to you.

QuanXiang is a cloud-native, fully containerized open source low-code platform, used to assist in building various types of digital applications for enterprises. The platform currently provides two application development modes: no-code and low-code on the cloud, and supports visual design, allowing developers and business users to quickly complete application development through simple drag-and-drop and parameter configuration. As a multi-application integration and management platform integrating low-code development capability, identity authentication capability and container DevOps capability, QuanXiang supports rapid application building, easy maintenance and management of applications, integration of enterprise stock business and full-image cloud building business.

# Features
QuanXiang builds a low-code ecosystem around application design, development, deployment, operation and maintenance. The core capabilities of the platform are as follows:

### Rapid application development
- Visual designer: Users can complete form, workflow, data_models, and permissions through simple drag and drop, parameter configuration, etc.
- Form engine: Provides rich page components.
- Workflow engine: Supports a variety of triggering methods and process components, and provides the ability of a rule engine to meet the logic definitions of complex businesses.

###  Cloud deployment operation and maintenance
- QuanXiang is based on Kubernetes deployment, CI/CD continuous delivery deployment.
- Support the deployment and operation and maintenance of different cloud vendors.
- Provide system log, support to view all operation records.

### Multi-terminal adaptation
- Apply one-time design and adapt flexibly to multiple ends. Support one-click publishing as WEB App.
- Form engine supports one-click publishing as Native APP.

### Organization management
- Corporate directory：Provide a variety of ways to manage the corporate directory to help companies quickly build an organization.
- Role management: Enterprise role permissions are subdivided to ensure platform account access security and data security.

### System connectivity
- Supports data connection in applications, providing data connection capabilities of different granularity, for example, data linkage update between tables and interaction between fields.

### Pluggable open source
- QuanXiang is a cloud native, distributed architecture platform system. Core services (except for aggregated services) are completely decoupled and low cohesive, and services are accessed through API interfaces.

# Roadmap
In 2022 Q1, QuanXiang will focus on improving the platform's application development capabilities. The platform will add custom pages, support independent access to applications, and support building web-based and simple versions of Native APPs, while significantly optimizing the usability, ease of use, stability and maintainability of the platform. The specific features to be improved include:

### Workflow Capability Improvement
- Add timed task triggering function to solve the need of timed task management in daily use.
- Improve the application of process variables in the workflow to solve the flow of data in the process engine.
- Add Webhook nodes for push, custom API requests.
- Improve the ability to update node data. Support users to modify the form data and the corresponding subform data of the triggering process.

### Page Engine(Custom Page)
- Add the data source types supported by the page engine to unify the management of component data sources.
    - Custom variables: Bind the component to the variable by defining an intermediate variable, and the component will be re-rendered when the variable changes.
    - API request: By defining API variables (in this case, API variables are one of the variables), the API forms a binding relationship with the component, the API sends a request, and when the received data changes, the component is re-rendered.
- New page engine components: including text, images, buttons, containers, input boxes, link text, iframes.
- Support for modifying the style of pages and components: including but not limited to position, size, background color, font and other styles.
- Supports cyclic rendering of component data: provides the ability to render into multiple pieces of data when the API returns multiple pieces of data.
- Supports displaying the component hierarchy of the entire page in the form of an outline tree, and positioning the components in the page by selecting components in the outline tree.
- Support for page lifecycle management: JavaScript syntax logic can be defined on page load and close.

### Others
- Single-application management: Support application independent access. Including application login, approval, filling, etc., all can be managed according to single application for function.
- Application URL settings: In addition to platform URL access, application independent URL access will also be supported.

The above is the development plan for QuanXiang 2022 Q1, if you have different ideas, you can raise an issue to us on GitHub, we look forward to all the comments and suggestions from the community!






