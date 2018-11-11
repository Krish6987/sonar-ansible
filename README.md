# Sonar server + Java project setup

## Requirements

- Sonar CE 7.x
- Postgresql 9.6
- Open JDK 8

# Setup Ansible

Configure `/etc/ansible/hosts` to be used by ansible:

```yml
[sonar]
#ec2-52-207-217-64.compute-1.amazonaws.com
ec2-52-2-93-142.compute-1.amazonaws.com

[sonar:vars]
ansible_ssh_private_key_file=~/AWS/my-instance.pem
```

## Run on localhost
```sh
ansible-galaxy install -r requirements.yml
```
Go to project dir:
```sh
cd project_root_dir
```

Run ansible on sonar instance:
```sh
ansible-playbook playbook.yml -u ubuntu
```

> tip: run `htop` on sonar instance during provisioning

## Run on sonar host

- sudo apt-get update
- sudo apt install python

# Sonar console user:

user: admin
pass: admin

# https://docs.sonarqube.org/7.4/analysis/analysis-parameters/

# Steps to analize a project
- Create a project
- Get token
- Set maven plugin

ex:
java-project: 7de9efcb0af6923f86a55a17ceae1d8efa23114e

mvn sonar:sonar \
  -Dsonar.host.url=http://52.207.217.64:9000 \
  -Dsonar.login=7de9efcb0af6923f86a55a17ceae1d8efa23114e

### References
https://medium.com/@mattpwest/setting-up-sonarqube-with-ansible-fcabadee6953
https://docs.sonarqube.org/7.4/analysis/analysis-parameters/
https://github.com/eugenp/tutorials/tree/master/cas/cas-secured-app