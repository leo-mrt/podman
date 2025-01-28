# zabbix-podman
A Zabbix server (with pgsql/alpine tag) with web interface (nginx) in podman, with quadlet implementation (Kubernetes ready).


## Getting started
This deployment uses docker hub published offical containers for Zabbix.  

Edit `zabbix-cm.yml` to your liking (changing things like passwords, usernames...) and then either run directly with:

#`podman kube play zabbix-secrets.yml` #postgresql does not support base64 encoded secret 
`podman play kube --configmap=zabbix-cm.yml pgsql-pod.yml`
`podman play kube --configmap=zabbix-cm.yml zabbix-server-pod.yml`
`podman play kube --configmap=zabbix-cm.yml zabbix-web-pod.yml`

OR use Quadlet (systemd) in rootless mode:

Copy all the yml/quadlet files to user systemd directory `$HOME/.config/containers/systemd/`.

Then run `systemctl --user daemon-reload` and you should now have services called `pgsql-pod.service, zabbix-server-pod.service, zabbix-web-pod.service` that you can enable and start. 

Use `loginctl enable-linger $USER` as root to allow a user to keep background processes running even after disconnecting from an interactive session.