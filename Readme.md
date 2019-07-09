# Docker Swarm using Vagrant and Ansible

## Install Ansible on the local machine
- Install a Python 3 virtual environment
```bash
bash
$ python3 -m venv pyenv
# active your environment
$ . pyenv/bin/activate
# update PIP
$ python -m pip install --upgrade pip
# install packages
$ pip install wheel paramiko ansible 
$ pip list
Package      Version
------------ -------
ansible      2.8.2
asn1crypto   0.24.0
bcrypt       3.1.7
cffi         1.12.3
cryptography 2.7
Jinja2       2.10.1
MarkupSafe   1.1.1
paramiko     2.6.0
pip          19.1.1
pycparser    2.19
PyNaCl       1.3.0
PyYAML       5.1.1
setuptools   40.8.0
six          1.12.0
wheel        0.33.4
```
## Install Vagrant
Download setup files for your OS from https://www.vagrantup.com/

## Install Virtualbox
Download latest setup files for your OS from https://www.virtualbox.com and install Virtualbox Extension Pack

## Start your Docker Swarm machines
- Modify Vagrantfile MASTERS and WORKERS to suit your needs.
- Modify ansible/playbook.yml if you add more masters and workers.
- Start your machines:
```bash
bash
$ vagrant up
```
- Wait until vagrant finish creating your VMs.

## Verify your Swarm setup
- Connect to your Docker Swarm master
```bash
bash
$ vagrant ssh swarm-master-1
```
- List your Docker Swarm nodes:
```bash
bash
$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
um9kkzgmroaov0dkbr7ioxtyp *   swarm-master-1      Ready               Active              Leader              18.09.7
sn203dl3xmqu1w3v363tr2zea     swarm-master-2      Ready               Active              Reachable           18.09.7
pn4gdomv6u04fnkfj0xdx6glk     swarm-worker-1      Ready               Active                                  18.09.7
jociawr1nro7gftfsciamj6o2     swarm-worker-2      Ready               Active                                  18.09.7
2p2b6aw2lq98rc6m2qfd4jlv0     swarm-worker-3      Ready               Active                                  18.09.7
fb1os8cou91uj0qe0awbc0sm6     swarm-worker-4      Ready               Active                                  18.09.7

```

### Have fun with deploying services