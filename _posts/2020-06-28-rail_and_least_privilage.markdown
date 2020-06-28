---
layout: post
title:      "Rail and least Privilage"
date:       2020-06-28 19:38:08 +0000
permalink:  rail_and_least_privilage
---


A recommended best practice of securing servers is to reduce the attack surface. This involves removing or turning off anything that is not needed by the server. For instance, Microsoft server has modes that disable graphical user interface and even RDP. This will both diminish a server's chance of getting exploited and odd interactions that can happen between services. In addition to security and stability advantages, it can also reduce server requirements.

When starting my rails project, I wondered why people would choose to use Sinatra when the is so much backed into rails. As I worked through my project, I received a few vulnerability alerts, from GitHub, on dependencies rails was using. Some of these would have also affected Sinatra, however with fewer dependencies, there is less to get affected.

While the proliferation of gems and similar library packages does make it easier to develop a solution by using pre-built components, it does have risks. You need to trust that the gems you're using are not malicious or have a bad implementation. Best practices recommend using well-trusted gems that are currently maintained. This will greatly reduce your risk, but you still need to be vigilant.  The rails command line has the option to disable features and options if not needed.

The next step is to reduce the reach of exploitation and failures. The objective is to provide each application with the least amount of capabilities needed to do their job. For instance, a web application will likely not need to change the server's users/ passwords, change system time, or other privileged tasks. The quickest way is for, if possible, each application should run as a unique non-privileged account. This will prevent the application from modifying the system or other applications. If an application must run as privileged, most modern OS's have a way to selectively provide privileges instead of granting all of them.

After isolating based on the running user, applications can be limited to external access. The application will need to run and connect to resources outside of itself to do meaningful work, such as storage, system calls, and third-party API. Most external resources will have a mechanism to set limits.  For example, our application may need to read and write from the SQL server, however, it is unlikely to need administrative access to the server itself. Additionally segmenting access can provide limits as well. For example, data passed a certain time or event should be purged from servers or moved into secure cold storage. This is a big part of compliance with many standards.

Finally, an application can be broken into multiple processes and discrete subcomponents. This way if one component is exploited, the reach is limited. Then each subcomponent is access limited.  For instance, the controller layer does not need disk access. In rails convention limits access, not a security barrier. Additionally, only select processes will need to know about secrets instead of the entire application, such as the SSO key and secret used by Omniauth. However, this does add complexity to the network or IPC layer and increase application requirements. 

