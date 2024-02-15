Firewalld is the standard firewall service in the fedora linux enviroment.
> [!attention]
> all commands are executed as root

## Check availability
```bash
systemctl status firewalld
```

```bash
firewall-cmd --state
```

## List relevant information about the default zone
```bash
firewall-cmd --list-all
```

## Start/Stop the service
```bash
systemctl unmask firewalld
systemctl start firewalld
```

```bash
systemctl stop firewalld
systemctl mask firewalld
```

### Enable firewalld at os startup
```bash
systemctl enable firewalld
```

### Disable firewalld at os startup
```bash
systemctl disable firewalld
```

## List ports

- List of allowed ports in the current zone
> ```bash
> firewall-cmd --list-ports
- List of allowed services in the current zone
>```bash
>firewall-cmd --list-services


## Open a port/service in firewalld 

```bash
firewall-cmd --permanent --add-port=80/tcp
```

```bash
firewall-cmd --permanent --add-service=http
```

## Close a port/service in firewalld
```bash
firewall-cmd --remove-port=port-number/port-type
```

## Reload firewall
```bash
firewall-cmd --reload
```
**or**
```bash
firewall-cmd --runtime-to-permanent
```

## Firewall zones 
