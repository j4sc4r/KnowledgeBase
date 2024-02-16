# Firewalld
Firewalld is the standard firewall service in the fedora linux enviroment.
> [!attention] All commands are executed as root

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
firewall-cmd --remove-port=80/tcp
```

## Reload firewall
```bash
firewall-cmd --reload
```

## Make temporary changes permanent 
```bash
firewall-cmd --runtime-to-permanent
```

## Firewall zones 

Zones categorize network interfaces and apply predefined security policies to regulate incoming and outgoing traffic, facilitating network segmentation and tailored security configurations.

### Preconfigured zones 

| Zone        | Explaination        |
| ----------- | ------------------- |
| Internal Zone |  for trustworthy internal networks |
| DMZ zone | for demilitarised zones with restricted access to internal resources.|
| Public Zone | for public networks |

### Create custom zones 

```bash
firewall-cmd --permanent --zone=<name> --add-rule=<rules>
```

### List zones

```bash
firewall-cmd --list-all-zones
```

For only show a specific zone configuration

```bash
firewall-cmd --zone=<name> --list-all
```
