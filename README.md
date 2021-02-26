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
