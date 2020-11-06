# Motioneye Homeassistant MQTT Sensor
A simple script to update motion state in Homeassistant via MQTT
- uses the [binary_sensor](https://www.home-assistant.io/integrations/binary_sensor.mqtt/) component
- has [autodiscovery](https://www.home-assistant.io/docs/mqtt/discovery/)

Its meant to be used by [motioneye](https://github.com/ccrisan/motioneye) 

## Install
Install on a Raspberry Pi running [motioneyeos](https://github.com/ccrisan/motioneyeos)
### Pre build binary
```bash
curl https://github.com/manzari/message-hass-motioneyeos/releases/download/latest/message-hass --output /data/message-hass \
    && chmod +x /data/message-hass
```

### Build from source
```bash
env GOOS=linux GOARCH=arm GOARM=5 \
go build -o ./build/message-hass
```
- copy over the binary from the host`./build/updatemqttmotion` to motioneyeos `/data/updatemqttmotion`
- make it executable `chmod +x /data/updatemqttmotion`
- run it once to generate the default config `/data/updatemqttmotion`

## Configure
### Config File
Edit the file `/data/etc/hass.json` to suit your needs
```json
{
  "Host": "192.168.178.33:1883",
  "User": "user",
  "Pass": "70p53cr37",
  "Dump": false,
  "Retain": false,
  "BaseTopic": "homeassistant",
  "Cameras": [
    {
      "DeviceName": "entrance_camera_motion",
      "DeiceFriendlyName": "Entrance Motion",
      "DeviceClass": "motion"
    }
  ],
  "AutoConfig": true
}
```
### MotionEye UI
- Go the hamburger menu to the left after logging in as admin
- Open the `Motion Notifications` tab
- Enter `bash -c "/data/updatemqttmotion ON"` into the field `Run A Command`
- Enter `bash -c "/data/updatemqttmotion OFF"` into the field `Run An End Command`

#### For additional cameras
- Enter `bash -c "/data/updatemqttmotion -cam=1 ON"` into the field `Run A Command`
- Enter `bash -c "/data/updatemqttmotion -cam=1 OFF"` into the field `Run An End Command`
