---
slug: /development
sidebar_position: 4
---

# Development

Primary, SignalNode has a frontend written in ReactJS (Typescript) and a backend written in Typescript (NodeJS / ExpressJS).

SignalNode should be very generic, so everyone can write integrations. This makes some things more difficult.


## Class Diagram
First let's have a look at the current database schema.

![Example banner](/img/diagrams/class-diagram.png)

**Red highlighted columns may removed in the near future*


## Integration Concept

Integrations are extensions for SingalNode.
At this point an integration has the following interface:

``` typescript
interface SignalNodeIntegration<C, P extends string> {
    configLayout?: SignalNodeConfigLayout<C>, // (optional) - Defines the layout for the configuration of an integration
    properties?: SignalNodeProperty<C, P>, // (optional) - The properties an integration has
    start: (signalBus: SignalBus, serviceManager: SignalNodeServiceManager, config: C) => Promise<void>; // The main function for setting up things
}
```


## Device Concept

A device is a layer to interact with an integration. One device can only represent one integration.

But you can have multiple devices which represents the same integration, but with a different configuration.

> **_NOTE:_**  Maybe the name "device" is no good choice


## Property Concept

A property is an attribute of a device. One device can have multiple properties.

A property stores exact one value, but properties can have a history for saving a value for a specific timestamp.

> **_NOTE:_** There will be a special integration for a "virtual device" which can inject properties from other devices.

