---
layout: post
title: 'Give HyperV VM Internet Access'
tags: ['hyperv', 'vm']
category: 'hyperv'
date: '2017-06-08 18:43'
author: 'GaryNg'
---

# Give HyperV VM Internet Access
## Solution
### Creating a New Virtual Swtich
1. Open Hyper-V Manager
2. Goto Action > Virtual Switch Manager...  
![Virtual Swtich Manager...](../images/posts/give-hyperv-vm-internet-access/2017-06-08_184621.png)
3. Select External > Create Virtual Switch  
![Create a new external virtual switch](../images/posts/give-hyperv-vm-internet-access/2017-06-08_184758.png)
4. Name the switch > select the correct network card (which is connected to the Internet) > Click OK  
	![Creating the virtual switch](../images/posts/give-hyperv-vm-internet-access/2017-06-08_185034.png)

### Configuring the Virtual Machine
1. Choose the virtual machine > Settings  
![Select the virtual machine](../images/posts/give-hyperv-vm-internet-access/2017-06-08_190201.png)
2. Goto Network Adapter > Select the created virtual switch > OK  
![Select the created virtual switch](../images/posts/give-hyperv-vm-internet-access/2017-06-08_190329.png)

## Reference
[Windows 8 Hyper-V - how to give VM internet access?](https://superuser.com/questions/469806/windows-8-hyper-v-how-to-give-vm-internet-access)
