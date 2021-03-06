Cloud Computing Development Track Day 2 (VEP)
---------------------------------------------------

Hypervisors structure:
----------------------

	USER SPACE <APPS>
	Kernel Space
	HW. Emulator
	
Virtualization Tools:
---------------------

	1. KVM 
	2. Xen 
	3. VMware
		
			- Vsphere	
			- VMware workstation
			
	4. RedHat	RHEV
	5. Windows	Hyper-v



Vendors:
--------

		- VMware
		- CITRIX
		- RedHat
		- Microsoft
		
Server Virtualization:
----------------------

1- Fully Virtualization 
		
				---------------------------------
				| Guest	| Windows | Linux OS| ..|
				----------------------------------
				|		| 		HyperVisor		|
				---------------------------------
				|		|		Kernel 			|
				|  HOST	-------------------------
				|		| Physical Hardware		|
				--------------------------------

			 Advantages:
				- able to run over any operating system
			 disadvantages:
				- lower performance due to using the hiegest number of virtualization stack
				
			 Examples:
					VMware Workstation


2- Para Virtualization

			------------------------------------
			Guest OS | Guest OS ...
			------------------------------------
			Hypervisor
			------------------------------------
			Share Xen Kernel for all Guest OSes
			------------------------------------
			HardWare
			-------------------------------------
			
			
			in para virtualization all OSes in para share the same kernel in case of Microsoft Windows uses the full
			stack virtualization

			- XEN Kernel:
				- disadvantages --- specific linux kernel, where kernel limitaions.
			- XEN citrix: provides XENServer, XenDesktop
			
			
3- kernel virtualization

			- KVM: Enable Hypervisor operation in linux kernel, where KVM provides the 
					virtualization layer on the same kernel of Host OS
			
			
			------------------------------
			VM1 "APP + Kernel" | VM2 | VM3
			------------------------------
			KERNEL
			------------------------------
			Physical Hardware
			------------------------------
			
			- Technologies: RHEV "RedHat Enterprise Virtualization"
							VMware-Vsphere and V-cloud
							

Types of Hypervisor:
--------------------

Type 1 : Bare-Metal Hypervisor

			-----------------------------------------------
			| OS1 | OS2| .................................| 
			-----------------------------------------------
			|			Virtualization Layer			  |
			-----------------------------------------------
			| X86 Architecture "CPU + RAM + NIC + Storage"|
			-----------------------------------------------

		1- VMware ESX and ESXI has a management tool called Vcenter
		2- RHEV-H	has a Management tool called RHEV-M
		
				-----------------------------								 -----------------	
				|H1|		|H2|		|H3|	Hypervisor servers --------> | SHARED STORAGE|		
				-----------------------------								 ----------------- 	
				  |			 |			 |
				  |----------------------|
							|
					---------------------
					|	Management Tool |		Management Server
					---------------------									-------------
							|-----------------------------------------------|	Client 	|
																			-------------
				
				- Better performance for virtual machine provisioning
				- support live migration for from strugglers Hypervisor server to another.
				- But for live migration, all virtual machine must be shared on the same physical storage
				  to be enabled, they use the meta data of virtual machine on shared physical storage 
				  to start any virtual machine and balance the load over hypervisor servers.
				- this type of virtualization supports the high availability and data consistancy of service. 


		- Live Migeration:
		------------------
										-------------STORAGE---------
										|							|
					|Guest OS1|	|Guest OS1|				|Guest OS1||Guest OS1|
					-----------------------				----------------------
					|	HyperVisor 1	  |				| Hypervisor 2		|
					-----------------------				----------------------	

			- Failure Detector: User specify in configurations how to detect the Virtual Machine Failure to migrate the VM from H1 to 
			  H2 and vice versa.
			- Provide Fast Recovery time with minimal down time.

		- Storage:
		----------
				1. Backup/clone: by cloning virtual machine 'Full backup' the same size of the source Virtual machine
				2. Snapshot: copying of index but the data still exists, if there is any change (Edit/Delete/Add) in file  
				   system, copy this change to snapshot, to keep track all changes in file system. according to processes that 
				   run on virtual machine: when user takes snapshot it follows the "Snapshot Algorithm" or Chandy–Lamport algorithm
				   is used to track all running processes at specific time and build save all running processes states in vector where 
				   each process has list of states and communication with other processes on the system.			

			
			
Type 2: Hosted Hypervisor

			-------------------------------------
			|		|	Guest OS | Guest OS	| ..|
			|	APP	-----------------------------
			|		| Virtualization Layer		|
			-------------------------------------
			|		Physical Hardware			|
			-------------------------------------

Notes:

		Hardware assistance:
	
			improve performance and support virtualization of DMA I/O and memory virtualization 
			for example VT-x and AMD-V started being introduced into CPU desgins in 2005


		Dynamic Load Balancing:
		-----------------------
		
			- Load balancing is used to distribute the load over virtual machines in cluster. 
			- From network prespective it scales the performance of a server-based program, such as a Web server, by distributing 
			its client requests across multiple servers within the cluster. As traffic increases, additional servers 
			can be added to the cluster, with up to 32 servers possible in any one cluster. High availability.
			- High availability provides: active<------->standby in clustering 
			- Load balancing provides:	active <--------> active  


Network Virtualization:
-----------------------
		
		
				VM1 | VM2				VM3| .......
				----------				--------------
				Virtual switch/Router    Virtual switch/Router
				- Using Bridging		- Using Bridging
				- Using NAT				- Using NAT
					H1						H2
				---------				--------------
				   NIC1			  			NIC2
				----------				--------------
					|						|
					|	--------			|
					----|SWITCH|-------------	
						--------										---------		
							|-------------------------------------------|YOUR PC|
																		---------	
		- Virtual Isolated network (Host Only)
			
		- Bridged:
				
				A bridge is a device that separates two or more network segments within one logical network connected directly to physical host.
				
		- Network address translation:
				
				(NAT) is a methodology of remapping one IP address space into another by modifying network address information in
				Internet Protocol (IP) datagram packet headers while they are in transit across a traffic routing device.

		
					10.0.0.5	 
				PC1 --------------------	Local Network
					10.0.0.6			|----------------->|Router|---->Ineternet--->www.google.com (8.8.8.8)
				PC2	--------------------	10.0.0.1		(Public IP of router)42.2.1.3
		
					
					Router:
					change the ip of PC1 address to router address in destination and route it back to PC1 after recieving packets from 8.8.8.8.
																
							Source 				Distenationn
							10.0.0.5			8.8.8.8
					
		- VLAN: Virtual LAN:
					
					A VLAN is a group of end stations with a common set of requirements, independent of physical location. VLANs have 
					the same attributes as a physical LAN but allow you to group end stations even if they are not located physically 
					on the same LAN segment.
							
							----------------------------------
							|PC1 						PC2  |
							|Eth0		VLAN			Eth1 |
							----------------------------------
											|
								|---------ROUTER----------|
											|
								PC3--------------------PC4			




Desktop Virtualization:
-----------------------

	Desktop Virtualization embarces number of technologies with different attributes:

		- Thin Terminal (Thin Client virtualization) is used for remote access
		- Small provisioning time 
		- Roaming
		- Distaster Recovery





