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

# Triex

Is the pipeline processor.

It defines interfaces and data model, provides tools and runtime to create and execute pipelines.

Processor has a registry of registered configurators, configs and blocks, which are accessible at runtime for pipeline creation.

### Pipeline [\</>](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/source.ts#L83)

Pipeline describes complex event processing model. It consists of nodes and links between nodes.

***

*   **name**: `string`

    Name of the pipeline.
*   **nodes**: `PipelineNodeSpecSource[];` [#](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/source.ts#L59C1-L69C3)

    List of nodes in pipeline.

### Node [\</>](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/source.ts#L59C1-L69C3)

Node represents basic atomic operation within pipeline. Node is made from a block. Being specified in a pipeline, node describes actual block execution options and parameters. Node could have a state, managed by block implementation.

***

*   **name**: `string`

    Name of the node.
*   **block**: `string`

    The type of block describing this node.
* **input**: `PipelineNodeInputSpecSource` (_optional_) [#](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/source.ts#L14)
* **output**: `PipelineNodeOutputSpecSource` (_optional_) [#](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/source.ts#L41)
* **resource**: `string` (_optional_)
* **values**: `object` (_optional_)
* **options**: `object` (_optional_)
* **params**: `object` (_optional_)
* **assert**: `AssertSpec` (_optional_) [#](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/node.ts#L6)

### Link [\</>](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/link.ts#L5)

Link is meant to attach one node output to another node input. Data objects travels from one to another block via link. Link can be configured to limit its troughtput and buffering capabilities. When node reads from its input, it pulls data from attached link. When node writes to its output, it pushed data to attached link. Link is a stateful object, holding buffered data objects as its state. State changes on successful pushes and pulls.

### Block [\</>](https://github.com/yaroslav-korotaev/triex-types/blob/439855db5a87eac450123f9d82cf5a819b670fd1/src/block.ts#L113C26-L113C26)

The core entity. Block implements any basic operation and declares its features and requirements. Block consists of declarations of its inputs and outputs, state, configs, params and lifecycle method implementations.

Block could declare:

* **named inputs** (_zero or more_)
* **named outputs** (_zero or more_)
* **state**
* **named configs** (_zero or more_) created by declared configurator. Could be thought as shared "static" inputs.
* **params** set literally in node specification in a pipeline.
* **`init` method** called once when node is created and added to execution tree.
* **`trigger` method** called back by internal scheduler, if block implemetation had set schuduled triggers.
* **`process` method** called when block inputs are ready for reading.

### Configurator <a href="#user-content-configurator" id="user-content-configurator"></a>

Configurator is a constructor for shared config objects. Block declares which config it needs referring to the name of a specific configurator. Configurator declares config type and a method to create it. It is possible to implement two-step configurator, for example to confirm ownership of an email address with a verification code.

### Config

Config is just a static object, made by some specific configurator. Could be attached to node in a pipeline.

### Stream <a href="#user-content-stream" id="user-content-stream"></a>

Stream is just a special builtin block. This higher-level abstraction is a first class citizen just for a convinience. Stream does not have any inputs, automatically triggers itself and manages its state, allowing developer to implement fetching new data objects like this

`fetch(current state, config, params) => next state + output data objects`.

### Query <a href="#user-content-query" id="user-content-query"></a>

Stream is just a special builtin block. This higher-level abstraction is a first class citizen just for a convinience. Query does not have a state and scheduled triggers, allowing developer to implement some logic like this

`query(input, config, params) => output data objects`.
