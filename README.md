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
