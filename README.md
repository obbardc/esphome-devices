# esphome-devices

My [ESPHome](https://github.com/esphome) device configurations!


## Building

### Pull latest ESPHome image

```
$ docker pull docker.io/esphome/esphome:latest
```

### Modify secrets file

```
$ cp secrets.example.yaml secrets.yaml
$ vi secrets.yaml
```

### Build

May need to remove cache from previous runs:

```
$ rm -rf .esphome
```

```
$ docker run -it \
  --rm \
  -v "$(pwd)":/config \
  docker.io/esphome/esphome:latest \
  compile \
  pdu-sonoff-s20.yaml
```

### Upload over OTA using web interface

The built firmware for OTA is located under:
```
.esphome/build/<name>/.pioenvs/<name>/firmware.ota.bin
```

### Upload over serial

Press the device button, apply power then run the following command to flash over
serial:

```
$ docker run -it \
  --rm \
  -v "$(pwd)":/config \
  --device=/dev/ttyUSB0 \
  docker.io/esphome/esphome:latest \
  run \
  --device=/dev/ttyUSB0 \
  pdu-s26-0001.yaml
```

### Upload over HTTP OTA

```
$ docker run -it \
  --rm \
  -v "$(pwd)":/config \
  --net=host \
  docker.io/esphome/esphome:latest \
  run \
  pdu-s26-0001.yaml
```


### Change a device's hostname
```
esphome:
  # New hostname
  name: pdu-s26-0001

wifi:
  # Old hostname OR the device's IP address
  use_address: lava-pdu-s26-0001
```
