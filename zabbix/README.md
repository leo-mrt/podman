# zabbix-podman
A Zabbix server (with pgsql and alpine tag) with web interface (nginx) in podman, with quadlet implementation (Kubernetes ready).


## Getting started
This deployment uses docker hub published offical containers for Zabbix.  

Edit `zabbix-server-cm.yml` and `zabbix-server-pod.yml` to your liking (changing things like passwords, usernames, pod names accordingly) and then either run directly with

`podman kube play zabbix-secrets.yml`
`podman play kube --configmap=pgsql-cm.yml pgsql-pod.yml`
`podman play kube --configmap=zabbix-server-cm.yml zabbix-server-pod.yml`
`podman play kube --configmap=zabbix-web-cm.yml zabbix-web-pod.yml`

OR use Quadlet. 
Copy the pod and configmap definitions to /etc/containers/systemd or user systemd directory (systemctl --user). 
Copy the `quadlet/zabbix-server-pod.kube` file to /etc/containers/systemd. 
Then run `systemctl daemon-reload` and you should now have a service called `zabbix-server-pod.service` that you can start. 