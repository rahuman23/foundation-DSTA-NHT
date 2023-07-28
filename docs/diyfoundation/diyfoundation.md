---
title: Foundation
---

# Overview

!!!info
        Estimated time to complete: **60 Minutes**

Foundation is used to automate the installation of the hypervisor and
Controller VM on one or more nodes. In this exercise you will practice
imaging a physical cluster with Foundation. In order to keep the lab
self-contained, you will create a single node cluster on which you
will deploy your Foundation VM. That Foundation instance will be used to
image and create a cluster from the remaining 3 nodes in the Block.

!!!caution
          In following steps, you should replace xx part of the IP octet with your assigned cluster ID

 
## Please find the below table for your Foundation VM IP

Please open up a browser and enter the IP address of the foundation IP address. This will bring you foundation VM page. Step 1 has been done for you to save time of uploading the image. Please proceed with Step 3! 

| Name                  | Foundation VM IP |
| --------------------- | ---------------- |
| Pern Ren              | 10.38.15.211     |
| Whai Chun Kit         |                  |
| Koh Yong Jun Rick     | 10.38.15.212     |
| Pang Yoke Shim Jerome |                  |
| Tay Yi Hang           | 10.38.15.213     |
| Yip Mun Kit           |                  |
| Ong Wu Loong Eric     | 10.38.15.214     |
| Enkizen Wen Ming      |                  |
| Yap Kian Wee Clarence | 10.38.15.215     |
|                       |                  |
| Lim Lui Siang Alex    | 10.38.15.216     |
|                       |                  |
| Tan Rong Tai Damien   | 10.38.15.217     |
|                       |                  |
| Chong Loo Tong Andrew | 10.38.15.218     |
|                       |                  |
| Hu Huini Joey         | 10.38.15.219     |
|                       |                  |
| Wong Teck Yuan Simon  | 10.38.15.220     |
|                       |                  |


## Foundation Node ABC cluster

!!!note
       We will do this section of the lab from your desktop (Windows or Mac) computer. This is the fastest way as remote consoles will be slow.

By default, Foundation does not have any AOS or hypervisor images. You can download your desired AOS package from the [Nutanix Portal](https://portal.nutanix.com/#/page/releases/nosDetails).

2.  From you desktop computer, open Google Chrome browser and navigate to Foundation VM's IP

3.  Access Foundation UI via any browser at ``http://<Foundation VM IP>``

4.  Fill the following fields:

    -   **Select your hardware platform**: Autodetect
    -   **Netmask of Every Host and CVM** - 255.255.255.128
    -   **Gateway of Every Host and CVM** - 10.42.xx.1
    -   **Gateway of Every IPMI** - 10.42.xx.1
    -   **Netmask of Every IPMI** - 255.255.255.128
    -   Under **Double-check this installer's networking step**
    -   **Skip this Validation** - selected

    ![image](images/image014.png)

5.  In new foundation page, Tools menu choose **Remove Unselected Rows** to clear all auto discovered nodes

    ![image](images/remove-nodes.png)

6.  Click **Add nodes manually**

    ![image](images/image0141.png)

7.  Fill in block information, fill in the following information:

    -   **Number of blocks** - 1
    -   **Number of nodes** - 4
    -   **How should these nodes be reached?** - choose **I will provide the IPMI's MACs**

8.  Click **Add**

    ![image](images/image104.png)

    !!!tip 
           Foundation will automatically discover any hosts in the same IPv6 Link Local broadcast domain that is not already part of a cluster. 
           
           When transferring POC assets in the field, it's not uncommon to receive a cluster that wasn't properly destroyed at the conclusion of the previous POC. In that case, the nodes are already part of existing clusters and will not be discovered. 
           
           In this lab, we choose manually specify the MAC address instead in order to practice as the real world.

    !!!info
           There are at least 2 methods to get MAC address remotely.

           Method.1: Identify IPMI MAC Address (BMC MAC address) of Nodes (A, B, and C) by accessing IPMI IP in a browser for each node 
           
           Method.2 Identify IPMI MAC Address of Nodes (A, B, C) by logging to the AHV hosts with User: root, Password: *default* for each node and using the following commands: 
           
           ``` bash
           ssh -l root <IP address of Host/Hypervisor>
           ```

           ``` bash
           ipmitool lan print | grep "MAC Address" 
           ```
           ```bash
           # output here 
           MAC Address             : 0c:c4:7a:3c:c9:ad
           # repeat for nodes B and C for unique IPMI MAC addresses
           ```

9.  Access Node A IPMI through IP 10.42.xx.33 with ADMIN/ADMIN

    ![image](images/image101.png)

    ![image](images/image102.png)

10. Record your NODE A/B/C BMC MAC address (in above example , it is **ac:1f:6b:1e:95:eb** )

    Doing the same with your other 2 nodes B/C, access Node B and C IPMI through IP 10.42.xx.34/35 with ADMIN/ADMIN, record all 3 BMC MAC addresses.

11. Click **Tools** and select **Range Autofill** from the drop down list

12. Depending on which cluster you are using, Rahuman has being a nice guy has provided you with the range of IP address to fill in for all the nodes. Look for your cluster IPMI, HOST and CVM IP and fill up on your foundation page:


    -   **IPMI IP** - 10.42 or 38.xx.33,34,35,36
    -   **Hypervisor IP** - 10.42 or 38.xx.25,26,27,28
    -   **CVM IP** - 10.42 or 38.xx.29,30,31,32
    -   **HOSTNAME OF HOST** -- POCxx-A

| Name                  | Cluster Name | IPMI IP                                                      | HOST IP                                                      | CVM IP                                                       |
| --------------------- | ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pern Ren              | PHX-POC102   | 10.42.102.33<br>10.42.102.34<br>10.42.102.35<br>10.42.102.36 | 10.42.102.25<br>10.42.102.26<br>10.42.102.27<br>10.42.102.28 | 10.42.102.29<br>10.42.102.30<br>10.42.102.31<br>10.42.102.32 |
| Whai Chun Kit         |              |
| Koh Yong Jun Rick     | PHX-POC183   | 10.38.183.33<br>10.38.183.34<br>10.38.183.35<br>10.38.183.36 | 10.38.183.25<br>10.38.183.26<br>10.38.183.27<br>10.38.183.28 | 10.38.183.29<br>10.38.183.30<br>10.38.183.31<br>10.38.183.32 |
| Pang Yoke Shim Jerome |              |
| Tay Yi Hang           | PHX-POC295   | 10.38.67.33<br>10.38.67.34<br>10.38.67.35<br>10.38.67.36     | 10.38.67.25<br>10.38.67.26<br>10.38.67.27<br>10.38.67.28     | 10.38.67.29<br>10.38.67.30<br>10.38.67.31<br>10.38.67.32     |
| Yip Mun Kit           |              |
| Ong Wu Loong Eric     | PHX-POC030   | 10.42.30.33<br>10.42.30.34<br>10.42.30.35<br>10.42.30.36     | 10.42.30.25<br>10.42.30.26<br>10.42.30.27<br>10.42.30.28     | 10.42.30.29<br>10.42.30.30<br>10.42.30.31<br>10.42.30.32     |
| Enkizen Wen Ming      |              |
| Yap Kian Wee Clarence | PHX-POC031   | 10.42.31.33<br>10.42.31.34<br>10.42.31.35<br>10.42.31.36     | 10.42.31.25<br>10.42.31.26<br>10.42.31.27<br>10.42.31.28     | 10.42.31.29<br>10.42.31.30<br>10.42.31.31<br>10.42.31.32     |
|                       |              |
| Lim Lui Siang Alex    | PHX-POC061   | 10.42.61.33<br>10.42.61.34<br>10.42.61.35<br>10.42.61.36     | 10.42.61.25<br>10.42.61.26<br>10.42.61.27<br>10.42.61.28     | 10.42.61.29<br>10.42.61.30<br>10.42.61.31<br>10.42.61.32     |
|                       |              |
| Tan Rong Tai Damien   | PHX-POC065   | 10.42.65.33<br>10.42.65.34<br>10.42.65.35<br>10.42.65.36     | 10.42.65.25<br>10.42.65.26<br>10.42.65.27<br>10.42.65.28     | 10.42.65.29<br>10.42.65.30<br>10.42.65.31<br>10.42.65.32     |
|                       |              |
| Chong Loo Tong Andrew | PHX-POC018   | 10.42.18.33<br>10.42.18.34<br>10.42.18.35<br>10.42.18.36     | 10.42.18.25<br>10.42.18.26<br>10.42.18.27<br>10.42.18.28     | 10.42.18.29<br>10.42.18.30<br>10.42.18.31<br>10.42.18.32     |
|                       |              |
| Hu Huini Joey         | PHX-POC020   | 10.42.20.33<br>10.42.20.34<br>10.42.20.35<br>10.42.20.36     | 10.42.20.25<br>10.42.20.26<br>10.42.20.27<br>10.42.20.28     | 10.42.20.29<br>10.42.20.30<br>10.42.20.31<br>10.42.20.32     |
|                       |              |
| Wong Teck Yuan Simon  | PHX-POC029   | 10.42.29.33<br>10.42.29.34<br>10.42.29.35<br>10.42.29.36     | 10.42.29.25<br>10.42.29.26<br>10.42.29.27<br>10.42.29.28     | 10.42.29.29<br>10.42.29.30<br>10.42.29.31<br>10.42.29.32     |
|                       |              |

    ![image](images/image105.png)

13. Click **Next**

14. In the **Cluster** page, fill the following details:

    -   **Cluster Name** - POCxx-ABC
    -   **Timezone of Every Hypervisor and CVM** - America/Phoenix
    -   **Cluster Redundancy Factor** - RF2
    -   **Cluster Virtual IP** - 10.42.xx.37
    -   **NTP Servers of Every Hypervisor and CVM** - 0.pool.ntp.org,1.pool.ntp.org,2.pool.ntp.org,3.pool.ntp.org
    -   **DNS Servers of Every Hypervisor and CVM** - <refer to  table above> 
    -   **vRAM Allocation for Every CVM, in Gigabytes** - 32

    ![image](images/foundation-cluster-config.png)

15. Click **Next**

    -   **Select an AOS installer** - Select your uploaded (simply use whatever that was uploaded for you)
        *nutanix_installer_package-release-*.tar.gz* file
    -   **Arguments to the AOS Installer (Optional)** - leave blank

    ![image](images/image106.png)

16. Click **Next**

17. Fill out the following fields and click **Next**:

    -   **Select a hypervisor installer** - AHV, AHV installer bundled inside the AOS installer

    ![image](images/image020.png)

    !!!tip
          Every AOS release contains a version of AHV bundle with that release.
    
18. Click **Next**

19. Enter the existing IPMI credentials as **ADMIN** and **ADMIN** for all three nodes. Note that this will be different in the field.

    ![image](images/image021.png)

20. Click **Start**

21. Confirm that the installer will be active by clicking on **Won't Sleep**

    ![image](images/image021-confirm.png)

22. In the **Warning of Data Loss Possibility** window, click on **Ignore and Re-image**

    ![image](images/image021-ignore-warning.png)

    Foundation will run a couple of tests to make sure all the configuration details you have provided are correct and then direct you the installation progress page.

23. Click the **Log** link to view the realtime log output from your node.

    ![image](images/image022.png)

    When all CVMs are ready, Foundation initiates the cluster creation process.

24. Monitor the foundation process until completion

    ![image](images/image023.png)

25. Once Foundation finishes successully, either click on **Click here**
    link as shown above or open ``https://<Cluster Virtual IP>:9440`` (10.42.xx.37)in your browser

26. Log in with the following credentials:

    -   **Username** - admin
    -   **Change the Password** - *use the same password in RX*

27. Once the password is changed, you can login to Prism Element

    ![image](images/image024.png)

## Takeaways

- You have successfully prepared your environment in a single operation called Foundation:
- 
  - Installed Hypervisor (AHV) - This can also be ESXi or Hyper-V
  - Installed CVM (AOS)
    - Distributed File System (Data Plane)
    - Prism Element (Control Plane) 

## Reset UI Login password

 - Login to CVM via ssh (username: nutanix password: nutanix/4u)
 - execute the following commands 
 - ncli user reset-password user-name="admin" password=ntnx/4DSO




Now we will proceed to install Prism Central(PC).  PC can manage several Prism Elements akin to cloud managers provided by public cloud providers. 