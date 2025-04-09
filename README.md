# docker-home-automation

## Setup
Create `.env` from `.env.example` and fill the values

## Directories

- `/opt/homeautomation`  this repository
- `/opt/homeassistant`  home assistant data
- `/opt/mosquitto` mosquitto data
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

