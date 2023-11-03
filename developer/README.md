# Introduction

Welcome to the developer documentation. It is intended to help you with the integration of your product with Web3alert.

Web3alert is an automation platform combined with a public hub of data providers, integrations and pre-configured automation use cases. An integration with a product published in the Web3alert hub is called a **project**. Triggers and actions are published within the project.&#x20;

Currently with our service users can create free subscriptions to monitor certain blockchain events or changes and do actions - for example, send a message to Telegram, Discord, Slack or webhook.

Integration of your project with Web3alert will allow you to:

* create custom triggers
* pre-fill subscription parameters on your frontend to simplify subscription setup for your users. [Here's an example of such pre-fill​](general/integration-example.md)
* feature your project among others on our platform
* eventually, fully self-service your project due to updates of UI, CLI and accesses (planned feature, see the [Roadmap](general/roadmap.md))

### Internal structure <a href="#internal-structure" id="internal-structure"></a>

Web3alert is based on a pipeline processor. A running pipeline can continuously monitor changes in some systems and trigger actions in others. The pipeline runtime allows you to interact with any system, perform complex data transformations, and execute arbitrary code if necessary.

Web3alert provides not only an execution environment for such pipelines but also a simplified model for creating automation scripts. This model is based on triggers and actions. Triggers and actions are premade pieces of pipelines that can be published in a public hub.

The hub allows developers to connect their products to Web3alert and publish pre-configured integration methods with them. Developers will also be able to integrate Web3alert into their products and use the Web3alert runtime to automate certain operations for their users.

Web3alert focuses on integrations with blockchains and dapps. Any blockchain or application can be connected to the Web3alert infrastructure. A typical scenario is to send a notification to the user on a certain event or state change in the blockchain. An application developer can prepare a trigger that listens for the desired event and provide their users with the ability to subscribe to it. At the same time, in most cases, developers will not need to maintain additional infrastructure - the work of monitoring, collecting and converting data will be done in the Web3alert runtime environment.

### Current state and plans <a href="#current-state-and-plans" id="current-state-and-plans"></a>

Web3alert is under active development. The concept of the pipeline runtime and hub was formed some time after the launch of the first version of the product, so we are currently in the process of migrating and implementing new features.

At the moment, the pipeline execution environment is ready and we are preparing it for open access. In addition, we are preparing documentation and tools for developers to test and publish triggers. The features of the public hub of products, integrations, triggers and actions are currently partially implemented on top of the old version of the product and are in the process of being reworked and migrated to the new version.

At the moment, to publish a project or make changes, you need to contact the support (see the[ Integration guide](general/step-by-step-integration-guide.md)). You can describe the task or the necessary triggers, our engineers will prepare, test and publish them. We will transfer your project data to you so that in the future you can edit and publish it yourself.

Our immediate priority goal is to completely transfer control of the published project into the hands of its developer through the web interface and CLI of Web3alert. Project data, including trigger pipelines, is stored in a set of YAML files.

In addition, we are preparing opportunities to integrate alerts into your product. At the moment, the most basic method is ready, in which you can place a special link leading to a Web3alert page with a pre-filled form for creating a subscription from a specific trigger, where the user will only have to select the channel for receiving the notifications. The obvious disadvantage of this method is the need for the user to register with Web3alert and the lack of feedback from Web3alert to your product. Therefore, our next priority is to enable full integration and management of subscriptions within your application.\
