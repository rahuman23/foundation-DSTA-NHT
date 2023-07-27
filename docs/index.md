

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
| Yip Mun Kit           | PHX-SPOC015-4-User06 | ntnx/4DSO         |
| Ong Wu Loong Eric     | PHX-SPOC015-4-User07 | ntnx/4DSO         |
| Enkizen Wen Ming      | PHX-SPOC015-4-User08 | ntnx/4DSO         |
| Yap Kian Wee Clarence | PHX-SPOC015-4-User09 | ntnx/4DSO         |
|                       | PHX-SPOC015-4-User10 | ntnx/4DSO         |
| Lim Lui Siang Alex    | PHX-SPOC015-4-User11 | ntnx/4DSO         |
|                       | PHX-SPOC015-4-User12 | ntnx/4DSO         |
| Tan Rong Tai Damien   | PHX-SPOC015-4-User13 | ntnx/4DSO         |
|                       | PHX-SPOC015-4-User14 | ntnx/4DSO         |
| Chong Loo Tong Andrew | PHX-SPOC015-4-User15 | ntnx/4DSO         |
|                       | PHX-SPOC015-4-User16 | ntnx/4DSO         |
| Hu Huini Joey         | PHX-SPOC015-4-User17 | ntnx/4DSO         |
|                       | PHX-SPOC015-4-User18 | ntnx/4DSO         |
| Wong Teck Yuan Simon  | PHX-SPOC015-4-User19 | ntnx/4DSO         |
|                       | PHX-SPOC015-4-User20 | ntnx/4DSO         |


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


#### 3 Node Cluster HPOC

For some workshops we are using Single Node Clusters (SNC). The reason for this is to allow more people to have a dedicated cluster but still have enough free clusters for the bigger workshops including those for
customers.

The network in the SNC config is using a /26 network. This splits the network address into four equal sizes that can be used for workshops. The below table describes the setup of the network in the four
partitions. It provides essential information for the workshop with respect to the IP addresses and the services running at that IP address.

| Name                  | Foundation VM | Foundation VM IP | Cluster Name | Cluster IP   | Cluster Username | Cluster Password | Primary Netwok | Primary VLAN | Primary GW  | Secondary Subnet | Secondary IP Range | Secondary VLAN | Secondary GW  | IPMI Username | IPMI Password | DNS          | NTP            |
| --------------------- | ------------- | ---------------- | ------------ | ------------ | ---------------- | ---------------- | -------------- | ------------ | ----------- | ---------------- | ------------------ | -------------- | ------------- | ------------- | ------------- | ------------ | -------------- |
| Pern Ren              | FOVM_001      | 10.38.15.211     | PHX-POC102   | 10.42.102.37 | admin            | ntnx/4DSO        | 10.42.102.0/25 | 0            | 10.42.102.1 | 10.42.102.128/25 | 10.42.102.132-254  | 1021           | 10.42.102.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
| Whai Chun Kit         |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Koh Yong Jun Rick     | FOVM_002      | 10.38.15.212     | PHX-POC183   | 10.38.183.37 | admin            | ntnx/4DSO        | 10.38.183.0/25 | 0            | 10.38.183.1 | 10.38.183.128/25 | 10.38.183.132-254  | 1833           | 10.38.183.129 | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
| Pang Yoke Shim Jerome |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Tay Yi Hang           | FOVM_003      | 10.38.15.213     | PHX-POC295   | 10.38.67.37  | admin            | ntnx/4DSO        | 10.38.67.0/25  | 0            | 10.38.67.1  | 10.38.67.128/25  | 10.38.67.132-254   | 207            | 10.38.67.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
| Yip Mun Kit           |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Ong Wu Loong Eric     | FOVM_004      | 10.38.15.214     | PHX-POC030   | 10.42.30.37  | admin            | ntnx/4DSO        | 10.42.30.0/25  | 0            | 10.42.30.1  | 10.42.30.128/25  | 10.42.30.132-254   | 301            | 10.42.30.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
| Enkizen Wen Ming      |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Yap Kian Wee Clarence | FOVM_005      | 10.38.15.215     | PHX-POC031   | 10.42.31.37  | admin            | ntnx/4DSO        | 10.42.31.0/25  | 0            | 10.42.31.1  | 10.42.31.128/25  | 10.42.31.132-254   | 311            | 10.42.31.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
|                       |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Lim Lui Siang Alex    | FOVM_006      | 10.38.15.216     | PHX-POC061   | 10.42.61.37  | admin            | ntnx/4DSO        | 10.42.61.0/25  | 0            | 10.42.61.1  | 10.42.61.128/25  | 10.42.61.132-254   | 611            | 10.42.61.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
|                       |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Tan Rong Tai Damien   | FOVM_007      | 10.38.15.217     | PHX-POC065   | 10.42.65.37  | admin            | ntnx/4DSO        | 10.42.65.0/25  | 0            | 10.42.65.1  | 10.42.65.128/25  | 10.42.65.132-254   | 651            | 10.42.65.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
|                       |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Chong Loo Tong Andrew | FOVM_008      | 10.38.15.218     | PHX-POC018   | 10.42.18.37  | admin            | ntnx/4DSO        | 10.42.18.0/25  | 0            | 10.42.18.1  | 10.42.18.128/25  | 10.42.18.132-254   | 181            | 10.42.18.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
|                       |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Hu Huini Joey         | FOVM_009      | 10.38.15.219     | PHX-POC020   | 10.42.20.37  | admin            | ntnx/4DSO        | 10.42.20.0/25  | 0            | 10.42.20.1  | 10.42.20.128/25  | 10.42.20.132-254   | 201            | 10.42.20.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
|                       |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |
| Wong Teck Yuan Simon  | FOVM_010      | 10.38.15.220     | PHX-POC029   | 10.42.29.37  | admin            | ntnx/4DSO        | 10.42.29.0/25  | 0            | 10.42.29.1  | 10.42.29.128/25  | 10.42.29.132-254   | 291            | 10.42.29.129  | ADMIN         | ADMIN         | 10.42.194.10 | 0.pool.ntp.org |
|                       |               |                  |              |              |                  |                  |                |              |             |                  |                    |                |               |               |               |              |                |

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

- https://nutanixinc-my.sharepoint.com/:x:/g/personal/rahuman_pichai_nutanix_com/EaNgeE7S6H9Gj7BAoVzvuVEB5NnA5oT2tC_-WM2yn1L1TA?e=NJEROt

