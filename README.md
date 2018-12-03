## Description
This is an example of deploying F5s Declarative Onboarding (DO) and Application Services 3 (AS3) Extensions via Ansible to provision a BIG-IP in a declarative manner.


#### Output
High level playbook flow:

* Install Declarative Onboarding 
* Install App Services 3
* POST to DO (onboard BIG-IP)
* POST to AS3 (LTM Config)
* POST to AS3 (GSLB Config)


#### File Structure

```shell
├── ansible.cfg                                              # Settings for Ansible
├── declarative_demo.yaml                                    # Playbook
├── files                                                    # Extensions to be installed
│   ├── f5-appsvcs-<version>.noarch.rpm
│   └── f5-declarative-onboarding-<version>.noarch.rpm
├── host_vars                                                # Folder representing each device
│   └── bigip
│       ├── apps.json                                        # AS3 LTM Payload
│       ├── do.json                                          # DO Payload
│       ├── gslb.json                                        # AS3 GSLB Payload
│       ├── vars.yaml                                        # Connection Params for "bigip"
│       └── vault.yaml                                       # Password (should use vault to encrypt)
└── hosts
```

#### Setup

The ansible playbook has a hosts file with a single endpoint, **bigip**. It assumes that the device is already bootstrapped and reachable via its mgmt IP.

* Update **vars.yaml** & **vault.yaml** under the **bigip** folder to reflect your environments connection details.
* Update the **hosts** file with the name of the device.
* Update **do.json** with desired Onboard settings.
* Update **apps.json**  and **gslb.json** with desired App configs.
* Download and place the desired RPM version of both DO and AS3 in the **files** folder (the playbook will pull the file name based on naming standards).


## Run the Playbook


Run the following command from the root directory where **App1.yaml** is your edited variable file.
```shell
ansible-playbook declarative_demo.yaml
```
