# esphome-devices

My [ESPHome](https://github.com/esphome) device configurations!


## Building

### Pull latest ESPHome image

```
$ docker pull esphome/esphome:latest
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
  -v "$(pwd)":/config \
  --device=/dev/ttyUSB0 \
  esphome/esphome:latest \
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
  # Old hostname OR the device's IP address
  use_address: lava-pdu-s26-0001
```
