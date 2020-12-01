# K3S Agent Ansible role

![Basic role syntax check](https://github.com/nemonik/k3s-agent-role/workflows/Basic%20role%20syntax%20check/badge.svg)

An Ansible role for ensuring the configuration of an Agent [K3s](https://k3s.io/) worker node.

## Requirements

Requires Docker installed.

The role installs on CentOS 7, Alpine 3.10 and Ubuntu Bionic.

## Role Variables

| Variable                 | Required | Default               | Choices             | Comments                                         |
|--------------------------|----------|-----------------------|---------------------|--------------------------------------------------|
| default_retries          | yes      | 60                    | Integer value       | default number of retries                        |
| default_delay            | yes      | 60                    | Integer value       | default delay in seconds between retries         |
| k3s_version              | yes      | v1.19.4+k3s1          | matches release tag | k3s version to install                           |
| k3s_server_hostname      | yes      | 192.168.0.10          | String              | The address of the server                        |
| vault_k3s_cluster_secret | yes      |                       | String              | Please, set via Ansible vault                    |
| retrieve_kubeconfig      | no.      | false                 | Boolean             | Retreive the kubeconfig file                     |
| images_cache_path        | no       | not defined           | Path                | Path to folder used to cache saved Docker images |            
| cache_container_timeout  | no       | 300 seconds           | Integer value       | Number of seconds before Ansible times out       |

## Example Playbook

An example can be found used in my Hands-on DevOps course's [ansible/master-playbook.yml](https://github.com/nemonik/hands-on-DevOps/blob/master/ansible/master-playbook.yml).

```
- hosts: masters
  remote_user: vagrant
  roles:
    - common
    - docker
    - k3s-agent
```

The above Ansible playbook uses my

- [Common role](https://github.com/nemonik/common-role) to configure the instance past the base CentOS 7, Alpine 3.10 or Ubuntu Bionic image
- [Docker role](https://github.com/nemonik/docker-role) to install and configure Docker
- [This role](https://github.com/nemonik/k3s-agent-role) to install Lightweight Kubernetes (K3s)

For more information and to see this role put into action checkout my [Hands-on DevOps class](https://github.com/nemonik/hands-on-DevOps) project.

## Setting the k3s cluster secret

The K3s cluster secret is set by `vault_k3s_cluster_secret`.  Please, ansible vault this variable.

## License

3-Clause BSD License

## Author Information

Michael Joseph Walsh <mjwalsh@nemonik.com>
