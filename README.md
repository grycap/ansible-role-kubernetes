
Kubernetes Role
=======================

This ansible role installs a [Kubernetes](https://kubernetes.io/) cluster.

Role Variables
----------------

The variables that can be passed to this role and a brief description about them are as follows.

	# Type of node front or wn
	kube_type_of_node: front
	# IP address or name of the Kube front node
	kube_server: "{{ ansible_default_ipv4.address }}"
	# Security Token
	kube_token: some01.rand0mt0k3n16342
	# POD network cidr (only used in kube-router network)
	kube_pod_network_cidr: 10.244.0.0/16
	# Type of network to install: currently supported: flannel, kube-router, romana, calico
	kube_network: flannel
	# Kubelet extra args
	kubelet_extra_args: ''


Example Playbook
----------------

This an example of how to install this role in the front-end node:

    - hosts: server
      roles:
      - { role: 'grycap.kubernetes', kube_token: 'some01.rand0mt0k3n16344' }

And in the WNs:

    - hosts: wn
      roles:
      - { role: 'grycap.kubernetes', kube_type_of_node: 'wn', kube_server: '10.0.0.1', kube_token: 'some01.rand0mt0k3n16344' }

Contributing to the role
========================
In order to keep the code clean, pushing changes to the master branch has been disabled.
If you want to contribute, you have to create a branch, upload your changes and then create a pull request.
Thanks
