# Event-based and state-based alerts

Event-based alerts are regular alerts triggered by an on-chain event.

State-based alerts are triggered by **stateful events -** a concept used for alerts that do not have a specific triggering on-chain event, but require monitoring of a specific value in the blockchain (e.g. gas price, collateralization ratio, treasury balance updates, etc.). Here is what that concept requires and how it works**:**

* Event
  * Name
  * Parameters
* Subscription rule
  * Event name
  * Conditions
  * Execution policy
* Subscription rule execution policy
  * Trigger execution policy
  * Watch execution policy
    * state
    * "for" parameter (waiting time)

The **event** contains a **name** (internal technical identifier) and may contain **parameters** (e.g. "recipient address", "token ticker" or "validator list").&#x20;

A **subscription rule** contains the **name of the event** to be tracked and may contain a **condition** under which the rule must be executed. A condition is a logical expression from event parameters, such as "recipient address is X" or "validator list has address Y". Besides that, you can specify an **execution policy** for the subscription rule.&#x20;

An **execution policy** can be:

* a **trigger execution policy.** A notification is sent each time a watched event occurs which satisfies the subscription rule.&#x20;
* a **watch execution policy.** With this policy, a subscription rule can be in three **states** - standby, pending and firing. The watch execution policy has an additional parameter "**for"** - waiting time for transition from pending to firing state. A notification is sent each time a rule goes from the pending to the firing state.&#x20;

State transitions work as follows:

* By default, the subscription rule is in the standby state
* As long as the occurring events monitored by the rule do NOT meet the condition, the subscription rule remains in standby state
* When a monitored event occurs and satisfies the condition, the subscription rule will go into the pending state
* If the subscription rule stays in the pending state longer than specified in the policy parameter "**for**" it goes into the firing state
* If in the pending or firing state a monitored event occurs and does NOT meet the condition, the rule will return to the standby state

You can also refer to the alert execution model of AlertManager/Grafana - the concept was taken from there [https://grafana.com/docs/grafana/latest/alerting/alerting-rules/](https://grafana.com/docs/grafana/latest/alerting/alerting-rules/)
