# Configure Suricata Biult in AWS to send logs to Wazuh Dashboard

## Recommended:
```
Ubuntu 22.04
```
## First Install Suricata on the Sensor
 [Installation-Suricata](Installation.md)

 ## Then Install Wazuh 
  [Wazuh-Installtion-Giude](Wazuh/Installation-guide-onAWS.md)

 ## Configure Wazuh To Read Suricata Log
```
/var/ossec/etc/ossec.conf
```
Add:

```bash
<localfile>
<log_format>json</log_format>
<location>/var/log/suricata/eve.json</location>
</localfile>
```

Restart the agent:

```
sudo systemctl restart wazuh-agent
```

⚠️Note: 
 > Even after configuration the suricata sensor may not read the correct logs of it's Machine and might not see other Machines traffic so traffic mirroring is needed and should be configured as it's hosted on AWS, so to Trobleshoot this I created a guide to do this in [Network-Diagram](../Architecture/network-design.md)
