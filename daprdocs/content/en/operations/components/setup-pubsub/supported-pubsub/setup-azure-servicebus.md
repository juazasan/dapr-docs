---
type: docs
title: "Azure Service Bus"
linkTitle: "Azure Service Bus"
description: "Detailed documentation on the Azure Service Bus pubsub component"
---

## Setup Azure Service Bus

Follow the instructions [here](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-quickstart-topics-subscriptions-portal) on setting up Azure Service Bus Topics.

## Create a Dapr component

The next step is to create a Dapr component for Azure Service Bus.

Create the following YAML file named `azuresb.yaml`:

```yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: <NAME>
  namespace: <NAMESPACE>
spec:
  type: pubsub.azure.servicebus
  version: v1
  metadata:
  - name: connectionString
    value: <REPLACE-WITH-CONNECTION-STRING> # Required.
  - name: timeoutInSec
    value: <REPLACE-WITH-TIMEOUT-IN-SEC> # Optional. Default: "60". Timeout for sending messages and management operations.
  - name: handlerTimeoutInSec
    value: <REPLACE-WITH-HANDLER-TIMEOUT-IN-SEC> # Optional. Default: "60". Timeout for invoking app handler.
  - name: disableEntityManagement
    value: <REPLACE-WITH-DISABLE-ENTITY-MANAGEMENT> # Optional. Default: false. When set to true, topics and subscriptions do not get created automatically.
  - name: maxDeliveryCount
    value: <REPLACE-WITH-MAX-DELIVERY-COUNT> # Optional. Defines the number of attempts the server will make to deliver a message.
  - name: lockDurationInSec
    value: <REPLACE-WITH-LOCK-DURATION-IN-SEC> # Optional. Defines the length in seconds that a message will be locked for before expiring.
  - name: lockRenewalInSec
    value: <REPLACE-WITH-LOCK-RENEWAL-IN-SEC> # Optional. Default: "20". Defines the frequency at which buffered message locks will be renewed.
  - name: maxActiveMessages
    value: <REPLACE-WITH-MAX-ACTIVE-MESSAGES> # Optional. Default: "10000". Defines the maximum number of messages to be buffered or processing at once.
  - name: maxActiveMessagesRecoveryInSec
    value: <REPLACE-WITH-MAX-ACTIVE-MESSAGES-RECOVERY-IN-SEC> # Optional. Default: "2". Defines the number of seconds to wait once the maximum active message limit is reached.
  - name: maxConcurrentHandlers
    value: <REPLACE-WITH-MAX-CONCURRENT-HANDLERS> # Optional. Defines the maximum number of concurrent message handlers
  - name: prefetchCount
    value: <REPLACE-WITH-PREFETCH-COUNT> # Optional. Defines the number of prefetched messages (use for high throughput / low latency scenarios)
  - name: defaultMessageTimeToLiveInSec
    value: <REPLACE-WITH-MESSAGE-TIME-TO-LIVE-IN-SEC> # Optional.
  - name: autoDeleteOnIdleInSec
    value: <REPLACE-WITH-AUTO-DELETE-ON-IDLE-IN-SEC> # Optional.
```

> __NOTE:__ The above settings are shared across all topics that use this component.

{{% alert title="Warning" color="warning" %}}
The above example uses secrets as plain strings. It is recommended to use a secret store for the secrets as described [here]({{< ref component-secrets.md >}}).
{{% /alert %}}

## Apply the configuration

Visit [this guide]({{< ref "howto-publish-subscribe.md#step-2-publish-a-topic" >}}) for instructions on configuring pub/sub components.

## Related links
- [Pub/Sub building block]({{< ref pubsub >}})