
Kubernetes Role
=======================

This ansible role installs a [Kubernetes](https://kubernetes.io/) cluster.

Role Variables
----------------

The variables that can be passed to this role and a brief description about them are as follows.

    # Version to install or latest
    kube_version: 1.11.4
	# Type of node front or wn
	kube_type_of_node: front
	# IP address or name of the Kube front node
	kube_server: "{{ ansible_default_ipv4.address }}"
	# Security Token
	kube_token: "kube01.{{ lookup('password', '/tmp/tokenpass chars=ascii_lowercase,digits length=16') }}"
	# Token TTL duration (0 do not expire)
	kube_token_ttl: 0
	# POD network cidr
	kube_pod_network_cidr: 10.244.0.0/16
	# Type of network to install: currently supported: flannel, kube-router, romana, calico, weave
	kube_network: flannel
	# Kubelet extra args
	kubelet_extra_args: ''
	# Kube API server options
	kube_apiserver_options: []
	# Flag to set HELM to be installed
	kube_install_helm: true
	# Helm version
	kube_install_helm_version: "v2.11.0"
	# Deploy the Dashboard
	kube_deploy_dashboard: false
	# value to pass to the kubeadm init --apiserver-advertise-address option
	kube_api_server: 0.0.0.0
	# A set of git repos and paths to be applied in the cluster. Following this format:
	# kube_apply_repos: [{repo: "https://github.com/kubernetes-incubator/metrics-server", version: "master", path: "deploy/1.8+/"}]
	kube_apply_repos: []
	# Flag to set Metrics-Server to be installed
	kube_install_metrics: false
	# Flag to set the nginx ingress controller to be installed
	kube_install_ingress: false
	# Flag to set the kubeapps UI to be installed
	kube_install_kubeapps: false

Example Playbook
----------------

This an example of how to install this role in the front-end node:

    - hosts: server
      roles:
      - { role: 'grycap.kubernetes', kube_apiserver_options: [{option: "--insecure-port", value: "8080"}] }

And in the WNs:

    - hosts: wn
      roles:
      - { role: 'grycap.kubernetes', kube_type_of_node: 'wn', kube_server: '10.0.0.1' }

Contributing to the role
========================
In order to keep the code clean, pushing changes to the master branch has been disabled.
If you want to contribute, you have to create a branch, upload your changes and then create a pull request.
Thanks
