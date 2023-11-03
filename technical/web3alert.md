---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Web3alert

Web3alert manages product-specific entities and renders it down to Triex runtime objects.

Web3alert provides registry for apps, triggers and actions.

### Subscription

Subscription is a combination of triggers and actions. Most basic subscription could be represented by one trigger, and one action – when trigger emits an event then the action is executed.

In fact, subscription consists of rules and actions. Each rule consists of one trigger. All actions are executed, if any rule emits an event.

Subscription is rendered to a Triex pipeline.

### Template <a href="#user-content-template" id="user-content-template"></a>

A template that requires parameters and renders to a Subscription. Contains groups with set of topics, which maps to a set of triggers. Creating subscription from a template is equivalent to filling required template parameters, choosing group, topics and adding actions applied to all topics at once.

### Event <a href="#user-content-event" id="user-content-event"></a>

Ephemeral interface and data structure, which is exists only in subscription context. Triggers must produce objects of the Event interface, and actions must be able to consume so.

Also, data objects, flowing through the pipelines, could be thought as an events. Actually, those objects will have a shape of an Event interface directly in gap between trigger and action, but may have arbitrary shape in other places.

### Trigger <a href="#user-content-trigger" id="user-content-trigger"></a>

Represents something to what user can subscribe to. May have required parameters, which must be specified during subscription setup. Trigger carries a beginning of pipeline, which will be rendered from a subscription. This carried chunk of pipeline could be parametrised with trigger params.

Trigger also contains some metadata such as description and labels that could be used for indexing and grouping.

***

**Properties:**

* **name**: _`string`_
* **project**: _`string`_
* **values**: _`Schema = object`_ [#](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/common.ts#L1)
* **pipeline**: _`TriggerPipeline`_ [#](web3alert.md#triggerpipeline)
* **defaults**: _`TriggerDefaults`_ [#](web3alert.md#triggerdefaults)
* **tags**: _`Tags = string[]`_
* **labels**: _`Labels`_ [#](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/common.ts#L7)
* **meta**: _`TriggerMeta`_ [#](web3alert.md#triggermeta)

#### **TriggerPipeline**

* **output**: _`string`_
* **nodes**: _`PipelineNodeSpecSource[]`_

#### **TriggerDefaults**

* **message**: _`string`_ (_optional_)
* **links**: _`EventLink[]`_ (_optional_) [#](web3alert.md#eventlink)

#### **TriggerMeta**

* **title**: _`string`_
* **description**: _`string`_ (_optional_)

#### **EventLink**

* **text**: _`string`_
* **url**: _`string`_

### Action

Represents something useful user can do with an event. May have required parameters, which must be specified during subscription setup. Action carries an ending of pipeline, which will be rendered from a subscription. This carried chunk of pipeline could be parametrised with trigger params.

Action also contains some metadata such as description and labels that could be used for indexing and grouping.

### Resource

Entity, which will represent shared configs and linked credentials to other services. Renders to Triex configs. Will also be a product of authorization process.

***

* **id**: _`string`_
* **name**: _`string`_
* **fullname**: _`string`_
* **project**: _`string`_ _(optional)_
* **workspace**: _`string`_
* **public**: _`boolean`_
* **blueprint**: _`string`_
* **data**: _`object`_

### App <a href="#user-content-app" id="user-content-app"></a>

Pointer to remote HTTP application, serving implementation of blocks, streams and queries. When app is created, its resources will be discovered and corresponding blocks will be rendered and registered.

### Project <a href="#user-content-project" id="user-content-project"></a>

Container for apps, triggers and actions. Subject for access control. Has metadata for indexing and grouping.

***

* **id**: _`string`_
* **name**: _`string`_
* **fullname**: _`string`_
* **workspace**: _`string`_
* **public**: _`boolean`_
* **meta**: _`ProjectMeta`_

#### ProjectMeta

* **title**: _`string`_
* **description**: _`string`_

### Workspace <a href="#user-content-workspace" id="user-content-workspace"></a>

Represents an organisation or personal account. Container for projects, resources and subscriptions. Subject for access control. Has metadata for indexing and grouping.
