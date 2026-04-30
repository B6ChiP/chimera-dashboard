
# Chimera 

Chimera is a heterogeneous distributed memory high performance compute cluster. 

Additional information on CPU/GPU nodes can be found [here](https://www.umb.edu/rc/hpc/chimera/)

## Set up

Generate an ssh key for deploy@b6 to store on Chimera by running this command
```bash
ssh-keygen
```

Configure port forwarding in the ssh config file on deploy@b6. This will allow us to open up both node_exporter and dcgm_exporter ports automatically
```bash
.ssh/config
```
```
Host chimera
    HostName chimera.umb.edu
    User blake.moody001
    LocalForward 9101 localhost:9101
    LocalForward 9401 chimera21:9401
    SessionType none
```

## Running the command

ssh into Chimera by running this command
```bash
ssh - fN chimera
```

## Tmux 

Create tmux session on deploy@b6

Make sure the prometheus yaml file is configured for ports 9401 and 9101. 

Start the node_exporter on port 9101 by running this command
```bash
cd node_exporter && ./node_exporter --web.listen-address=:9101
```