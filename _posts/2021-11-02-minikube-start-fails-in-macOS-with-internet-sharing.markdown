---
layout: post
author: Juande Santander-Vela
title:  "Minikube start fails in macOS with Internet Sharing activated"
categories: command-line-interface, macOS, docker, minikube, hyperkit, virtualbox, containers
---

I have not seen this issued mentioned, much less resolved, anywhere on the internet, som I'm posting this just in case you find yourself running into this issue.

Because of the amount of resource usage (also known as unacceptably hot and almost unusable laptop state), but also due to their recent policy changes, I've decided to move away from the official Docker Community Edition, into the usage of Minikube and HyperKit.

I followed the [instructions from Arnon Rotem-Gal-Oz on Cirrus Minor][1], and they worked quite well: just type

[1]: https://arnon.me/2021/09/replace-docker-with-minikube/ "Cirrus Minor: Replacing Docker Desktop with hyperkit + minikube"

    brew install hyperkit
    brew install minikube
    brew install docker # assuming you don't have the official Docker distribution, or you've removed it
    minikube start
    eval $(minikube docker-env) # creates the relevant Docker environmenta variables

However, after a reboot, when I wanted to restart the minikube with `minikube start`, things failed:

    $ minikube start
    😄  minikube v1.23.2 on Darwin 11.6.1
        ▪ MINIKUBE_ACTIVE_DOCKERD=minikube
    ✨  Using the hyperkit driver based on existing profile
    👍  Starting control plane node minikube in cluster minikube
    🔄  Restarting existing hyperkit VM for "minikube" ...
    🤦  StartHost failed, but will try again: driver start: getting MAC address from UUID: vmnet: error from vmnet.framework: -1

    🔄  Restarting existing hyperkit VM for "minikube" ...
    😿  Failed to start hyperkit VM. Running "minikube delete" may fix it: driver start: getting MAC address from UUID: vmnet: error from vmnet.framework: -1


    ❌  Exiting due to PR_HYPERKIT_VMNET_FRAMEWORK: Failed to start host: driver start: getting MAC address from UUID: vmnet: error from vmnet.framework: -1

    💡  Suggestion: Hyperkit networking is broken. Upgrade to the latest hyperkit version and/or Docker for Desktop. Alternatively, you may choose an alternate --driver
    🍿  Related issues:
        ▪ https://github.com/kubernetes/minikube/issues/6028
        ▪ https://github.com/kubernetes/minikube/issues/5594

The message seems to imply that the issue is with HyperKit, or with the HyperKit/Minikube interaction. But the strange thing is that it had worked very well before…

I tried to delete the minikube completely, using `minikube delete --all purge`, but that did not help at all. I also tried using the virtualbox driver, but that also failed:

    $ minikube delete
    🔥  Deleting "minikube" in hyperkit ...
    💀  Removed all traces of the "minikube" cluster.
    
    $ minikube start --driver=virtualbox
    😄  minikube v1.23.2 on Darwin 11.6.1
        ▪ MINIKUBE_ACTIVE_DOCKERD=minikube
    ✨  Using the virtualbox driver based on user configuration
    👍  Starting control plane node minikube in cluster minikube
    🔥  Creating virtualbox VM (CPUs=2, Memory=4000MB, Disk=20000MB) ...
    ❌  minikube is unable to connect to the VM: dial tcp 192.168.99.106:22: i/o timeout

    	This is likely due to one of two reasons:

    	- VPN or firewall interference
    	- virtualbox network configuration issue

    	Suggested workarounds:

    	- Disable your local VPN or firewall software
    	- Configure your local VPN or firewall to allow access to 192.168.99.106
    	- Restart or reinstall virtualbox
    	- Use an alternative --vm-driver
    	- Use --force to override this connectivity check
	

    ❌  Exiting due to GUEST_PROVISION: Failed to validate network: dial tcp 192.168.99.106:22: i/o timeout

    ╭───────────────────────────────────────────────────────────────────────────────────────────╮
    │                                                                                           │
    │    😿  If the above advice does not help, please let us know:                             │
    │    👉  https://github.com/kubernetes/minikube/issues/new/choose                           │
    │                                                                                           │
    │    Please run `minikube logs --file=logs.txt` and attach logs.txt to the GitHub issue.    │
    │                                                                                           │
    ╰───────────────────────────────────────────────────────────────────────────────────────────╯

And even `minikube logs` does not work, because the control plane is not started!

What to do? I tried to thing of things that had changed, and I had activated a VPN. I removed the VPN configuration… and it still did not work.

Not sure what was the mental jump that made me realise that Internet Sharing might be something that might change MAC addreses as seen by HyperKit, but I went, deactivated Internet Sharing… and lo and behold! the issue was resolved…

So I'm not sure exactly how I managed to start the minikube in the first place, because I think I had Internet Sharing active, but the real thing is that you can indeed use Internet Sharing… after you have started the minikube. But just bear in mind that there might be networking errors in your minikube that might be related to Internet Sharing…

Hope that helps!

ps. I've raised it as an [issue in Minikube][2], as this happens both with HyperKit and VirtualBox…

[2]: https://github.com/kubernetes/minikube/issues/12840 "Github: kubernetes/minikube issue #12840: Minikube start fails in macos Big Sur with Internet Sharing on regardless of driver"