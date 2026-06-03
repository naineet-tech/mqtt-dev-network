# MQTT Client Integration Guide

## Broker Configuration

| Parameter  | Value                                             |
| ---------- | ------------------------------------------------- |
| Broker URL | `a33vst7pv0zvsa-ats.iot.ap-south-1.amazonaws.com` |
| Port       | `8883`                                            |
| Protocol   | MQTT over TLS/SSL                                 |

---

## Client ID Requirements

All MQTT clients must use a Client ID prefixed with:

```text
naineet_
```

### Valid Examples

```text
naineet_a3bea4
naineet_4i9sfi4
naineet_11111
naineet_test_client
```

---

## Topic Structure

### Request Topic

Publish requests to:

```text
device/jack
```

Example Request:

```json
{
  "messageId": "device/naineet",
  "ipAddress": "192.168.1.100:100",
  "opType": "READ",
  "meters": [
    {
      "meterId": 2,
      "meterTypeId": 14
    }
  ]
}
```

---

### Response Topic

The client must provide its own response topic using the `messageId` field.

> **Important:** All topic(pub/sub) name must always start with the `device/` prefix.

#### Valid Topic Examples

```text
device/my-client
device/dashboard
device/client-01
device/test123
device/naineet
device/naineet/response
```

#### Invalid Examples

```text
my-client
response-topic
client/test
```

Example in your request body:

```json
{
  "messageId": "device/naineet"
}
```

The MQTT Device Client will publish the response to:

```text
device/naineet
```

---

### Error Topic

All processing errors are published to:

```text
device/jack/error
```

Clients should subscribe to this topic if they want to receive error notifications.

---

## Recommended Subscriptions

Subscribe to:

```text
device/<your-topic>
device/jack/error
```

Example:

```text
device/naineet
device/jack/error
```

---

## Communication Flow

```text
┌───────────────┐
│ MQTT Client   │
└───────┬───────┘
        │
        │ Subscribe
        ├──────────────────► device/naineet
        │
        ├──────────────────► device/jack/error
        │
        │ Publish Request
        ▼
     device/jack
        │
        ▼
┌──────────────────────────────────────────┐
│ AWS IoT MQTT Broker (MQTT Device Client) │
│ Port: 8883                               │
└──────────────┬───────────────────────────┘
               │
      ┌────────┴────────┐
      │                 │
      ▼                 ▼

device/naineet   device/jack/error
   (Success)           (Failure)
```

---

## Architecture Diagram

Excalidraw Reference:

```text
https://excalidraw.com/#json=iEaXo_yuD4rRqcgIfi_Th,usp1dWOa06-3PUE3tSUUIg
```

---

## Quick Summary

| Purpose                        | Topic                 |
| ------------------------------ | --------------------- |
| Publish Requests               | `device/jack`         |
| Receive Responses              | `device/<your-topic>` |
| Error Notifications            | `device/jack/error`   |
| Required Topic Prefix          | `device/`             |
| Required Client ID Prefix      | `naineet_`            |

---

## Example Client Configuration

```yaml
broker: a33vst7pv0zvsa-ats.iot.ap-south-1.amazonaws.com
port: 8883
clientId: naineet_a3bea4

subscribe:
  - device/naineet
  - device/jack/error

publish:
  - device/jack
```
