# Vagrant Example of Enrollment

## Creation Your Own SSH Key

```bash
$ ssh-keygen -f provisioning/.ssh/id_ed25519 -t ed25519 -N "" -C "vagrant@domain.local"
```

## What to do...

### Setup

```bash
$ vagrant up
```

### Setup touchdown

```bash
$ vagrant ssh touchdown
```

### Configure

```bash
$ vagrant ssh touchdown
vagrant@touchdown:~$ sudo apt install sshpass
vagrant@touchdown:~$ cd /vagrant/setup/
vagrant@touchdown:/vagrant/setup$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts-p0-dc0 -i hosts-p0-dc1 playbook_0_setup.yaml
```

### Enrollment

```bash
vagrant@touchdown:/vagrant/setup$ su - ruser
ruser@touchdown:~$ cd /vagrant/setup/
ruser@touchdown:/vagrant/setup/$ ansible-galaxy collection install ansible.posix
ruser@touchdown:/vagrant/setup/$ ssh-keygen
ruser@touchdown:/vagrant/setup/$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts-p0-dc0 -i hosts-p0-dc1 playbook_1_enrol_0_known_hosts.yaml --ask-pass
ruser@touchdown:/vagrant/setup/$ ansible-playbook -i hosts-p0-dc0 -i hosts-p0-dc1 playbook_1_enrol_1_authorized_key.yaml --ask-pass
```

### Checking

```bash
vagrant@touchdown:/vagrant/setup$ su - ruser
ruser@touchdown:~$ cd /vagrant/setup/
ruser@touchdown:/vagrant/setup/$ ansible-playbook -i hosts-p0-dc0 -i hosts-p0-dc1 playbook_2_check.yaml
```
