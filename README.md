
Kubernetes Role
=======================

This ansible role installs a [Kubernetes](https://kubernetes.io/) cluster.

This work is co-funded by the [EOSC-hub project](http://eosc-hub.eu/) (Horizon 2020) under Grant number 777536.
<img src="https://wiki.eosc-hub.eu/download/attachments/1867786/eu%20logo.jpeg?version=1&modificationDate=1459256840098&api=v2" height="24">
<img src="https://wiki.eosc-hub.eu/download/attachments/18973612/eosc-hub-web.png?version=1&modificationDate=1516099993132&api=v2" height="24">

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
	# Type of network to install: currently supported: flannel, kube-router, calico, weave
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
	# KubeApps chart version to install (or latest)
	kube_kubeapps_chart_version: "7.3.2"
	# Extra options for the flannel plugin
	kube_flanneld_extra_args: [] 
	# Enable to install and manage Certificates with Cert-manager
	kube_cert_manager: false
	# Public IP to use by the cert-manager (not needed if kube_public_dns_name is set)
	kube_cert_public_ip: "{{ ansible_default_ipv4.address }}"
	# Public DNS name to use in the dashboard tls certificate
	kube_public_dns_name: ""
	# Email to be used in the Let's Encrypt issuer
	kube_cert_user_email: jhondoe@server.com
	# Options to add in the docker.json file
	kube_docker_options: {}
	# Compatible docker versions
	kube_docker_compatible_versions: ['17.03.', '18.06.', '18.09.', '19.03.']
	# Install docker with pip
	kube_install_docker_pip
	# Command flags to use for launching k3s in the systemd service
	kube_k3_exec: ""
	# How to install K8s: kubeadm or k3s
	kube_install_method: kubeadm
	# Servers to install and configure ntp. If [] ntp will not be configured
	kube_ntp_servers: [ntp.upv.es, ntp.uv.es]

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
