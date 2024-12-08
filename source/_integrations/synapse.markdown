---
title: Digital Alchemy Synapse
description: Usage instructions for Digital Alchemy Synapse
ha_category:
  - Hub
ha_release: 2024.4
ha_iot_class: Local Push
ha_platforms:
  - binary_sensor
  - button
  - date
  - datetime
  - lock
  - number
  - scene
  - select
  - sensor
  - switch
  - text
  - time
ha_config_flow: true
ha_codeowners:
  - '@zoe-codez'
---

Digital Alchemy Synapse ([docs](https://docs.digital-alchemy.app/docs/home-automation/synapse/)) integration allows for the creation and management of helper entities and devices from inside of a Typescript based application.

The integration operates by communicating with the connected application via the websocket. There are no configuration options available within the integration

## Creating entities

See external docs for full usage instructions. A basic entity can be created with the following:

```typescript
function ExampleService({ logger, synapse, context }: TServiceParams) {
  synapse.button({
    context,
    name: "Press me",
    press() {
      logger.info("that tickles!");
    }
  })
}
```

### With custom device

```typescript
// 1. register device
const device = synapse.device.register("unique identifier", {
  name: "My cool device",
  ...options
});

synapse.sensor({
  // 2. associate with an entity
  device_id: device,
  ...options
});
```

## Adding your app

Once your app is connected (see external docs), and is running with `LIB_SYNAPSE`, you can this integration through a UI config flow.

The integration will query all connected apps looking for new items. These are presented in a list to pick from, multiple connected apps supported.

## That's it!

The integration works together with the Typescript library to:

- manage entity availability
- emit entity events (button presses, input value changes, turn on/off, etc)
- receive entity state & attribute changes
- create devices & associate virtual entities
- automatic device & entity management

Major functionality for this integration is controlled from the Typescript side.
