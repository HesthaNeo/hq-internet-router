<p align="center">
<img width="791" height="257" alt="Screenshot 2026-02-07 171520" src="https://github.com/user-attachments/assets/220b2130-a504-4326-8ef6-ec513d20357b" />
</p>
<h1><u>Milestone 4: HQ Internet Router</u></h1>
    <p>Third phase, we will install 1 CISCO2911/K9 with ipbasek9 and securityk9 licensing. This router will act as the gateway for all WAN services that connect Headquarters to Branch 1 and Branch 2. This includes a Private WAN connection to Branch 1 via the WAN service provider using BGP peering. In addition, a second internet service will be connected to this router solely for the purpose of creating an IPSec Site to Site (L2L) Virtual Private Network connection.</p>
    <h2><strong><u>Configuration Steps</u></strong></h2>
    <p>Step 1: Rack, Mount, and Power On The Cisco 2911 Router</p>
    <p>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</p>
    <p>Step 3: Install Securityk9 License</p>
    <p>Step 4: Configure Inbound Internet Access-List</p>
    <p>Step 5: Configure NAT</p>
        <p>- A. NAT Inside Access-List</p>
        <p>- B. NAT Overload</p>
    <p>Step 6: Configure IOS Firewall Inspection Rules</p>
    <p>Step 7: Configure and Connect Inside LAN Interface G0/0</p>
        <p>- A. MGMT Interface VLAN 100</p> 
        <p>- B. DATA Interface VLAN 192</p>
            <p>- i. NAT Inside</p>
    <p>Step 8: Configure and Connect Outside Internet Interface G0/1</p>
        <p>- A. IP Address</p>
        <p>- B. Disable CDP</p>
        <p>- C. Apply Inbound Access-List</p>
        <p>- D. Apply IOS Firewall Outbound</p>
        <p>- E. NAT Outside</p>
    <p>Step 9: Configure Static Routes</p>
        <p>- A. Default Route Pointing to Internet Gateway Public IP</p>
        <p>- B. Routes to Branch 1 Networks and Branch 2 Networks Pointing to HQ WAN Router IP Address</p>
        <p>- C. Route to Guest Network Pointing to HQ Core Switch Data Network HSRP Address</p>
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
        <h3>Step 4: Configure Inbound Internet Access-List</h3>
            <p>- Next we will configure an access control list that will be applied to protect the internet facing interface.</p>
                <img width="866" height="261" alt="Screenshot 2026-02-07 185411" src="https://github.com/user-attachments/assets/a4186eb3-0afb-42f2-b84a-a27f474a7b4e" />
        <h3>Step 5: Configure NAT</h3>
            <p>- Next we will configure an access control list for translating all data and management networks, and also the HQ guest network.</p>
                <img width="868" height="272" alt="Screenshot 2026-02-07 185904" src="https://github.com/user-attachments/assets/ea041f79-6b51-4cc8-967f-cd8b1b539e63" />
            <p>- Next we will configure NAT for "INSIDE" ACL with Overload to interface G0/1.</p>
                <img width="872" height="179" alt="Screenshot 2026-02-07 190203" src="https://github.com/user-attachments/assets/ef5afac0-4946-44e9-a52e-97e71c00a86e" />
            <p><em>- We use the overload command to allow devices in our private internal network to access the internet simultaneously using a single public IP address assigned to our router's g0/1 OUTSIDE interface.</em></p>
        <h3>Step 6: Configure IOS Firewall Inspection Rules</h3>
            <p>- Next we will configure IOS firewall inspection rules for allowed internet traffic.</p>
                <img width="872" height="307" alt="Screenshot 2026-02-08 124931" src="https://github.com/user-attachments/assets/87eb1138-ead1-4908-ab09-9cb65c99f21e" />
            <p><em>- We do this to enable stateful packect inspection allowing authorized outgoing traffic while automatically opening temporary, secure return paths for legitimate replies. This prevents unauthorized incoming traffic (hackers) while allowing internal users to access internet services as expected. Unlike standard Access Control Lists (ACLs) that require manual rules for both directions, the command "inspect" remembers outgoing requests and allows only the matching return packets back in. It verifies that incoming traffic is actually a reply to a request made from inside, rather than unsolicited malicious traffic. It understands and monitors application-layer details for TCP, UDP, ICMP, and HTTP, ensuring the session follows correct protocol behavior. It dynamically creates temporary openings in the firewall for allowed sessions, closing them immediately when the conversation ends.</em></p>
        <h3>Step 7: Configure and Connect Inside LAN Interface G0/0</h3>
            <p>- Next we will configure the inside LAN interface G0/0 as a trunk for the Management and Data Networks, and connect the interface to the Core switched infrastructure.</p>
                <p>- A: Configure the inside LAN interface.</p>
                <img width="871" height="709" alt="Screenshot 2026-02-07 181525" src="https://github.com/user-attachments/assets/77acffef-9166-4de3-94f9-7fbab0801481" />
            <p><em>- As you can see, we changed the speed of the g0/0 interface to match the interface of the core switch for predictable performance. We also created sub interfaces on the port for both the data vlan and the management vlan for better traffic management.</em></p>
                <p>- B: Connect router interface G0/0 to a switchport using a straight-through cable on HQ-CORE-SW2 that is already configured as a trunk (ie. FastEthernet0/19).</p>
                <img width="747" height="887" alt="Screenshot 2026-02-07 182345" src="https://github.com/user-attachments/assets/f0944b22-198a-409e-a64f-ab28e90992ec" />
                <img width="869" height="709" alt="Screenshot 2026-02-07 182703" src="https://github.com/user-attachments/assets/ca12f94f-bde6-4f7c-847a-2059ac43cfed" />
            <p><em>- Successful pings, showing we are able to establish connectivity to both the MGMT and DATA networks.</em></p>
        <h3>Step 8: Configure and Connect Outside Internet Interface G0/1</h3>
            <p>- In this step, we will configure the default gateway for all 3 switches.</p>
                <img width="867" height="227" alt="Screenshot 2026-02-06 173804" src="https://github.com/user-attachments/assets/7889b8e9-57a4-489e-830c-0666a44a69cd" />
                <img width="868" height="226" alt="Screenshot 2026-02-06 173845" src="https://github.com/user-attachments/assets/f0f17c2b-956e-49ff-b165-c225725d7412" />
                <img width="874" height="225" alt="Screenshot 2026-02-06 173925" src="https://github.com/user-attachments/assets/10c4ef2e-7b14-4da8-8c5c-26a442f6884b" />
        <h3>Step 9: Configure Static Routes</h3>
            <p>- For this step, we will configure an access-list to ensure that only authorized administrators can log into network devices either locally or remotely via SSH.</p>
                <img width="866" height="338" alt="Screenshot 2026-02-06 174735" src="https://github.com/user-attachments/assets/79618d22-e5f1-4501-bcda-477e60cc495f" />
                <img width="870" height="335" alt="Screenshot 2026-02-06 174909" src="https://github.com/user-attachments/assets/1cdb276d-d96b-4453-b06f-f8e5b1d0e1a8" />
                <img width="868" height="339" alt="Screenshot 2026-02-06 175110" src="https://github.com/user-attachments/assets/1a88f976-e08d-4855-9e4f-b80cab455061" />

















            












 





