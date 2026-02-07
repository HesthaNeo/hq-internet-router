<p align="center">
<img width="791" height="257" alt="Screenshot 2026-02-07 171520" src="https://github.com/user-attachments/assets/220b2130-a504-4326-8ef6-ec513d20357b" />
</p>
<h1><u>Milestone 4: HQ Internet Router</u></h1>
    <p>Third phase, we will install 1 CISCO2911/K9 with ipbasek9 and securityk9 licensing. This router will act as the gateway for all WAN services that connect Headquarters to Branch 1 and Branch 2. This includes a Private WAN connection to Branch 1 via the WAN service provider using BGP peering. In addition, a second internet service will be connected to this router solely for the purpose of creating an IPSec Site to Site (L2L) Virtual Private Network connection.</p>
    <h2><strong><u>Configuration Steps</u></strong></h2>
    <p>Step 1: Rack, Mount, and Power On The Cisco 2911 Router</p>
    <p>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</p>
    <p>Step 3: Install Securityk9 License</p>
    <p>Step 4: Configure and Connect HQ LAN Interface G0/0</p>
        <p>- A. MGMT Interface VLAN 100</p>
        <p>- B. DATA Interface VLAN 192</p>
    <p>Step 5: Configure and Connect Private WAN Interface G0/1</p>
        <p>- A. IP Address</p>
        <p>- B. Disable CDP</p>
    <p>Step 6: Configure Private WAN Border Gateway Protocol (BGP) Peering</p>
        <p>- A. BGP ASN 65123</p>
            <p>- I. Router ID</p>
            <p>- II. Neighbor</p>
            <p>- III. Networks</p>
    <p>Step 7: Configure Private WAN Voice Quality of Service</p>
        <p>- A. VOIP Control and RTP Access-Lists</p> 
        <p>- B. VOIP Control and RTP Class-Maps</p>
        <p>- C. Policy-Map</p>
        <p>- D. Apply Policy-Map to Private WAN Interface G0/1</p>
    <p>Step 8: Configure IPSec/Isakmp VPN Policy and Cryptography</p>
        <p>- A. Branch 2 Traffic Access List</p>
        <p>- B. Isakmp Policy</p>
        <p>- C. Isakmp Key</p>
        <p>- D. Ipsec SA Lifetime and Transform-Set</p>
        <p>- E. Ipsec-Isakmp Crypto Map</p>
    <p>Step 9: Configure Access-List to Allow Only VPN Traffic From Branch 2</p>
    <p>Step 10: Configure and Connect Internet Interface G0/2</p>
        <p>- A. IP Address</p>
        <p>- B. Disable CDP</p>
        <p>- C. Apply VPN Only Access-List Inbound</p>
        <p>- D. Apply VPN Crypto Map For Branch 2 VPN</p>
    <p>Step 11: Configure Static Routes</p>
        <p>- A. Default Route Pointing to HQ Internet Router DATA Interface IP Address</p>
        <p>- B. Route to HQ Voice Network Pointing to HQ Core Switch Voice Network HSRP Address</p>
        <p>- C. Route to Branch 2 Public IP address via Internet Gateway Public IP</p>
        <p>- D. Routes to Branch 2 Private Networks via Branch 2 Public IP</p>
    <h2><strong><u>Implementation</u></strong></h2>
        <h3>Step 1: Rack, Mount, and Power On The Cisco 2911 Router</h3>
            <p>- First, we'll Add a 2901 Router to the topology by dragging and dropping it into the Headquarters section of the lab. We'll place the 2901 Router in the top right area of HQ and label it as “HQ-INET-RTR”.</p>
                <img width="739" height="970" alt="Screenshot 2026-02-07 173927" src="https://github.com/user-attachments/assets/1ceae563-e79f-4427-930b-e8699e4e4c4e" />
        <h3>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</h3>
            <p>- In this step, we did basic configuration for both of the switches including changing their hostnames, setting their time zones, enabling SSH, setting domain names, adding securiting to console and vty lines for SSH, and creating user profiles with a password thedevices</p>
                <img width="871" height="1002" alt="Screenshot 2026-02-07 174426" src="https://github.com/user-attachments/assets/b17c20ed-f02e-4dc9-8c0d-9b39391efbc5" />
        <h3>Step 3: Install Securityk9 License</h3>
            <p>- Next we will activate the security licensing 60 day grace period on the 2901 Router. We do this to unlock advanced security features, primarily for setting up VPNs (IPsec), secure communication, and enhanced firewall functionality.</p>
                <img width="874" height="939" alt="Screenshot 2026-02-07 180229" src="https://github.com/user-attachments/assets/252fd020-0fd3-470d-a065-6d02df2954ff" />
                <img width="866" height="1158" alt="Screenshot 2026-02-07 180422" src="https://github.com/user-attachments/assets/b1d7090a-d18b-4744-8603-26d0e7dbaeaa" />
            <p><em>- After reloading the router, you can see that the securityk9 licensing software was installed successfully.</em></p>
        <h3>Step 4: Configure and Connect HQ LAN Interface G0/0</h3>
            <p>- Next we will configure the inside LAN interface G0/0 as a trunk for the Management and Data Networks, and connect the interface to the Core switched infrastructure.</p>
                <p>- A: Configure the inside LAN interface.</p>
                <img width="871" height="709" alt="Screenshot 2026-02-07 181525" src="https://github.com/user-attachments/assets/77acffef-9166-4de3-94f9-7fbab0801481" />
            <p><em>- As you can see, we changed the speed of the g0/0 interface to match the interface of the core switch for predictable performance. We also created sub interfaces on the port for both the data vlan and the management vlan for better traffic management.</em></p>
                <p>- B: Connect router interface G0/0 to a switchport using a straight-through cable on HQ-CORE-SW2 that is already configured as a trunk (ie. FastEthernet0/19).</p>
                <img width="747" height="887" alt="Screenshot 2026-02-07 182345" src="https://github.com/user-attachments/assets/f0944b22-198a-409e-a64f-ab28e90992ec" />
        <h3>Step 5: Configure and Connect Private WAN Interface G0/1</h3>
            <p>- In this step, we will configure the default gateway for all 3 switches.</p>
                <img width="867" height="227" alt="Screenshot 2026-02-06 173804" src="https://github.com/user-attachments/assets/7889b8e9-57a4-489e-830c-0666a44a69cd" />
                <img width="868" height="226" alt="Screenshot 2026-02-06 173845" src="https://github.com/user-attachments/assets/f0f17c2b-956e-49ff-b165-c225725d7412" />
                <img width="874" height="225" alt="Screenshot 2026-02-06 173925" src="https://github.com/user-attachments/assets/10c4ef2e-7b14-4da8-8c5c-26a442f6884b" />
        <h3>Step 6: Configure Private WAN Border Gateway Protocol (BGP) Peering</h3>
            <p>- For this step, we will configure an access-list to ensure that only authorized administrators can log into network devices either locally or remotely via SSH.</p>
                <img width="866" height="338" alt="Screenshot 2026-02-06 174735" src="https://github.com/user-attachments/assets/79618d22-e5f1-4501-bcda-477e60cc495f" />
                <img width="870" height="335" alt="Screenshot 2026-02-06 174909" src="https://github.com/user-attachments/assets/1cdb276d-d96b-4453-b06f-f8e5b1d0e1a8" />
                <img width="868" height="339" alt="Screenshot 2026-02-06 175110" src="https://github.com/user-attachments/assets/1a88f976-e08d-4855-9e4f-b80cab455061" />
        <h3>Step 7: Configure Private WAN Voice Quality of Service</h3>
            <p>- Now we will configure all necessary access ports so that the corresponding end devices may connect to their specific vlan. We do this to provide security by segregating the traffic, simplifying network management, and ensuring these end devices only receive data intended for their assigned network segment. We will be configuring fast access ports Fa0/1 - 22 for all 3 switches. </p>
                <img width="872" height="607" alt="Screenshot 2026-02-06 180001" src="https://github.com/user-attachments/assets/6ddf15a6-dd85-4b57-b455-e21dc4cdf042" />
                <img width="869" height="317" alt="Screenshot 2026-02-06 180042" src="https://github.com/user-attachments/assets/b482fd4e-2296-418a-a168-5a5645146501" />
                <img width="871" height="615" alt="Screenshot 2026-02-06 180157" src="https://github.com/user-attachments/assets/c02b2791-b0a5-42dd-97b3-7ff8bd6b4af6" />
                <img width="873" height="349" alt="Screenshot 2026-02-06 180227" src="https://github.com/user-attachments/assets/4dff446f-1601-4267-9cde-dcb661249f1e" />
                <img width="868" height="797" alt="Screenshot 2026-02-06 180327" src="https://github.com/user-attachments/assets/d2db6517-1af0-44dd-97a4-4ee74d4fef8f" />
                <img width="873" height="325" alt="Screenshot 2026-02-06 180400" src="https://github.com/user-attachments/assets/d774149c-9f74-4526-8555-59991272ac5e" />
        <h3>Step 8: Configure IPSec/Isakmp VPN Policy and Cryptography</h3>
            <p>- For this next step, we will configure interfaces fa0/23-24 as our trunk ports, while also administratively shutting down our gig ports for added security.</p>
                <img width="867" height="386" alt="Screenshot 2026-02-06 181415" src="https://github.com/user-attachments/assets/5cc841fe-bd6e-40cb-a1cc-1cb2cd8952f8" />
                <img width="868" height="387" alt="Screenshot 2026-02-06 181548" src="https://github.com/user-attachments/assets/b64da8dd-b3d7-4cbf-8c24-d53e40269be8" />
                <img width="870" height="381" alt="Screenshot 2026-02-06 181705" src="https://github.com/user-attachments/assets/0f8dd081-9bb0-4669-8d3e-244d0e3e4b16" />
            <p>- A. We will now connect each access switch trunk port to the core switches using ethernet crossover cables.</p>
            <p><em>- We will connect ASW 1-3 ports Fa0/23 to trunk port fa0/19, fa0/20, and fa0/21 on CORE-SW1.</em></p>
            <p><em>- We will connect ASW 1-3 ports Fa0/24 to trunk port fa0/19, fa0/20, and fa0/21 on CORE-SW2.</em></p>
                <img width="734" height="863" alt="Screenshot 2026-02-06 183510" src="https://github.com/user-attachments/assets/e8f4ceeb-dd2a-48b6-80af-976ac2016021" />
            <p>- B. Now we will verify the VLAN database to ensure all VLANs were copied over from the VTP Servers to the VTP Clients (I.e. from core switches to access switches).</p>
                <img width="871" height="588" alt="Screenshot 2026-02-07 161651" src="https://github.com/user-attachments/assets/35a4eabe-3543-4ce5-8c21-02abfdd5b8b2" />
                <img width="869" height="526" alt="Screenshot 2026-02-07 161746" src="https://github.com/user-attachments/assets/d60e1916-9caa-43dd-bbd8-5017a862837b" />
                <img width="871" height="530" alt="Screenshot 2026-02-07 161828" src="https://github.com/user-attachments/assets/10589e89-a61f-4bb0-b4dd-1d741ac01eaf" />
             <p><em>- As you can see, all of our vlans were successfully transferred over from our core switches to the access switches using VTP protocol.</em></p>
        <h3>Step 9: Configure Access-List to Allow Only VPN Traffic From Branch 2</h3>   
            <p>- For the final step in this second milestone, we will now connect a new Test PC to the Data VLAN for testing network access via the Access Switches.</p>
            <p>- A. We will Drag and drop a PC into the topology and label it as “ASW-Test-PC.</p>
                <img width="848" height="971" alt="Screenshot 2026-02-07 164138" src="https://github.com/user-attachments/assets/55d790db-750e-4fed-b6f2-242d38b1321b" />
            <p>- B. Next we'll connect a straight-through from the PC FastEthernet0 to an Access Port on HQ-ASW1.</p>
                <img width="762" height="880" alt="Screenshot 2026-02-07 164435" src="https://github.com/user-attachments/assets/37ffda36-08c7-45d4-a0e2-ed146ba43b07" />
            <p>- C. Now we'll click on the PC to configure a static IP address, subnet mask, and default gateway. Our IP address for this Test PC will be 192.168.10.151 255.255.255.0 with a default gateway of 192.168.10.100.</p>
                <img width="870" height="884" alt="Screenshot 2026-02-07 164807" src="https://github.com/user-attachments/assets/0e91fbeb-993d-4804-811d-c0a8a08220d3" />
                <img width="867" height="887" alt="Screenshot 2026-02-07 164844" src="https://github.com/user-attachments/assets/815ebfbf-4859-4ee0-a1a7-8a0ae616d3ac" />
            <p>- D. Now we can access the command prompt of the ASW-Test-PC to test connectivity to various IPs.</p>
                <img width="2557" height="1599" alt="Screenshot 2026-02-07 165312" src="https://github.com/user-attachments/assets/affc40cd-8a5c-4162-8670-b8bd41363f5c" />
            <p><em>- As you can see, we were able to successfully ping our default gateway (192.168.10.100), the Test-PC connected to our core switches (192.168.10.150), the NOC-PC (192.168.110.50), and all 3 of our access switches (192.168.110.241-3) after ARP finished resolving.</em></p>
            <p>- E. Now from the command prompt of the ASW-Test-PC we'll verify management plane ssh access to the access switches is restricted.</p>
                <img width="875" height="269" alt="Screenshot 2026-02-07 165953" src="https://github.com/user-attachments/assets/eb771257-9913-434e-b375-41069453b493" />
            <p><em>- As you can see, we are unable to remotely access the management plane of our network, due to the access control lists we configured earlier in the network configuration. Our access list is deny any other IP address that aren't explicitly stated in the configuration, showing that this was successful.</em></p>
            <p>- F. Now using the NOC-PC, lets verify successful management plane access via ssh to the access switches from the management network.</p>
                <img width="871" height="1017" alt="Screenshot 2026-02-07 170701" src="https://github.com/user-attachments/assets/681e4b22-3f65-4ab5-b612-21ad63e06eb8" />
            <p><em>- We were able to connect successfully to the management plane of the newly installed access switches.</em></p>
         <h3>Step 10: Configure and Connect Internet Interface G0/2</h3>\
         <h3>Step 11: Configure Static Routes</h3>

















            












 





