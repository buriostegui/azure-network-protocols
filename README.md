<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Steps and Observations</h2>

Setting Up VMs and Wireshark:
- Create two VMs on Azure, one Linux and one Windows 10 machine.
- Ensure both VMs have two CPUs and are on the same Virtual Network (VNET).
- On the Windows machine, download and install Wireshark.
- Use Wireshark to filter and capture only ICMP traffic, which is a network layer protocol used for network connection messages, such as ping tests.

![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/043a4a6a-db7c-47cf-b564-664228abd68e)

Pinging and Blocking ICMP Traffic:
- Continuously ping the Linux machine using the ping -t command from the Windows machine.
- While the pinging is ongoing, block inbound ICMP traffic on the Linux machine's firewall.
- Achieve this by creating a new Network Security Group on the Linux machine to block ICMP. Unblock the traffic by allowing ICMP in the Azure Network Security Groups settings.

![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/83623a00-fa4b-47f0-ac84-7ef6d223f568)
![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/1508f3b5-8f70-44d7-9940-5c2420ece6c4)

Capturing SSH Traffic: 
- Use the Windows machine to SSH into the Linux machine, which provides command-line access.
- Set Wireshark to capture only SSH packets.
- Upon initiating the SSH connection with the command "ssh labuser@10.0.0.5," observe Wireshark capturing SSH packets.

![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/51aa6977-e047-47ab-9bd9-1fdb226df41a)

Filtering DHCP Traffic:
- Configure Wireshark to filter for DHCP traffic.
- Trigger DHCP traffic by running the "ipconfig /renew" command, which requests a new IP address.
- Wireshark captures DHCP traffic related to IP address assignment.

![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/fe35f646-9e24-47f2-aba3-5cefbad66555)

Filtering DNS Traffic:
- Set Wireshark to filter DNS traffic.
- Generate DNS traffic by running the command "nslookup www.google.com," which queries the DNS server for Google's IP address.
- Wireshark captures DNS traffic as the DNS server responds.

![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/9c02821c-addf-46b9-999c-ae105761c4d6)

Filtering RDP Traffic:
- Filter for RDP traffic in Wireshark using the filter "tcp.port==3389."
- Observe continuous traffic as Remote Desktop Protocol (RDP) is used to connect to the Virtual Machine.

![image](https://github.com/buriostegui/azure-network-protocols/assets/148411510/fbd127c4-e23d-44ac-8ca9-d35ce6912b2d)

These steps guide you through exploring and monitoring various network protocols and their traffic using Wireshark within a controlled environment.
