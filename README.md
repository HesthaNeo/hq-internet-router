<p align="center">
<img width="791" height="257" alt="Screenshot 2026-02-07 171520" src="https://github.com/user-attachments/assets/220b2130-a504-4326-8ef6-ec513d20357b" />
</p>
<h1><u>Milestone 3: HQ Access Switching</u></h1>
    <p>Second phase, we will install 3 Cisco WS-C2960-24TT layer 2 access switches.</p>
    <h2><strong><u>Configuration Steps</u></strong></h2>
    <p>Step 1: Rack, Mount, and Power On All 3 Switches</p>
    <p>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</p>
    <p>Step 3: Configure VLAN Trunking Protocol (VTP) Client</p>
    <p>Step 4: Configure MGMT VLAN Interface</p>
    <p>Step 5: Configure Default Gateway</p>
    <p>Step 6: Configure Access-List To Protect The Management Plane</p>
    <p>Step 7: Configure Access Ports</p>
    <p>Step 8: Configure and Connect Trunk Ports</p>
    <p>Step 9: Verify Connectivity In The Network</p>
    <h2><strong><u>Implementation</u></strong></h2>
        <h3>Step 1: Rack, Mount, and Power On All 3 Switches</h3>
            <p>- First, we'll add three 2960 switches to the topology by dragging and dropping them into the Headquarters section of the lab. Place them side by side and label them as HQ-ASW1, HQ-ASW2, and HQ-ASW3.</p>
                <img width="849" height="976" alt="Screenshot 2026-02-06 170658" src="https://github.com/user-attachments/assets/7704547b-449d-4bf6-a9e5-b3cb783f1ac2" />
        <h3>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</h3>
            <p>- In this step, we did basic configuration for both of the switches including changing their hostnames, setting their time zones, enabling SSH, setting domain names, adding securiting to console and vty lines for SSH, and creating user profiles with a password the devices</p>
                <img width="867" height="896" alt="Screenshot 2026-02-06 171129" src="https://github.com/user-attachments/assets/3ae0553b-ebfd-4adc-8154-4c4cac1bd1b1" />
                <img width="870" height="905" alt="Screenshot 2026-02-06 171255" src="https://github.com/user-attachments/assets/bfbb60cc-eb80-42e5-96e2-53c630386aa8" />
                <img width="872" height="907" alt="Screenshot 2026-02-06 171401" src="https://github.com/user-attachments/assets/f6f42ebc-d37f-4d1f-becb-f746c8e8955f" />
        <h3>Step 3: Configure VLAN Trunking Protocol (VTP) Client</h3>
            <p>- Next we will configure VTP on these switches to receive and sync all VLAN updates from the vtp server we configured in the first milestone.</p>
                <img width="873" height="618" alt="Screenshot 2026-02-06 172047" src="https://github.com/user-attachments/assets/286483a4-c123-4d64-91e9-1392d67fe7a6" />
                <img width="871" height="616" alt="Screenshot 2026-02-06 172212" src="https://github.com/user-attachments/assets/0239a279-7874-41fe-9cde-7602be6e307d" />
                <img width="871" height="890" alt="Screenshot 2026-02-06 172337" src="https://github.com/user-attachments/assets/92834966-d56d-4f3a-b417-4e1c1a37db5f" />
        <h3>Step 4: Configure MGMT VLAN Interface</h3>
            <p>- Next we will configure the interface for the management VLAN connectivity on all 3 switches for centralized network management.</p>
                <img width="866" height="272" alt="Screenshot 2026-02-06 172923" src="https://github.com/user-attachments/assets/f4bc5bc7-b1c7-406a-99c1-572975935a4d" />
                <img width="871" height="337" alt="Screenshot 2026-02-06 173041" src="https://github.com/user-attachments/assets/92a3c725-654c-48a2-a163-69e590954c51" />
                <img width="871" height="275" alt="Screenshot 2026-02-06 173158" src="https://github.com/user-attachments/assets/cb897151-013a-4724-9fb4-ab388a8a53a2" />
        <h3>Step 5: Configure Default Gateway</h3>
            <p>- In this step, we will configure the default gateway for all 3 switches.</p>
                <img width="867" height="227" alt="Screenshot 2026-02-06 173804" src="https://github.com/user-attachments/assets/7889b8e9-57a4-489e-830c-0666a44a69cd" />
                <img width="868" height="226" alt="Screenshot 2026-02-06 173845" src="https://github.com/user-attachments/assets/f0f17c2b-956e-49ff-b165-c225725d7412" />
                <img width="874" height="225" alt="Screenshot 2026-02-06 173925" src="https://github.com/user-attachments/assets/10c4ef2e-7b14-4da8-8c5c-26a442f6884b" />
        <h3>Step 6: Configure Access-List To Protect The Management Plane</h3>
            <p>- For this step, we will configure an access-list to ensure that only authorized administrators can log into network devices either locally or remotely via SSH.</p>
                <img width="866" height="338" alt="Screenshot 2026-02-06 174735" src="https://github.com/user-attachments/assets/79618d22-e5f1-4501-bcda-477e60cc495f" />
                <img width="870" height="335" alt="Screenshot 2026-02-06 174909" src="https://github.com/user-attachments/assets/1cdb276d-d96b-4453-b06f-f8e5b1d0e1a8" />
                <img width="868" height="339" alt="Screenshot 2026-02-06 175110" src="https://github.com/user-attachments/assets/1a88f976-e08d-4855-9e4f-b80cab455061" />
        <h3>Step 7: Configure Access Ports</h3>
            <p>- Now we will configure all necessary access ports so that the corresponding end devices may connect to their specific vlan. We do this to provide security by segregating the traffic, simplifying network management, and ensuring these end devices only receive data intended for their assigned network segment. We will be configuring fast access ports Fa0/1 - 22 for all 3 switches. </p>
                <img width="872" height="607" alt="Screenshot 2026-02-06 180001" src="https://github.com/user-attachments/assets/6ddf15a6-dd85-4b57-b455-e21dc4cdf042" />
                <img width="869" height="317" alt="Screenshot 2026-02-06 180042" src="https://github.com/user-attachments/assets/b482fd4e-2296-418a-a168-5a5645146501" />
                <img width="871" height="615" alt="Screenshot 2026-02-06 180157" src="https://github.com/user-attachments/assets/c02b2791-b0a5-42dd-97b3-7ff8bd6b4af6" />
                <img width="873" height="349" alt="Screenshot 2026-02-06 180227" src="https://github.com/user-attachments/assets/4dff446f-1601-4267-9cde-dcb661249f1e" />
                <img width="868" height="797" alt="Screenshot 2026-02-06 180327" src="https://github.com/user-attachments/assets/d2db6517-1af0-44dd-97a4-4ee74d4fef8f" />
                <img width="873" height="325" alt="Screenshot 2026-02-06 180400" src="https://github.com/user-attachments/assets/d774149c-9f74-4526-8555-59991272ac5e" />
        <h3>Step 8: Configure and Connect Trunk Ports</h3>
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
        <h3>Step 9: Verify Connectivity In The Network</h3>   
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

















            












 





