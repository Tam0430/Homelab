# Home lab
This repo contains all of the configuration and documentation of my homelab
I began working on this Feb 1 2025
## Tooling 
* K3s

## Goals
* Run Promethues and Grafana stack
* Have Grafana dashboard available with a URL
	* ingress
	* tls
	* DNS
* Everything should be deployed using Gitops
	* Try out Flux
# Installation
Decided to use k3s for installing Kubernetes. Used kubeadm before, but but prefer a less complicated approach for now. Even though kubeadm is a great way to learn, and I managed without problems, For long-term maintenance it is better to use k3s or microk8s. It also takes away cert comlexity for now. Might use kubeadm later

## Installation k3s

Just used the docs.
https://docs.k3s.io/quick-start

Struggled a bit with the error "error: error loading config file "/etc/rancher/k3s/k3s.yaml": open /etc/rancher/k3s/k3s.yaml: permission denied"

Solved with this-
mkdir ~/.kube/config
chmod 600 ~/.kube/config
sudo k3s kubectl config view --raw | tee ~/.kube/config
export KUBECONFIG=~/.kube/config

Problem was a faulty kubeconfig configurattion
Also had to disable ufw

## Setup the control plane cluste in you primary 
Copy the `~/.kube/config` on your remote machine to you primary machine same path `~/.kube/config
then replace the value of the `server: https:<ip>:6443` to your remote machine Ip, now you can manage your remote machine cluster to your primary machine 
note: Installt the kubectl on your primary machine using the below Installation link
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

