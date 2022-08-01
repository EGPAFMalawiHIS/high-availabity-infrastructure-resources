# Resources for Scale and High Availability

This repo contains miscellaneous resources for redundancy, data backup and recovery, automatic failover, and load balancing

## What is High Availability (HA)

High availability is a function of system design that allows an application to automatically restart or reroute work to another capable system in the event of a failure. In terms of servers, there are a few different technologies needed to set up a highly available system. There must be a component that can redirect the work and there must be a mechanism to monitor for failure and transition the system if an interruption is detected. Google did a pretty decent job on explaining HA, you can read about it [here](https://cloud.google.com/architecture/framework/reliability/design-scale-high-availability)

## Resources that you'll find in this repo

### Automatic failover (for Nginx)

This section discusses configuration for an active-passive Nginx pair in a solution based on keepalived and VRRP. You can read more about Keepalived [here](https://keepalived.readthedocs.io/en/latest/introduction.html)

#### Set up guide

In order to complete this failover guide, you will need two Ubuntu 20.04 servers. The servers should be on the same network. We will call the first server, "Primary", and the second one "Secondary".

On each of these servers, you will need a non-root user configured with sudo access and follow the steps below:

1; First, update your existing list of packages:

```bash
apt update 
```

2; Next, install Keepalived

```bash
sudo apt install keepalived
```

3; Optionally, you might also need to install libipset13

```bash
sudo apt install libipset13
```

4; The service looks for configuration in /etc/keepalived/keepalived.conf. Create that file on both of the servers:

```bash
nano /etc/keepalived/keepalived.conf
```

5; You can find keepalived.conf under automatic-failover on this repo. For more configurations read the official documentation [here](https://keepalived.readthedocs.io/en/latest/configuration_synopsis.html). Paste the template on your keepalived.conf on both servers and make changes to the configurations accordingly.

6; Activate the service:

```bash
sudo systemctl enable --now keepalived.service
```
