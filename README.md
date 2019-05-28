# ansible-beats-linux

**AntSec Collector Pack**

**THIS ROLE IS FOR 7.x**

**If you encounter unexpected behaviour, please contact us**
This is the AntSec Ansible role for 7.x beats.  Currently this works on Debian based linux systems.  Tested platforms are:

* Debian 9

** Using the role **
Place the received configuration in a folder (in this example "beats-ssl"). Do Not change the names of these files
Configure the default settings in your playbook:

```
- role: beats-linux
  beats_customer_id: <customer_id received from AntSec>
  enabled_collectors: 
      - "filebeat"
      - "packetbeat"
      - "metricbeat"
    mb_version_lock: true 
    mb_upgrade: false
    mb_major_version: "7.x"
    mb_version: "7.0.1"
    mb_modules:
      - "system"
    fb_version_lock: true
    fb_upgrade: false
    fb_major_version: "7.x"
    fb_version: "7.0.1"
    fb_system:
      enable_syslog: true
      enable_auth: true
    pb_version_lock: true
    pb_upgrade: false
    pb_major_version: "7.x"
    pb_version: "7.0.1"
    output:
      type: logstash
      hosts:
        - "<host>:<port>"
    ssl_config:
      directory: "/etc/ssl/as-collectors"
      verification_mode: full
      supported_protocols: TLSv1.2
      cert: "beats-ssl/{{ beats_customer_id }}.crt"
      key: "beats-ssl/{{ beats_customer_id }}.key"
      cacerts: "beats-ssl/antsec.cacerts"
    tags: 
      - deploy_collectors
```

If you require a specific configuration, please contact us.