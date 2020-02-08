# Wiser

## Setup

### 1 - Find your secret

Connection to the Drayton hub is done through a local LAN connection rather than via the cloud. This requires an app "secret" that the hub provides. To access this secret you need to jump through a couple of hoops:

1. Log out of the app. Make sure you’re at the login screen
1. Tap Setup / Create Account (even though your system has already been set up).
1. Select the HubR type you have
1. Press the Setup button on the hub
1. This will start the WiserHeatXXX access point.
1. Connect to WiserHeatXXX with you device or a real computer. You should get an IP in the 192.168.8.0/24 range from the hub's DHCP server.
1. Go to http://192.168.8.1/secret/ in a web browser. You'll set a long string of seemingly random numbers. This is your secret!
1. Now finish the setup…
1. Follow the on-screen instructions to connect your smartphone to WiserHeatXXX
1. Tap Skip when prompted to set up your heating system.
1. Follow the on-screen instructions to connect your Heat HubR to the
1. Internet by selecting your new Wi-Fi network.
1. Tap Skip when prompted to register an account.
1. You have now changed to a new Wi-Fi network. You will see the home screen and can proceed to control your heating as normal.

### 2 - Find your Wiser hub IP Address

Find and remember the hub address

## Get Domain Details

method: `GET`

address: `/data/domain/`

response:

```json
{
    "System": {...},
    "Cloud": {...},
    "HeatingChannel": [
        {...}
    ],
    "Room": [...],
    "Device": [...],
    "Zigbee": {...},
    "UpgradeInfo": [...],
    "SmartValve": [...],
    "RoomStat": [...],
    "SmartPlug": [...],
    "DeviceCapabilityMatrix": {...},
    "Schedule": [...]
}
```

[Full response](responses/domain.json)

## Get System Details

method: `GET`

address: `/data/domain/System`

response:

```json
{
    "PairingStatus": "Paired",
    "TimeZoneOffset": 0,
    "AutomaticDaylightSaving": true,
    "SystemMode": "Heat",
    "FotaEnabled": true,
    "ValveProtectionEnabled": false,
    "EcoModeEnabled": true,
    "AwayModeAffectsHotWater": true,
    "AwayModeSetPointLimit": 80,
    "BoilerSettings": { },
    "CoolingModeDefaultSetpoint": 210,
    "CoolingAwayModeSetpointLimit": 240,
    "ComfortModeEnabled": false,
    "PreheatTimeLimit": 10800,
    "DegradedModeSetpointThreshold": 180,
    "UnixTime": 1581156420,
    "ActiveSystemVersion": "2.44.0-0b3fba4327",
    "BrandName": "WiserHeat",
    "CloudConnectionStatus": "Connected",
    "LocalDateAndTime": { },
    "HeatingButtonOverrideState": "Off",
    "HotWaterButtonOverrideState": "Off",
    "OpenThermConnectionStatus": "Disconnected"
}
```

[Full response](responses/system.json)

## Get Rooms Details

method: `GET`

address: `/data/domain/Room`

response:

```json
[
    {
        "id": 1,
        "ManualSetPoint": 70,
        "ScheduleId": 1,
        "HeatingRate": 1200,
        "RoomStatId": 1,
        "Name": "hallway",
        "Mode": "Manual",
        "DemandType": "Modulating",
        "WindowDetectionActive": false,
        "ControlSequenceOfOperation": "HeatingOnly",
        "HeatingType": "HydronicRadiator",
        "CalculatedTemperature": 149,
        "CurrentSetPoint": 70,
        "PercentageDemand": 0,
        "ControlOutputState": "Off",
        "SetpointOrigin": "FromManualMode",
        "DisplayedSetPoint": 70,
        "ScheduledSetPoint": 170,
        "RoundedAlexaTemperature": 150,
        "EffectiveMode": "Manual",
        "PercentageDemandForItrv": 0
    },
    {...}
]
```

[Full response](responses/rooms.json)

## Get Room Details

method: `GET`

address: `/data/domain/Room/{room_id}`

response:

```json
{
    "id": 1,
    "ManualSetPoint": 70,
    "ScheduleId": 1,
    "HeatingRate": 1200,
    "RoomStatId": 1,
    "Name": "hallway",
    "Mode": "Manual",
    "DemandType": "Modulating",
    "WindowDetectionActive": false,
    "ControlSequenceOfOperation": "HeatingOnly",
    "HeatingType": "HydronicRadiator",
    "CalculatedTemperature": 149,
    "CurrentSetPoint": 70,
    "PercentageDemand": 0,
    "ControlOutputState": "Off",
    "SetpointOrigin": "FromManualMode",
    "DisplayedSetPoint": 70,
    "ScheduledSetPoint": 170,
    "RoundedAlexaTemperature": 150,
    "EffectiveMode": "Manual",
    "PercentageDemandForItrv": 0
}
```

## Change temperature

method: `PATCH`

address: `/data/domain/Room/{room_id}`

body:

```json
{
    "RequestOverride": {
        "Type": "Manual",
        "SetPoint": 100
    }
}
```

error response:

```json
{
    "Error": "Manual override requires a 'SetPoint' between 50 and 300 or -200 (i.e. from 5 to 30 degreesC or Off)"
}
```

## Manage Away Mode

TODO

## Smart Plugs

TODO
