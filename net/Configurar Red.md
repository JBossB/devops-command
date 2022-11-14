# Configurar Red Ubuntu 20

### Editar el archivo 
sudo nano /etc/netplan/01-network-manager-all.yaml
```
network:
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      dhcp4: true
  version: 2
```

ejecutar:
```
sudo netplan apply
```

```
sudo systemctl start systemd-resolved
sudo systemctl enable systemd-resolved
```