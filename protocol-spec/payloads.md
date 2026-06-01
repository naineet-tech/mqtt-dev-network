# Payload Specification

## Device Meter READ Request/Response For Only One Meter

### Request Payload

```json
{
  "messageId": "device/naineet/res",
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

### Response Payload(If data found)

```json
{
    "messageId": "device/naineet/res",
    "opType": "READ",
    "ipAddress": "192.168.1.100:100",
    "ipStatus": true,
    "message" : "success", //Optional
    "meters": [
        {
            "meterId": 2,
            "meterTypeId": 14,
            "data": {
                "status": true,
                "ebLoad": 4.5,
                "dgLoad": 2.0,
                "gridReading": 523.21,
                "dgReading": 86.37,
                "serialNo": "975975",
                "relayStatus": "ON",
                "firmwareVersion": "57",
                "opMode": "KWH",
                "kvaPhaseR": 36.17,
                "kvaPhaseY": 1.05,
                "kvaPhaseB": 26.62,
                "ebRelayR": true,
                "ebRelayY": false,
                "ebRelayB": true,
                "dgRelayR": true,
                "dgRelayY": false,
                "dgRelayB": true,
                "vphaseR": 237.77,
                "vphaseY": 229.82,
                "vphaseB": 231.71,
                "powerKW": 55.67,
                "powerKva": 52.89,
                "powerFactor": 0.88,
                "frequency": 50.19,
                "energySource": "DG",
                "cphaseR": 60.44,
                "cphaseY": 19.88,
                "cphaseB": 29.28,
                "kwphaseR": 14.24,
                "kwphaseY": 37.32,
                "kwphaseB": 35.35,
                "pfactorR": 0.73,
                "pfactorY": 0.96,
                "pfactorB": 0.98
            }
        }
    ]
}
```

### Response Payload(If data not found)

Case 1: When Meter Not Responding

```json
{
    "messageId": "device/naineet/res",
    "opType": "READ",
    "ipAddress": "192.168.1.100:100",
    "ipStatus": true,
    "meters": [
        {
            "meterId": 2,
            "meterTypeId": 14,
            "data": {
                "status": false,
            }
        }
    ]
}
```

Case 2: When IP Not Responding

```json
{
  "messageId" : "device/naineet/res",
  "opType" : "READ",
  "ipAddress" : "192.168.1.100:100",
  "ipStatus" : true,
  "message" : "Unable to connect to 192.168.1.100:100"
}
```
