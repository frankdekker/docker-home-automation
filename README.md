# docker-home-automation

## Setup
Create `.env` from `.env.example` and fill the values

## Directories

- `/opt/homeautomation`  this repository
- `/opt/homeassistant`  home assistant data
- `/opt/mosquitto` mosquitto data
- `/opt/zigbee2mqtt` zigbee2mqtt data
- `/opt/portainer` portainer data

## Setup mosquitto
Setup configuration and user/pass
Read: https://github.com/sukesh-ak/setup-mosquitto-with-docker

## Troubleshooting

### Cant connect to Sonoff zigbee adapter
- mostlikely the socket is still taken
  - log in to the sonoff adapter 192.168.1.200
  - check dashboard for socket clients
  - change sonoff port and restart the adapter
