# docker-home-automation

## Setup
Create `.env` from `.env.example` and fill the values

## Directories

- `/opt/homeautomation`  this repository
- `/opt/homeassistant`  home assistant data
- `/opt/mosquitto` mosquitto data
- `/opt/zigbee2mqtt` zigbee2mqtt data (contains the Zigbee network key, keep it private and backed up)
- `/opt/portainer` portainer data


## Installing HACS
Reference: https://www.hacs.xyz/docs/use/download/download/#to-download-hacs-container

```bash
# step into docker
docker exec -ti homeassistant bash

# download and run the hacs script
wget -O - https://get.hacs.xyz | bash -
```

Restart home assistant

## installing airco 
Reference: https://community.home-assistant.io/t/mitsubishi-wf-rac-smart-m-air/447917

Install using HACS In HACS go to the three dots int the upper right corner choose add custom repository and add https://github.com/jeatheak/Mitsubishi-WF-RAC-Integration to the list.

## Setup mosquitto
Setup configuration and user/pass
Read: https://github.com/sukesh-ak/setup-mosquitto-with-docker

## Setup zigbee2mqtt
Reference: https://www.zigbee2mqtt.io/guide/installation/02_docker.html

The coordinator is the Sonoff SLZB-06 on the network (`tcp://192.168.1.200:6638`).
Only one program can use it at a time: disable the ZHA integration in Home Assistant before starting zigbee2mqtt.

```bash
# MQTT user for zigbee2mqtt (never use -c here, it would wipe the existing users).
# Use the password_file path from: docker exec mqtt grep password_file /mosquitto/config/mosquitto.conf
docker exec mqtt mosquitto_passwd -b /mosquitto/config/pwfile zigbee2mqtt '<password>'
docker restart mqtt

# configuration
sudo mkdir -p /opt/zigbee2mqtt/data
sudo cp docker/zigbee2mqtt/configuration.yaml.example /opt/zigbee2mqtt/data/configuration.yaml
sudo nano /opt/zigbee2mqtt/data/secret.yaml      # one line: password: '<password>'
sudo chmod 600 /opt/zigbee2mqtt/data/secret.yaml

docker compose up -d zigbee2mqtt
docker logs -f zigbee2mqtt                        # wait for "Zigbee2MQTT started!"
```

The frontend runs on http://<server>:8080. On the first start zigbee2mqtt replaces `GENERATE` in the
configuration with a random network key, PAN ID and extended PAN ID. Back up `/opt/zigbee2mqtt/data`
afterwards: it holds the network key and `coordinator_backup.json`.
