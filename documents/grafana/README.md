
# Grafana

CPU/GPU performance metrics from the Chimera cluster will be visualized and displayed using Grafana. 

## Installation

Macos installation for Grafana can be found [here](https://grafana.com/docs/grafana/latest/setup-grafana/)

Window installation for Grafana can be found [here](https://grafana.com/docs/grafana/latest/setup-grafana/installation/windows/)

Ubuntu 24.04 installation for Grafana can be found [here](https://www.cherryservers.com/blog/install-grafana-ubuntu-2404)

## Homebrew

Homebrew is a package installation helper for Macos and can be found [here](https://brew.sh/)


## Commands

The Grafana service runs locally on port 3000 by default

To start the Grafana service run this command
```bash
systemctl start grafana-server
```
To stop the Grafana service run this command 
```bash
systemctl stop grafana-server
```

# Chimera Dashboard

The Chimera dashboard is deployed inside a VM (Proxmox) provided by UMB. Access to the dashboard can be found by typing http://localhost:3000 in the browser. 

The Grafana installation was deployed inside a VM to avoid sudo complications in previous set ups. 

The Grafana server is deployed using Systemd, which allows the service to run in the background. So starting the Grafana service is not required. 

You can check the Grafana service using this command
```bash
systemctl status grafana-server
```

In order to access the Grafana dashboard in the browser. We will port forward :3000 to our local machine. 

Start up a local terminal and run this command. You can keep this terminal open with a tmux session.
```bash
ssh -L 3000localhost:3000 deploy@ip_address
```

Access to the dashboard panel requires login information.
