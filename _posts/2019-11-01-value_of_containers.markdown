---
layout: post
title:      "Value of Containers"
date:       2019-11-02 02:52:33 +0000
permalink:  value_of_containers
---


A frequent issue I have encountered while working with in-house development teams, is that the application works in the development environment, but fails to run or operate strangely in the production environment. This can usually be attributed to drift between development and production. During development, the developer's environment tends to accumulate extras (gems, workarounds and scripts) that do not follow into production.  Additionally, developers usually  have difficulty fixing production issues due to the missing accumulated extras or differences environment layouts. Virtual machines are only able to provide limited relief to this problem as long lived virtual machines would accumulate drift as well.

With the introduction of containers, it has become much easier to ensure that production and development don't drift from each other. Containers, like virtual machines, allow the developer to create their own environments for their application. However, the container cannot have a different OS from the host machine without a virtualization layer. Thus, Windows host must have a Windows container and Linux host must have a Linux container. Additionally, the developer can be confident the systems administrators are not deploying the application without the needed dependencies or supporting files. Running containers are updated in-place, and the state is maintained in an external volume(s). Additionally, containers also provide some security isolation for applications and can be tailored to the applications needs to be more or less secure. However, all containers share the same kernel with their host's and are vulnerable to potential kernel exploits. If you want more aggressive isolation, you can look at Gvisor or Kata containers. Though this will increase the resource requirements and start up time of containers.

While many applications tend to work well inside a container, it can be difficult to move legacy or larger monolithic applications to a container. Legacy applications tend to have workarounds applied to them over the years and forgotten/obscure dependencies that integrate deeply with the host OS. Large monolithic applications, like legacy, tend to have deep ties to the host machine.  For instance, a legacy application I have worked with made use of specific applications and file system features for high availability and clustering.

If you are looking to start in container applications, it is best to look at the docker documentation.  While docker has run into many competing offerings, such as podman, buildah, and CRI-O, it is still the defector standard by which other applications are measured against.

