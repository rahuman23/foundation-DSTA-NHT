

# Getting Started

Welcome to DSO Foundation Training Labs.

!!!info
       Estimated time to complete the labs is as follows:

       - **DIY Foundation** - 60 minutes
       - **Prism Central** - 30 minutes


## What's New

- Workshop uses for the following software versions:
  - AOS 6.8.0.5
  - Prism Central pc.2024.1.0.1

## Agenda

- DIY Foundation
- Deploying Prism Central


## Initial Setup

- Take note of the *Passwords* being used from you RX reservation details
- Log into your virtual desktops (connection info below)
- Login to Global Protect VPN if you have access

### Frame VDI

Login to: <https://console.nutanix.com/x/labs>


Please use the following username and password to login to the Frame VDI desktop.

|    | Name                 | Cluster Name | Frame Account     | Frame Account Pwd |
|----|----------------------|--------------|-------------------|-------------------|
| 1  | Giam Xiong Yao       | PHX-POC263   | PHX-POC263-User01 | ntnx/4DSTA        |
| 2  | Goh Hao Wei          | PHX-POC263   | PHX-POC263-User02 | ntnx/4DSTA        |
| 3  | Lim Xi Yang          | PHX-POC263   | PHX-POC263-User03 | ntnx/4DSTA        |
| 4  | Ong Sheng Jian       | PHX-POC263   | PHX-POC263-User04 | ntnx/4DSTA        |
| 5  | Seah Wei Hong        | PHX-POC204   | PHX-POC204-User01 | ntnx/4DSTA        |
| 6  | Tay Yi Hsuen         | PHX-POC204   | PHX-POC204-User02 | ntnx/4DSTA        |
| 7  | Tanya Elizabeth Khoo | PHX-POC204   | PHX-POC204-User03 | ntnx/4DSTA        |
| 8  | Soh Boon Yen         | PHX-POC204   | PHX-POC204-User04 | ntnx/4DSTA        |
| 9  | Lim Jun Wei          | PHX-POC002   | PHX-POC002-User01 | ntnx/4DSTA        |
| 10 | Kenneth Neoh Kim How | PHX-POC002   | PHX-POC002-User02 | ntnx/4DSTA        |
| 11 | Yee Jun Wei          | PHX-POC002   | PHX-POC002-User03 | ntnx/4DSTA        |
| 12 | Yang Kai Ze          | PHX-POC002   | PHX-POC002-User04 | ntnx/4DSTA        |
| 13 | Lim Ka Tiong         | PHX-POC007   | PHX-POC007-User01 | ntnx/4DSTA        |
| 14 | Wong Wei En, Matthew | PHX-POC007   | PHX-POC007-User02 | ntnx/4DSTA        |
| 15 | Wong Chin Hao        | PHX-POC007   | PHX-POC007-User03 | ntnx/4DSTA        |
| 16 |                      | PHX-POC007   | PHX-POC007-User04 | ntnx/4DSTA        |
| 17 |                      | PHX-POC062   | PHX-POC062-User01 | ntnx/4DSTA        |
| 18 |                      | PHX-POC062   | PHX-POC062-User02 | ntnx/4DSTA        |
| 19 |                      | PHX-POC062   | PHX-POC062-User03 | ntnx/4DSTA        |
| 20 |                      | PHX-POC062   | PHX-POC062-User04 | ntnx/4DSTA        |


## Environment Details

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images,networks, and VMs required to complete the exercises.

### Networking

As we are able to provide single node clusters in the HPOC environment, we need to describe each sort of cluster separately. The clusters are setup and configured differently.

#### Three/Four node HPOC clusters

####Single node Hosted POC clusters follow a standard naming convention:

####- **Cluster Name** - POC*XYZ*
####- **Subnet** - 10.**42**.*XYZ*.0
####- **Cluster IP** - 10.**42**.*XYZ*.*XYZ*

####For example:

####- **Cluster Name** - POC055*Node Character*
####- **Subnet** - 10.42.55.0
####
Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:
####| IP Address     |   Description |
####| 10.42.*XYZ*.*XX* |  Nutanix Cluster Virtual IP   |
####| 10.42.*XYZ*.*XX*  |  **DC** VM IP, NTNXLAB.local Domain Controller   |


####Each cluster is configured with 2 VLANs which can be used for VMs:


####|Network Name     | Address             | VLAN    | DHCP Scope|
####|-----------------| ------------------- |-------- | -----------|
####|Primary          | 10.42.*XYZ*.1/25    | 0       | 10.42.*XYZ*.50-10.42.*XYZ*.124|
####|Secondary        | 10.42.*XYZ*.129/25  | *XYZ1*  | 10.42.*XYZ*.132-10.42.*XYZ*.253|


#### 1 Node Cluster HPOC

For some workshops we are using Single Node Clusters (SNC). The reason for this is to allow more people to have a dedicated cluster but still have enough free clusters for the bigger workshops including those for
customers.

The network in the SNC config is using a /26 network. This splits the network address into four equal sizes that can be used for workshops. The below table describes the setup of the network in the four
partitions. It provides essential information for the workshop with respect to the IP addresses and the services running at that IP address.

|    | Name                 | Cluster Name | IPMI IP      | HOST IP      | CVM IP       | Frame Account     | Frame Account | Frame Account Pwd | Foundation VM | Foundation VM IP | Cluster Name | Cluster Password | Primary Network Name | Primary VLAN  | Primary GW  | Secondary Subnet | Secondary IP Range | Secondary VLAN | Secondary GW  | IPMI Username | IPMI Password | DNS          | NTP            | Prism Cental IP | Cluster IP   | DSIP         |
|----|----------------------|--------------|--------------|--------------|--------------|-------------------|---------------|-------------------|---------------|------------------|--------------|------------------|----------------------|---------------|-------------|------------------|--------------------|----------------|---------------|---------------|---------------|--------------|----------------|-----------------|--------------|--------------|
| 1  | Giam Xiong Yao       | PHX-POC263   | 10.38.35.34  | 10.38.35.25  | 10.38.35.29  | PHX-POC263-User01 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_001      | 10.42.36.78      | PHX-POC263-A | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.35.45     | 10.38.35.50  | 10.38.35.55  |
| 2  | Goh Hao Wei          | PHX-POC263   | 10.38.35.35  | 10.38.35.26  | 10.38.35.30  | PHX-POC263-User02 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_002      | 10.42.36.77      | PHX-POC263-B | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.35.46     | 10.38.35.51  | 10.38.35.56  |
| 3  | Lim Xi Yang          | PHX-POC263   | 10.38.35.36  | 10.38.35.27  | 10.38.35.31  | PHX-POC263-User03 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_003      | 10.42.36.76      | PHX-POC263-C | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.35.47     | 10.38.35.52  | 10.38.35.57  |
| 4  | Ong Sheng Jian       | PHX-POC263   | 10.38.35.37  | 10.38.35.28  | 10.38.35.32  | PHX-POC263-User04 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_004      | 10.42.36.71      | PHX-POC263-D | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.35.48     | 10.38.35.53  | 10.38.35.58  |
| 5  | Seah Wei Hong        | PHX-POC204   | 10.38.204.33 | 10.38.204.25 | 10.38.204.29 | PHX-POC204-User01 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_005      | 10.42.36.75      | PHX-POC204-A | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.204.45    | 10.38.204.50 | 10.38.204.55 |
| 6  | Tay Yi Hsuen         | PHX-POC204   | 10.38.204.34 | 10.38.204.26 | 10.38.204.30 | PHX-POC204-User02 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_006      | 10.42.36.72      | PHX-POC204-B | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.204.46    | 10.38.204.51 | 10.38.204.56 |
| 7  | Tanya Elizabeth Khoo | PHX-POC204   | 10.38.204.35 | 10.38.204.27 | 10.38.204.31 | PHX-POC204-User03 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_007      | 10.42.36.74      | PHX-POC204-C | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.204.47    | 10.38.204.52 | 10.38.204.57 |
| 8  | Soh Boon Yen         | PHX-POC204   | 10.38.204.36 | 10.38.204.28 | 10.38.204.32 | PHX-POC204-User04 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_008      | 10.42.36.56      | PHX-POC204-D | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.38.204.48    | 10.38.204.53 | 10.38.204.58 |
| 9  | Lim Jun Wei          | PHX-POC002   | 10.42.2.33   | 10.42.2.25   | 10.42.2.29   | PHX-POC002-User01 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_009      | 10.42.36.59      | PHX-POC002-A | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.2.45      | 10.42.2.50   | 10.42.2.55   |
| 10 | Kenneth Neoh Kim How | PHX-POC002   | 10.42.2.34   | 10.42.2.26   | 10.42.2.30   | PHX-POC002-User02 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_010      | 10.42.36.61      | PHX-POC002-B | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.2.46      | 10.42.2.51   | 10.42.2.56   |
| 11 | Yee Jun Wei          | PHX-POC002   | 10.42.2.35   | 10.42.2.27   | 10.42.2.31   | PHX-POC002-User03 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_011      | 10.42.36.54      | PHX-POC002-C | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.2.47      | 10.42.2.52   | 10.42.2.57   |
| 12 | Yang Kai Ze          | PHX-POC002   | 10.42.2.36   | 10.42.2.28   | 10.42.2.32   | PHX-POC002-User04 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_012      | 10.42.36.64      | PHX-POC002-D | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.2.48      | 10.42.2.53   | 10.42.2.58   |
| 13 | Lim Ka Tiong         | PHX-POC007   | 10.42.7.33   | 10.42.7.25   | 10.42.7.29   | PHX-POC007-User01 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_013      | 10.42.36.63      | PHX-POC007-A | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.7.45      | 10.42.7.50   | 10.42.7.55   |
| 14 | Wong Wei En, Matthew | PHX-POC007   | 10.42.7.34   | 10.42.7.26   | 10.42.7.30   | PHX-POC007-User02 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_014      | 10.42.36.66      | PHX-POC007-B | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.7.46      | 10.42.7.51   | 10.42.7.56   |
| 15 | Wong Chin Hao        | PHX-POC007   | 10.42.7.35   | 10.42.7.27   | 10.42.7.31   | PHX-POC007-User03 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_015      | 10.42.36.65      | PHX-POC007-C | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.7.47      | 10.42.7.52   | 10.42.7.57   |
| 16 |                      | PHX-POC007   | 10.42.7.36   | 10.42.7.28   | 10.42.7.32   | PHX-POC007-User04 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_016      | 10.42.36.67      | PHX-POC007-D | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.7.48      | 10.42.7.53   | 10.42.7.58   |
| 17 |                      | PHX-POC062   | 10.42.62.33  | 10.42.62.25  | 10.42.62.29  | PHX-POC062-User01 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_017      | 10.42.36.69      | PHX-POC062-A | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.128/25  | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.62.45     | 10.42.62.50  | 10.42.62.55  |
| 18 |                      | PHX-POC062   | 10.42.62.34  | 10.42.62.26  | 10.42.62.30  | PHX-POC062-User02 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_018      | 10.42.36.70      | PHX-POC062-B | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.0/25    | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.62.46     | 10.42.62.51  | 10.42.62.56  |
| 19 |                      | PHX-POC062   | 10.42.62.35  | 10.42.62.27  | 10.42.62.31  | PHX-POC062-User03 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_019      | 10.42.36.55      | PHX-POC062-C | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.0/25    | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.62.47     | 10.42.62.52  | 10.42.62.57  |
| 20 |                      | PHX-POC062   | 10.42.62.36  | 10.42.62.28  | 10.42.62.32  | PHX-POC062-User04 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_020      | 10.42.36.68      | PHX-POC062-D | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.0/25    | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG | 10.42.62.48     | 10.42.62.53  | 10.42.62.58  |


### Credentials

!!! note

    The *Cluster Password* is unique to each cluster and will be provided by the leader of the Workshop.

| Credential        | Username                 | Password           |
|------------------ |------------------------- |--------------------|
| Prism Element     | admin                    | ntnx/4DSTA          |
| Prism Central     | admin                    | ntnx/4DSTA          |
| Controller VM     | nutanix                  | ntnx/4DSTA          |
| Prism Central VM  | nutanix                  | ntnx/4DSTA          |

Each cluster has a dedicated domain controller VM, **DC**, responsible for providing AD services for the **NTNXLAB.local** domain. The domain is populated with the following Users and Groups:


| Group            | Username(s)              | Password |
|-----------------| ------------------------- |------------|
| Administrators    | Administrator             | nutanix/4u |
| SSP Admins        | adminuser01-adminuser25   | nutanix/4u |
| SSP Developers    | devuser01-devuser25       | nutanix/4u |
| SSP Consumers     | consumer01-consumer25     | nutanix/4u |
| SSP Operators     | operator01-operator25     | nutanix/4u |
| SSP Custom        | custom01-custom25         | nutanix/4u |
| Bootcamp Users    | user01-user25             | nutanix/4u |


## Access Instructions

The Nutanix Hosted POC environment can be accessed a number of different ways:

### Lab Access User Credentials

PHX Based Clusters:

- **Username:** PHX-POCxxx-User01 (up to PHX-POCxxx-User20),
- **Password:** *Provided by Instructor*

RTP Based Clusters:

- **Username:** RTP-POCxxx-User01 (up to RTP-POCxxx-User20),
- **Password:** *Provided by Instructor*


## Nutanix Version Info

- AOS 6.8.0.5
- Prism Central pc.2024.1.0.1

## Access to lab info

!!! note

    - ```https://nutanixinc-my.sharepoint.com/:x:/g/personal/rahuman_pichai_nutanix_com/EQnLHJ7E_VVCuUsD5kNYabABn1uE0fURhlKYwD2_9pgZ8g?e=AMk948
