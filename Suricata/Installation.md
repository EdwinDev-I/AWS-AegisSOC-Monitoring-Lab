# Suricata setup

## Step1: Install ufw(Uncomplicated Firewall) To Work With Suricata
```
 sudo apt-get update
```
then
```
sudo apt install ufw
```
## Step2: enable it
```
sudo ufw enable
```
## Step3: Default security rules:
```
sudo ufw default deny incoming
sudo ufw default allow outging
```

## Step4: Allow required service
 ```bash
  sudo ufw allow 22/tcp

   sudo ufw allow 80/tcp

   sudo ufw allow 443/tcp
```
## you can allow more this is just an allowed sample

## Step5: Check status
```
   sudo ufw status verbose
```
## Step6: Install Suricata & start the service
```
   sudo apt install suricata
   sudo systemctl start suricata 
   sudo systemctl status suricata
```

## Step7: if needed check logs
```
   sudo tail -f /var/log/suricata/fast.log
```


# Troubleshooting quide if necessary
## When Suricata not active

## Step1: Check the exact error
```
   sudo journalctl -u suricata -xe
```

##or 
```
   sudo suricata -T -c /etc/suricata/suricata.yaml -v
```

## Step2: Check eth0 by checking your ipaddress to see if it matches
```
   ip a 

##or 

   ifconfig
```

## Step3: Open the Suricata config most common problem wrong network interface 
```
   sudo nano /etc/suricata/suricata.yaml
```

### then find section:

```bash
   af-packect:
     - interface: eth0
```

## Step4: Rstart Suricata
```
   sudo sysytemctl restart suricata
```

## Step5: Check status again
```
   sudo systemctl status suricata
```

### it should be (running) now  😁

## Image Example:

![Fast-log](./Suricata/Image/Fastlog-capture.png)
