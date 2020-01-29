# Motioneye MQTT
A simple script to alert homeassistant via mqtt
- uses the binary_sensor component
- has autodiscovery

## Install
### Pre build binary
```bash
curl https://tba/latest/updatemqttmotion --output /data/updatemqttmotion \
    && chmod +x /data/updatemqttmotion
```

### Build
```bash
env GOOS=linux GOARCH=arm GOARM=5 \
go build -o ./build/updatemqttmotion github.com/manzari/motioneyeos_mqtt #gosetup
```

## Configure
### Config File
`/data/etc/updatemqttmotion.json`
```json
{
  "Host": "192.168.178.33:1883",
  "User": "user",
  "Pass": "70p53cr37",
  "Dump": false,
  "Retain": false,
  "BaseTopic": "homeassistant",
  "DeviceName": "entrance_camera_motion",
  "DeiceFriendlyName": "Entrance Motion",
  "DeviceClass": "motion"
}
```
### MotionEye UI
- Go the hamburger menu to the left after logging in as admin
- Open the `Motion Notifications` tab
- Enter `bash -c "/data/updatemqttmotion ON"` into the field `Run A Command`
- Enter `bash -c "/data/updatemqttmotion OFF"` into the field `Run An End Command`

