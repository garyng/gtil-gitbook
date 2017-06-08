---
layout: post
title: 'Setting Up Samba on Ubuntu'
tags: ['samba', 'ubuntu']
category: 'ubuntu'
date: '2017-06-08 22:26'
author: 'GaryNg'
---

# Setting Up Samba on Ubuntu
## Solution
1. Create a new folder > Right Click > Properties > Local Network Share > Share this folder  
![Sharing folder in Ubuntu](../images/posts/setting-up-samba-on-ubuntu/2017-06-08_223707.png)
2. Install the services  
![Installing the services](../images/posts/setting-up-samba-on-ubuntu/2017-06-08_223826.png)
3. Check `Allow others to create and delete files in this folder`
![Allow others to create and delete files in this folder](../images/posts/setting-up-samba-on-ubuntu/2017-06-08_223928.png)

### Accessing the Folder on Windows
1. Open File Explorer > Goto the IP address of the Ubuntu machine  
![Accessing the shared folder on Windows](../images/posts/setting-up-samba-on-ubuntu/2017-06-08_224350.png)
2. Enter the credentials if required  
![Entering the username and pasword](../images/posts/setting-up-samba-on-ubuntu/2017-06-08_224528.png)

## Reference
[Samba/SambaServerGuide](https://help.ubuntu.com/community/Samba/SambaServerGuide)

[Samba/SambaClientGuide](https://help.ubuntu.com/community/Samba/SambaClientGuide)
