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

|    | Name                 | Foundation VM | Foundation VM IP |
|----|----------------------|---------------|------------------|
| 1  | Giam Xiong Yao       | FOVM_001      | 10.42.36.78      |
| 2  | Goh Hao Wei          | FOVM_002      | 10.42.36.77      |
| 3  | Lim Xi Yang          | FOVM_003      | 10.42.36.76      |
| 4  | Ong Sheng Jian       | FOVM_004      | 10.42.36.71      |
| 5  | Seah Wei Hong        | FOVM_005      | 10.42.36.75      |
| 6  | Tay Yi Hsuen         | FOVM_006      | 10.42.36.72      |
| 7  | Tanya Elizabeth Khoo | FOVM_007      | 10.42.36.74      |
| 8  | Soh Boon Yen         | FOVM_008      | 10.42.36.56      |
| 9  | Lim Jun Wei          | FOVM_009      | 10.42.36.59      |
| 10 | Kenneth Neoh Kim How | FOVM_010      | 10.42.36.61      |
| 11 | Yee Jun Wei          | FOVM_011      | 10.42.36.54      |
| 12 | Yang Kai Ze          | FOVM_012      | 10.42.36.64      |
| 13 | Lim Ka Tiong         | FOVM_013      | 10.42.36.63      |
| 14 | Wong Wei En, Matthew | FOVM_014      | 10.42.36.66      |
| 15 | Wong Chin Hao        | FOVM_015      | 10.42.36.65      |
| 16 |                      | FOVM_016      | 10.42.36.67      |
| 17 |                      | FOVM_017      | 10.42.36.69      |
| 18 |                      | FOVM_018      | 10.42.36.70      |
| 19 |                      | FOVM_019      | 10.42.36.55      |
| 20 |                      | FOVM_020      | 10.42.36.68      |

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
    -   **Number of nodes** - 1
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


    |    | Name                 | Cluster Name | IPMI IP      | HOST IP      | CVM IP       | Cluster Name | Cluster IP   | DSIP         |
    |----|----------------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|
    | 1  | Giam Xiong Yao       | PHX-POC263   | 10.38.35.34  | 10.38.35.25  | 10.38.35.29  | PHX-POC263-A | 10.38.35.50  | 10.38.35.55  |
    | 2  | Goh Hao Wei          | PHX-POC263   | 10.38.35.35  | 10.38.35.26  | 10.38.35.30  | PHX-POC263-B | 10.38.35.51  | 10.38.35.56  |
    | 3  | Lim Xi Yang          | PHX-POC263   | 10.38.35.36  | 10.38.35.27  | 10.38.35.31  | PHX-POC263-C | 10.38.35.52  | 10.38.35.57  |
    | 4  | Ong Sheng Jian       | PHX-POC263   | 10.38.35.37  | 10.38.35.28  | 10.38.35.32  | PHX-POC263-D | 10.38.35.53  | 10.38.35.58  |
    | 5  | Seah Wei Hong        | PHX-POC204   | 10.38.204.33 | 10.38.204.25 | 10.38.204.29 | PHX-POC204-A | 10.38.204.50 | 10.38.204.55 |
    | 6  | Tay Yi Hsuen         | PHX-POC204   | 10.38.204.34 | 10.38.204.26 | 10.38.204.30 | PHX-POC204-B | 10.38.204.51 | 10.38.204.56 |
    | 7  | Tanya Elizabeth Khoo | PHX-POC204   | 10.38.204.35 | 10.38.204.27 | 10.38.204.31 | PHX-POC204-C | 10.38.204.52 | 10.38.204.57 |
    | 8  | Soh Boon Yen         | PHX-POC204   | 10.38.204.36 | 10.38.204.28 | 10.38.204.32 | PHX-POC204-D | 10.38.204.53 | 10.38.204.58 |
    | 9  | Lim Jun Wei          | PHX-POC002   | 10.42.2.33   | 10.42.2.25   | 10.42.2.29   | PHX-POC002-A | 10.42.2.50   | 10.42.2.55   |
    | 10 | Kenneth Neoh Kim How | PHX-POC002   | 10.42.2.34   | 10.42.2.26   | 10.42.2.30   | PHX-POC002-B | 10.42.2.51   | 10.42.2.56   |
    | 11 | Yee Jun Wei          | PHX-POC002   | 10.42.2.35   | 10.42.2.27   | 10.42.2.31   | PHX-POC002-C | 10.42.2.52   | 10.42.2.57   |
    | 12 | Yang Kai Ze          | PHX-POC002   | 10.42.2.36   | 10.42.2.28   | 10.42.2.32   | PHX-POC002-D | 10.42.2.53   | 10.42.2.58   |
    | 13 | Lim Ka Tiong         | PHX-POC007   | 10.42.7.33   | 10.42.7.25   | 10.42.7.29   | PHX-POC007-A | 10.42.7.50   | 10.42.7.55   |
    | 14 | Wong Wei En, Matthew | PHX-POC007   | 10.42.7.34   | 10.42.7.26   | 10.42.7.30   | PHX-POC007-B | 10.42.7.51   | 10.42.7.56   |
    | 15 | Wong Chin Hao        | PHX-POC007   | 10.42.7.35   | 10.42.7.27   | 10.42.7.31   | PHX-POC007-C | 10.42.7.52   | 10.42.7.57   |
    | 16 |                      | PHX-POC007   | 10.42.7.36   | 10.42.7.28   | 10.42.7.32   | PHX-POC007-D | 10.42.7.53   | 10.42.7.58   |
    | 17 |                      | PHX-POC062   | 10.42.62.33  | 10.42.62.25  | 10.42.62.29  | PHX-POC062-A | 10.42.62.50  | 10.42.62.55  |
    | 18 |                      | PHX-POC062   | 10.42.62.34  | 10.42.62.26  | 10.42.62.30  | PHX-POC062-B | 10.42.62.51  | 10.42.62.56  |
    | 19 |                      | PHX-POC062   | 10.42.62.35  | 10.42.62.27  | 10.42.62.31  | PHX-POC062-C | 10.42.62.52  | 10.42.62.57  |
    | 20 |                      | PHX-POC062   | 10.42.62.36  | 10.42.62.28  | 10.42.62.32  | PHX-POC062-D | 10.42.62.53  | 10.42.62.58  |

    ![image](images/image105.png)

13. Click **Next**

14. In the **Cluster** page, fill the following details:

    -   **Cluster Name** - POCxx-ABC
    -   **Timezone of Every Hypervisor and CVM** - America/Phoenix
    -   **Cluster Redundancy Factor** - RF2
    -   **Cluster Virtual IP** - 10.42.xx.xx
    -   **NTP Servers of Every Hypervisor and CVM** - 0.pool.ntp.org,1.pool.ntp.org,2.pool.ntp.org,3.pool.ntp.org
    -   **DNS Servers of Every Hypervisor and CVM** - <refer to  table above>
    -   **vRAM Allocation for Every CVM, in Gigabytes** - 32

    ![image](images/foundation-cluster-config.png)

15. Click **Next**

    -   **Select an AOS installer** - Select your uploaded (simply use whatever that was uploaded for you)
        *nutanix_installer_package-release-*.tar.gz* file
    -   **The AOS Should be 6.8, screenshot file is for reference**    
    -   **Arguments to the AOS Installer (Optional)** - leave blank

    ![image](images/image106.png)

16. Click **Next**

17. Fill out the following fields and click **Next**:

    -   **Select a hypervisor installer** - AHV, AHV installer bundled inside the AOS installer
    -   **Select AHV-DVD-x86_64-el8.nutanix.20230302.100187.iso** - from AOS 6.8 onwards, hypervisor file needs to be uploaded to Foundation VM.


    ![image](images/image020.png)

    !!!tip
          Every AOS release contains a version of AHV bundle with that release.

18. Click **Next**

19. Enter the existing IPMI credentials as **ADMIN** and **ADMIN** for all nodes. Note that this will be different in the field.

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

    - IMPORTANT: Foundation will not be able to successfully create cluster for this version of AOS. We will need to SSH into CVM IP using Putty.
    - **Username** - nutanix
    - **Change the Password** - *nutanix/4u*
    - run the following command to create a 1 node cluster
    - ``cluster --cluster_name=PHX-POC263-A --cluster_external_ip=10.38.xx.xx --ntp_servers=0.POOL.NTP.ORG --dns_servers=10.42.194.10 --svm_ips=10.38.xx.xx --cluster_function_list=one_node_cluster create``
    - Please refer to table for External IP, CVM IP and Cluster Name

    |    | Name                 | HOST IP      | CVM IP       | Cluster Name | Cluster IP   | DSIP         |
    |----|----------------------|--------------|--------------|--------------|--------------|--------------|
    | 1  | Giam Xiong Yao       | 10.38.35.25  | 10.38.35.29  | PHX-POC263-A | 10.38.35.50  | 10.38.35.55  |
    | 2  | Goh Hao Wei          | 10.38.35.26  | 10.38.35.30  | PHX-POC263-B | 10.38.35.51  | 10.38.35.56  |
    | 3  | Lim Xi Yang          | 10.38.35.27  | 10.38.35.31  | PHX-POC263-C | 10.38.35.52  | 10.38.35.57  |
    | 4  | Ong Sheng Jian       | 10.38.35.28  | 10.38.35.32  | PHX-POC263-D | 10.38.35.53  | 10.38.35.58  |
    | 5  | Seah Wei Hong        | 10.38.204.25 | 10.38.204.29 | PHX-POC204-A | 10.38.204.50 | 10.38.204.55 |
    | 6  | Tay Yi Hsuen         | 10.38.204.26 | 10.38.204.30 | PHX-POC204-B | 10.38.204.51 | 10.38.204.56 |
    | 7  | Tanya Elizabeth Khoo | 10.38.204.27 | 10.38.204.31 | PHX-POC204-C | 10.38.204.52 | 10.38.204.57 |
    | 8  | Soh Boon Yen         | 10.38.204.28 | 10.38.204.32 | PHX-POC204-D | 10.38.204.53 | 10.38.204.58 |
    | 9  | Lim Jun Wei          | 10.42.2.25   | 10.42.2.29   | PHX-POC002-A | 10.42.2.50   | 10.42.2.55   |
    | 10 | Kenneth Neoh Kim How | 10.42.2.26   | 10.42.2.30   | PHX-POC002-B | 10.42.2.51   | 10.42.2.56   |
    | 11 | Yee Jun Wei          | 10.42.2.27   | 10.42.2.31   | PHX-POC002-C | 10.42.2.52   | 10.42.2.57   |
    | 12 | Yang Kai Ze          | 10.42.2.28   | 10.42.2.32   | PHX-POC002-D | 10.42.2.53   | 10.42.2.58   |
    | 13 | Lim Ka Tiong         | 10.42.7.25   | 10.42.7.29   | PHX-POC007-A | 10.42.7.50   | 10.42.7.55   |
    | 14 | Wong Wei En, Matthew | 10.42.7.26   | 10.42.7.30   | PHX-POC007-B | 10.42.7.51   | 10.42.7.56   |
    | 15 | Wong Chin Hao        | 10.42.7.27   | 10.42.7.31   | PHX-POC007-C | 10.42.7.52   | 10.42.7.57   |
    | 16 |                      | 10.42.7.28   | 10.42.7.32   | PHX-POC007-D | 10.42.7.53   | 10.42.7.58   |
    | 17 |                      | 10.42.62.25  | 10.42.62.29  | PHX-POC062-A | 10.42.62.50  | 10.42.62.55  |
    | 18 |                      | 10.42.62.26  | 10.42.62.30  | PHX-POC062-B | 10.42.62.51  | 10.42.62.56  |
    | 19 |                      | 10.42.62.27  | 10.42.62.31  | PHX-POC062-C | 10.42.62.52  | 10.42.62.57  |
    | 20 |                      | 10.42.62.28  | 10.42.62.32  | PHX-POC062-D | 10.42.62.53  | 10.42.62.58  |

    Once cluster creation completed, open ``https://<Cluster Virtual IP>:9440`` (10.42.xx.xx)in your browser

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
 - ncli user reset-password user-name="admin" password=ntnx/4DSTA




Now we will proceed to install Prism Central(PC).  PC can manage several Prism Elements akin to cloud managers provided by public cloud providers.
