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
