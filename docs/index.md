

# Getting Started

Welcome to DSO Foundation Training Labs.

!!!info
       Estimated time to complete the labs is as follows:

       - **DIY Foundation** - 60 minutes
       - **Prism Central** - 30 minutes
       - **XRAY** - 60 minutes

## What's New

- Workshop uses for the following software versions:
  - AOS 5.20.3
  - Prism Central pc.2022.4.x

## Agenda

- DIY Foundation
- Deploying Prism Central
- XRAY

## Initial Setup

- Take note of the *Passwords* being used from you RX reservation details
- Log into your virtual desktops (connection info below)
- Login to Global Protect VPN if you have access

### Frame VDI

Login to: <https://console.nutanix.com/x/labs>


Please use the following username and password to login to the Frame VDI desktop.

| Name                  | Frame Account        | Frame Account Pwd |
| --------------------- | -------------------- | ----------------- |
| Pern Ren              | PHX-SPOC015-4-User01 | ntnx/4DSO         |
| Whai Chun Kit         | PHX-SPOC015-4-User02 | ntnx/4DSO         |
| Koh Yong Jun Rick     | PHX-SPOC015-4-User03 | ntnx/4DSO         |
| Pang Yoke Shim Jerome | PHX-SPOC015-4-User04 | ntnx/4DSO         |
| Tay Yi Hang           | PHX-SPOC015-4-User05 | ntnx/4DSO         |
| Yip Mun Kit           | PHX-POC295-User01    | ntnx/4DSO         |
| Ong Wu Loong Eric     | PHX-SPOC015-4-User07 | ntnx/4DSO         |
| Enkizen Wen Ming      | PHX-SPOC015-4-User08 | ntnx/4DSO         |
| Yap Kian Wee Clarence | PHX-SPOC015-4-User09 | ntnx/4DSO         |
|                       | PHX-POC102-User01    | ntnx/4DSO         |
| Lim Lui Siang Alex    | PHX-POC102-User02    | ntnx/4DSO         |
|                       | PHX-POC102-User07    | ntnx/4DSO         |
| Tan Rong Tai Damien   | PHX-POC295-User02    | ntnx/4DSO         |
|                       |                      | ntnx/4DSO         |
| Chong Loo Tong Andrew | PHX-POC102-User04    | ntnx/4DSO         |
|                       |                      | ntnx/4DSO         |
| Hu Huini Joey         | PHX-POC102-User05    | ntnx/4DSO         |
|                       |                      | ntnx/4DSO         |
| Wong Teck Yuan Simon  | PHX-POC102-User06    | ntnx/4DSO         |
|                       |                      | ntnx/4DSO         |


## Environment Details

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images,networks, and VMs required to complete the exercises.

### Networking

As we are able to provide three/four node clusters and single node clusters in the HPOC environment, we need to describe each sort of cluster separately. The clusters are setup and configured differently.

#### Three/Four node HPOC clusters

Three or four node Hosted POC clusters follow a standard naming convention:

- **Cluster Name** - POC*XYZ*
- **Subnet** - 10.**42**.*XYZ*.0
- **Cluster IP** - 10.**42**.*XYZ*.37

For example:

- **Cluster Name** - POC055
- **Subnet** - 10.42.55.0
- **Cluster IP** - 10.42.55.37 for the VIP of the Cluster

Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:

| IP Address     |   Description |
| -------------- | --------------- |
| 10.42.*XYZ*.37 |  Nutanix Cluster Virtual IP   |
| 10.42.*XYZ*.39 |  **PC** VM IP, Prism Central |
| 10.42.*XYZ*.41  |  **DC** VM IP, NTNXLAB.local Domain Controller   |


Each cluster is configured with 2 VLANs which can be used for VMs:


|Network Name     | Address             | VLAN    | DHCP Scope|
|-----------------| ------------------- |-------- | -----------|
|Primary          | 10.42.*XYZ*.1/25    | 0       | 10.42.*XYZ*.50-10.42.*XYZ*.124|
|Secondary        | 10.42.*XYZ*.129/25  | *XYZ1*  | 10.42.*XYZ*.132-10.42.*XYZ*.253|


#### 1 Node Cluster HPOC

For some workshops we are using Single Node Clusters (SNC). The reason for this is to allow more people to have a dedicated cluster but still have enough free clusters for the bigger workshops including those for
customers.

The network in the SNC config is using a /26 network. This splits the network address into four equal sizes that can be used for workshops. The below table describes the setup of the network in the four
partitions. It provides essential information for the workshop with respect to the IP addresses and the services running at that IP address.

|    | Name                 | Cluster Name | IPMI IP      | HOST IP      | CVM IP       | Frame Account     | Frame Account | Frame Account Pwd | Foundation VM | Foundation VM IP | Cluster Name | Cluster Password | Primary Network Name | Primary VLAN  | Primary GW  | Secondary Subnet | Secondary IP Range | Secondary VLAN | Secondary GW  | IPMI Username | IPMI Password | DNS          | NTP            |
|----|----------------------|--------------|--------------|--------------|--------------|-------------------|---------------|-------------------|---------------|------------------|--------------|------------------|----------------------|---------------|-------------|------------------|--------------------|----------------|---------------|---------------|---------------|--------------|----------------|
| 1  | Giam Xiong Yao       | PHX-POC263   | 10.38.35.34  | 10.38.35.25  | 10.38.35.29  | PHX-POC263-User01 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_001      |                  | PHX-POC263-A | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 2  | Goh Hao Wei          | PHX-POC263   | 10.38.35.35  | 10.38.35.26  | 10.38.35.30  | PHX-POC263-User02 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_002      |                  | PHX-POC263-B | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 3  | Lim Xi Yang          | PHX-POC263   | 10.38.35.36  | 10.38.35.27  | 10.38.35.31  | PHX-POC263-User03 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_003      |                  | PHX-POC263-C | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 4  | Ong Sheng Jian       | PHX-POC263   | 10.38.35.37  | 10.38.35.28  | 10.38.35.32  | PHX-POC263-User04 | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_004      |                  | PHX-POC263-D | ntnx/4DSTA       | 10.38.35.0/25        | 0             | 10.38.35.1  | 10.38.35.128/25  | 10.38.35.132-254   | 47             | 10.38.35.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 5  | Seah Wei Hong        | PHX-POC204   | 10.38.204.33 | 10.38.204.25 | 10.38.204.29 |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_005      |                  | PHX-POC204-A | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 6  | Tay Yi Hsuen         | PHX-POC204   | 10.38.204.34 | 10.38.204.26 | 10.38.204.30 |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_006      |                  | PHX-POC204-B | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 7  | Tanya Elizabeth Khoo | PHX-POC204   | 10.38.204.35 | 10.38.204.27 | 10.38.204.31 |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_007      |                  | PHX-POC204-C | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 8  | Soh Boon Yen         | PHX-POC204   | 10.38.204.36 | 10.38.204.28 | 10.38.204.32 |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_008      |                  | PHX-POC204-D | ntnx/4DSTA       | 10.38.204.0/25       | 0             | 10.38.204.1 | 10.38.204.128/25 | 10.38.204.132-254  | 2043           | 10.38.204.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 9  | Lim Jun Wei          | PHX-POC002   | 10.42.2.33   | 10.42.2.25   | 10.42.2.29   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_009      |                  | PHX-POC002-A | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 10 | Kenneth Neoh Kim How | PHX-POC002   | 10.42.2.34   | 10.42.2.26   | 10.42.2.30   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_010      |                  | PHX-POC002-B | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 11 | Yee Jun Wei          | PHX-POC002   | 10.42.2.35   | 10.42.2.27   | 10.42.2.31   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_011      |                  | PHX-POC002-C | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 12 | Yang Kai Ze          | PHX-POC002   | 10.42.2.36   | 10.42.2.28   | 10.42.2.32   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_012      |                  | PHX-POC002-D | ntnx/4DSTA       | 10.42.2.0/25         | 0             | 10.42.2.1   | 10.42.2.128/25   | 10.42.2.132-254    | 21             | 10.42.2.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 13 | Lim Ka Tiong         | PHX-POC007   | 10.42.7.33   | 10.42.7.25   | 10.42.7.29   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_013      |                  | PHX-POC007-A | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 14 | Wong Wei En, Matthew | PHX-POC007   | 10.42.7.34   | 10.42.7.26   | 10.42.7.30   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_014      |                  | PHX-POC007-B | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 15 | Wong Chin Hao        | PHX-POC007   | 10.42.7.35   | 10.42.7.27   | 10.42.7.31   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_015      |                  | PHX-POC007-C | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 16 |                      | PHX-POC007   | 10.42.7.36   | 10.42.7.28   | 10.42.7.32   |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_016      |                  | PHX-POC007-D | ntnx/4DSTA       | 10.42.7.0/25         | 0             | 10.42.7.1   | 10.42.7.128/25   | 10.42.7.132-254    | 71             | 10.42.7.129   | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 17 |                      | PHX-POC062   | 10.42.62.33  | 10.42.62.25  | 10.42.62.29  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_017      |                  | PHX-POC062-A | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.128/25  | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 18 |                      | PHX-POC062   | 10.42.62.34  | 10.42.62.26  | 10.42.62.30  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_018      |                  | PHX-POC062-B | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.0/25    | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 19 |                      | PHX-POC062   | 10.42.62.35  | 10.42.62.27  | 10.42.62.31  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_019      |                  | PHX-POC062-C | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.0/25    | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 20 |                      | PHX-POC062   | 10.42.62.36  | 10.42.62.28  | 10.42.62.32  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_020      |                  | PHX-POC062-D | ntnx/4DSTA       | 10.42.62.0/25        | 0             | 10.42.62.1  | 10.42.62.0/25    | 10.42.62.132-254   | 621            | 10.42.62.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 21 |                      | PHX-POC044   | 10.42.44.33  | 10.42.44.25  | 10.42.44.29  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_021      |                  | PHX-POC044-A | ntnx/4DSTA       | 10.42.44.0/25        | 0             | 10.42.44.1  | 10.42.44.128/25  | 10.42.44.132-254   | 441            | 10.42.44.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 22 |                      | PHX-POC044   | 10.42.44.34  | 10.42.44.26  | 10.42.44.30  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_022      |                  | PHX-POC044-B | ntnx/4DSTA       | 10.42.44.0/25        | 0             | 10.42.44.1  | 10.42.44.128/25  | 10.42.44.132-254   | 441            | 10.42.44.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 23 |                      | PHX-POC044   | 10.42.44.35  | 10.42.44.27  | 10.42.44.31  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_023      |                  | PHX-POC044-C | ntnx/4DSTA       | 10.42.44.0/25        | 0             | 10.42.44.1  | 10.42.44.128/25  | 10.42.44.132-254   | 441            | 10.42.44.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |
| 24 |                      | PHX-POC044   | 10.42.44.36  | 10.42.44.28  | 10.42.44.32  |                   | ntnx/4DSTA    | ntnx/4DSTA        | FOVM_024      |                  | PHX-POC044-D | ntnx/4DSTA       | 10.42.44.0/25        | 0             | 10.42.44.1  | 10.42.44.128/25  | 10.42.44.132-254   | 441            | 10.42.44.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.POOL.NTP.ORG |


### Credentials

!!! note

    The *Cluster Password* is unique to each cluster and will be provided by the leader of the Workshop.

| Credential        | Username                 | Password           |
|------------------ |------------------------- |--------------------|
| Prism Element     | admin                    | ntnx/4DSO          |
| Prism Central     | admin                    | ntnx/4DSO          |
| Controller VM     | nutanix                  | ntnx/4DSO          |
| Prism Central VM  | nutanix                  | ntnx/4DSO          |

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

- AOS 5.20.3
- Prism Central pc.2022.4.x

## Access to lab info

!!! note

    - ```https://nutanixinc-my.sharepoint.com/:x:/g/personal/rahuman_pichai_nutanix_com/EaNgeE7S6H9Gj7BAoVzvuVEB5NnA5oT2tC_-WM2yn1L1TA?e=NJEROt
