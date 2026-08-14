Cybersecurity Lab Setup

Networkwalks | Project 1 | Tools: VirtualBox + Kali Linux

Project Overview

This project documents the setup of an isolated virtual cybersecurity lab using VirtualBox and Kali Linux. The lab was built as a controlled, sandboxed environment for practicing security tools, network scanning, and general penetration testing techniques without putting the host machine or the home network at risk.

Why a Sandbox and Why an Isolated Network?

Security tools such as scanners, exploit frameworks, and malware samples can behave unpredictably. Running them directly on a host machine or a shared home network can expose real devices to accidental damage, data loss, or unwanted network traffic. An isolated virtual lab solves this by:

Keeping all testing activity inside a virtual machine that can be reset or deleted at any time.
Preventing lab traffic from reaching the home network or the internet unless it is explicitly needed.
Allowing multiple virtual machines to be added later as attacker and target systems without touching the host system.
Making it safe to experiment, break things, and learn from mistakes without real-world consequences.

Internal Network Name	CyberLab
Network Address	10.0.0.0/24
Kali IP Address	10.0.0.2/24
Default Gateway	10.0.0.1
DNS Server	8.8.8.8
Future VM Range	10.0.0.3 - 10.0.0.99



Step by Step Build
Step 1: Install VirtualBox

VirtualBox was installed on the host machine to act as the hypervisor for the lab. This is the base platform that all virtual machines run on.

Step 2: Import Kali Linux

The Kali Linux virtual machine image was downloaded from the official Kali website and imported into VirtualBox. Kali was chosen because it comes preloaded with the security and penetration testing tools needed for this and future lab work.

Step 3: Configure the Network Adapters

Two network adapters were configured on the Kali VM so the machine could stay isolated for internal testing while still reaching the internet when needed.

Adapter 1: NAT Network

Adapter 1 was attached to a custom NAT Network named CyberLab. A NAT Network was used instead of a simple NAT adapter because it allows multiple virtual machines connected to the same network to talk to each other, while still routing outbound traffic through the host. This makes it possible to add target machines later and have them communicate with Kali on the same internal segment.



Adapter 3: Bridged Adapter

Adapter 3 was attached in Bridged mode to the host's wireless adapter. This gives the Kali VM its own address on the physical network when a direct connection to the outside world is needed, separate from the internal NAT Network used for lab traffic.



Step 4: Assign a Static IP to Kali Linux

Once the network adapters were in place, Kali's wired connection was set to a manual (static) IPv4 configuration instead of relying on DHCP. This keeps the Kali machine's address predictable, which makes it easier to document the lab and reference the machine in later exercises.

Configuration used:

Address: 10.0.0.2
Netmask: 24
Gateway: 10.0.0.1
DNS: 8.8.8.8



Step 5: Take a Clean Snapshot

After the network was configured and verified, a VirtualBox snapshot was taken to capture this working baseline before any tools were run or any risky testing began.

Verification Tests
Test	Command	Expected Result
Check IP address	ip a	Correct Kali IP (10.0.0.2) shown on the interface
Ping the gateway	ping 10.0.0.1	Successful replies
Ping between VMs	ping <other VM IP>	Successful replies once additional VMs are added
Check internet access	ping 8.8.8.8	Successful replies
Check DNS resolution	nslookup google.com	Domain resolves correctly

Run these checks after any network change to confirm the lab is still working as expected before starting a testing session.






What I Learned This Week
The difference between a plain NAT adapter and a NAT Network in VirtualBox, and why a NAT Network is the better choice for a lab with multiple virtual machines.

How to configure a static IP address in Kali Linux and why a predictable address matters for documentation and future testing.
How bridged and NAT-based adapters differ, and when to use each one.
The value of taking a clean snapshot before making risky changes.
How to verify a network setup properly instead of assuming it works, using ip a, ping, and nslookup.

Security and Ethical Use

This lab is intended strictly for learning and for testing systems you own or have explicit permission to test. It should never be used against systems or networks without authorization.



Project Information

Internship: Cybersecurity Internship Week: Week_1 Project: Cybersecurity Lab Setup Organization: Networkwalks Academy
