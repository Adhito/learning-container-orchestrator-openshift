# Project Learning OpenShift Local / Code Ready Container (CRC)

### **Stage 1: Introduction to Code Ready Container (CRC)**
---
**Sub-Stage 1.1: Differences between CRC and OCP**

- Please do note that the OpenShift Container Platform cluster is ephemeral 
- The CRC will use single node which behaves as both a control plane and worker node.
- The cluster uses the  **172**  address range. This can cause issues when, for example, a proxy is run in the same address space.
<br />
<br />




### **Stage 2: Minimum Requirements**
---
**Sub-Stage 2.1: Requirements To Deploy  CRC on Windows 11**

When installing CRC here are the requirement that need to be full-filled before proceeding to the next stage.

| Resource Name   	| Minimum                       | Recommended                 |
|-------------------|-------------------------------|-----------------------------|
|CPU				| 4 vCPU			            | 8 vCPU            		  |
|RAM             	| 9 GB            				| 16 GB            			  |
|Storage          	| 35 GB							| 100 GB					  | 
|Windows          	| Windows 11 Pro (Hyper-V Enabled) 				| Windows 11 Pro (Hyper-V Enabled)						  | 
<br />
<br />




### **Stage 3: Setting Up CRC**
---
**Sub-Stage 3.1: ## Installing The Red Hat OpenShift Local**

- Download the  [latest release of Red Hat OpenShift Local](https://console.redhat.com/openshift/create/local)  for your platform.
- On Microsoft Windows, extract the contents of the archive.
- On macOS or Microsoft Windows, run the guided installer and follow the instructions.
<br />
<br />

**Sub-Stage 3.2: ## Setup The  Red Hat OpenShift Local**

- Prerequisites : 
	- Before running the CRC setup please make sure you are not running on an **elevated command prompt** otherwise CRC might not start.
	- Allow/Whitelist firewall connection from CRC either by adding it manually or accepting UAC prompt when asked
 	- [ INSERT PICTURE ] - Windows Firewall Settings
	- Allow/Whitelist CRC process from active AV or EDR
	- [ INSERT PICTURE ] - Microsoft Defender Settings
	- During the CRC setup please ensure you are not connected to VPN and the network is stable in order to download the CRC image.
	- For the OpenShift preset, ensure that you have a valid OpenShift user pull secret. Copy or download the pull secret from the Pull Secret section of the [Red Hat OpenShift Local page on the Red Hat Hybrid Cloud Console](https://console.redhat.com/openshift/create/local).
- Once the installation is complete initialize the CRC with the following command : 
    
    ```bash
    $ crc setup
    ```
<br />
<br />


**Sub-Stage 3.3: ## Configuring The Red Hat OpenShift Local**
- The  `crc setup`  command configures your system to run OpenShift and caches the VM image in  `$HOME/.crc`. However, it does not start the cluster automatically. At this point you could start the cluster with the default configuration. If your machine has more resources and you want to increase the resources available for your OpenShift cluster, you can adjust the VM configuration—like the number of CPUs or RAM—using  `crc config`.

- The default configuration creates a VM with 4 virtual CPUs and 9GB of RAM. This is enough for many cases but you may require more resources depending on your application requirements. For example, to increase the number of virtual CPUs to 8 and the memory to 16GB, run  `crc config`  like this:

- Set the CPU Resources : 
    ```bash
    $ crc config set cpus 8
    ```
    
- Set the RAM Resource : 
    ```bash
    $ crc config set memory 16384
    ```
    
- To view the available configurable properties: 
    ```bash
    $ crc config --help
    ```
    
- To view the complete current configuration:
    ```bash
    $ crc config view
    ```
<br />
<br />

**Sub-Stage 3.4: ## Starting The Red Hat OpenShift Local**

- Once the configuration to set the vCPU and RAM is completed to the recommended specs you can start the CRC with the following command :
    ```bash
    $ crc start
    ```
- When the crc start is initiated, the console will ask the pull secret, you can copy the pull secret from the Redhat Hybrid Cloud Console and paste it on the console <br />
	- [ INSERT PICTURE ] - Redhat Hybrid Cloud Console Pull Secret
	- [ INSERT PICTURE ] - Terminal Asking For Pull Secret 
	- 
- Alternatively you can also pass the full path to the `pull-secret` file you downloaded before in the command line to avoid having to paste it during the install:
    ```bash
    $ crc start -p ~/User/pull-secret
    ```

- After a few minutes, the cluster is up and running and  `crc`  prints the connection information:

	```shell
	Started the OpenShift cluster.

	The server is accessible via web console at:
	  https://console-openshift-console.apps-crc.testing

	Log in as administrator:
	  Username: kubeadmin
	  Password: PpQNn-HNABv-MxRuE-gTFBR

	Log in as user:
	  Username: developer
	  Password: developer

	Use the 'oc' command line interface:
	  $ eval $(crc oc-env)
	  $ oc login -u developer https://api.crc.testing:6443
	```
<br />
<br />


### **Post-Stage Installation : Moving CRC VM Location from C: Drive onto other drive**
---
**Post-Stage 1.0: Moving CRC Data Location With MKLink**

- Before creating the symlink/mklink please esure that .crc folder have not been created before creating the link( By default the .crc is located at C:\Users\UserName\.crc )
- Create the .crc folder at the desired location, in this example we will move the .crc onto D:\Programming-Environment-01\VM-OpenShift-CRC\.crc
- Create the symlink/mklink with the following command :
    ```bash
    $ mklink /J C:\Users\Adhito\.crc D:\Archive\Programming-Environment-01\VM-OpenShift-CRC\.crc
    ```
- Create the crc cluster with the setup & run command
    ```bash
    $ crc setup
    $ crc start
    ```
**Post-Stage 1.1: Moving CRC Data Location With Environment Variable Override**

- Before creating the CRC cluster run the following command
    ```bash
    $ Set-Variable -Name HOME -Value D:\Programming-Environment-01\VM-OpenShift-CRC -Force
    ```
- Create the crc cluster with the setup & run command
    ```bash
    $ crc setup
    $ crc start
    ```

