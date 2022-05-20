# pdu-esphome

### Improvements

TODO: Integrate into regular Ansible upgrade job

### Pull latest ESPHome image

```
$ docker pull esphome/esphome:latest
```

### Build

```
$ docker run -it \
  --rm \
  -v "${PWD}":/config \
  esphome/esphome:latest \
  compile \
  pdu-sonoff-s20.yaml
```

### Upload over serial

Press the device button, apply power then run the following command to flash over
serial:

```
$ docker run -it \
  --rm \
  -v "${PWD}":/config \
  --device=/dev/ttyUSB0 \
  esphome/esphome:latest \
  run \
  pdu-s26-0001.yaml
```

### Upload over HTTP OTA

```
$ docker run -it \
  --rm \
  -v "${PWD}":/config \
  --net=host \
  esphome/esphome:latest \
  run \
  pdu-s26-0001.yaml
```


### Change a device's hostname
```
esphome:
  # New hostname
  name: pdu-s26-0001

wifi:
  # Old hostname
  use_address: lava-pdu-s26-0001
```
