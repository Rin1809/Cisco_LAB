# Cisco Lab Configurations and Network Designs ᓚᘏᗢ

<details>
  <summary>Cisco Security Project (CCNA).pkt - Detailed Configuration Breakdown</summary>

# ANALYSIS - DESIGN AND IMPLEMENTATION

This section outlines the objectives and design considerations for the ABC Company network project.

## 3.1. Objectives:

ABC Company has 7 departments requiring a robust and secure network infrastructure: Director's Office, Server Room, and Employee Offices from Floor 1 to Floor 4.

**ABC Company's Network Requirements:**

This section details the specific functional and security requirements that the network design must address.

*   **Wireless Connectivity:**  Providing Wi-Fi access across all departments is a primary requirement.

    *   **WPA2-PSK Security:** Implement the WPA2 Pre-Shared Key (PSK) protocol for Wi-Fi network security in all departments.  This is a standard and widely used security protocol for Wi-Fi networks, providing encryption and authentication.
    *   **MAC Filtering for Director's Office:** Implement MAC address filtering on the Wireless Router in the Director's Office to restrict network access to only authorized devices. This adds a layer of access control based on device MAC addresses in the Director's Office for enhanced security.
    *   **RADIUS Server for Centralized Wi-Fi Authentication:** Configure a RADIUS (Remote Authentication Dial-In User Service) server for centralized Wi-Fi user authentication and access control. This system should authenticate users based on individual accounts and allow for role-based access control, particularly for the Director's Office, which requires special privileges. RADIUS provides a centralized authentication mechanism for Wi-Fi users, improving security and management.

*   **Wired Connectivity:**  Segmenting the wired network is crucial for security and management.

    *   **VLAN Segmentation by Department:**  Utilize VLANs (Virtual LANs) to segment the network by department. This enhances security by isolating network traffic within each department, improving network performance, and simplifying access management. VLAN segmentation is key for network security and management.

*   **Redundancy and Stability:** Ensuring network uptime and resilience is critical for business operations.

    *   **HSRP for Router Redundancy:** Configure HSRP (Hot Standby Router Protocol) on the Core Routers (Core-Server & Core2-Server). HSRP provides router redundancy, ensuring high availability for internet access by automatically failing over to a standby router in case of primary router failure. HSRP ensures router redundancy for high availability.
    *   **EtherChannel for Link Aggregation:** Implement EtherChannel to aggregate multiple physical links between critical network devices (like Core Switches). EtherChannel increases bandwidth by combining links and provides link redundancy, ensuring network stability and higher throughput for critical connections. EtherChannel enhances bandwidth and link redundancy.

*   **Scalability:** The network design must be adaptable to future growth and expansion.

    *   **Flexible Network Model:** Design a network model that is easily scalable to accommodate additional devices, users, and departments in the future without significant redesign or disruption. Scalability is essential for future network growth.

*   **Objective:** The overarching objective is to build a secure, stable, and efficient LAN system for ABC Company.

    *   **Secure, Stable, and Efficient LAN:** The primary objective is to create a LAN that meets the internal connectivity and data sharing needs of ABC Company employees while ensuring security, stability, and efficient network operation. The network should be secure, stable, and efficient.

## 3.2. IP Addressing Plan:

This section outlines the IP addressing scheme used for the network devices and VLANs.  A well-planned IP addressing scheme is crucial for network organization and routing.

| Device Name     | Interface | IP Address          | Connected Devices                                  | Note                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-----------------|-----------|---------------------|----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Core-Server     | Fa0/1-8   | 192.168.99.3/24     | sw-web-dns, sw-giamdoc, sw-tang1, sw-tang4          | **Core Router (Active HSRP):** Serving as the Active HSRP router for VLANs 10, 20, 30, 40, 50, and 99.  Handles inter-VLAN routing and provides DHCP server functionality for these VLANs. Configured for trunking VLANs and using VLAN 99 as the native VLAN.                                                                                                                                                                                                       |
|                 |           | 192.168.10.3/24     |                                                    | **VLAN 10 Interface:** IP address for VLAN 10 (Floor 1 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.20.3/24     |                                                    | **VLAN 20 Interface:** IP address for VLAN 20 (Floor 2 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.30.3/24     |                                                    | **VLAN 30 Interface:** IP address for VLAN 30 (Floor 3 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.40.3/24     |                                                    | **VLAN 40 Interface:** IP address for VLAN 40 (Floor 4 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.50.3/24     |                                                    | **VLAN 50 Interface:** IP address for VLAN 50 (Server Room Network).                                                                                                                                                                                                                                                                                                                                                                                                              |
|                 |           | 192.168.99.3/24     |                                                    | **VLAN 99 Interface:** IP address for VLAN 99 (Management Network).                                                                                                                                                                                                                                                                                                                                                                                                             |
| Core2-Server    | Fa0/1-9   | 192.168.99.2/24     | Sw-giamdoc, sw-quanly, sw-tang1, sw-tang4         | **Core Router (Standby HSRP):** Serving as the Standby HSRP router for VLANs 10, 20, 30, 40, 50, and 99.  Configured for trunking VLANs and using VLAN 99 as the native VLAN. Will take over routing duties if Core-Server fails.                                                                                                                                                                                                                                                           |
|                 |           | 192.168.10.2/24     |                                                    | **VLAN 10 Interface:** IP address for VLAN 10 (Floor 1 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.20.2/24     |                                                    | **VLAN 20 Interface:** IP address for VLAN 20 (Floor 2 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.30.2/24     |                                                    | **VLAN 30 Interface:** IP address for VLAN 30 (Floor 3 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.40.2/24     |                                                    | **VLAN 40 Interface:** IP address for VLAN 40 (Floor 4 Network).                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                 |           | 192.168.50.2/24     |                                                    | **VLAN 50 Interface:** IP address for VLAN 50 (Server Room Network).                                                                                                                                                                                                                                                                                                                                                                                                              |
|                 |           | 192.168.50.2/24     |                                                    | **VLAN 99 Interface:** IP address for VLAN 99 (Management Network).                                                                                                                                                                                                                                                                                                                                                                                                             |
| Sw-web-dns      | Fa0/1-5   | 192.168.99.50/24    | Core-server, TFTP server, DNS server, WEB server   | **Distribution Switch (Server Room):** Connects servers and core routers. Configured for trunking VLANs.  Fa0/3-5 are configured as access ports in VLAN 50.                                                                                                                                                                                                                                                                                                                       |
|                 | Fa0/3-5   |  Access VLAN 50     |                                                    | **Access Ports VLAN 50:**  Fa0/3, Fa0/4, and Fa0/5 are configured as access ports assigned to VLAN 50 (Server Room Network) for server connections.                                                                                                                                                                                                                                                                                                                            |
| Sw-giamdoc      | Fa0/1-5   | 192.168.99.60/24    | Wireless Router GiamDoc, Core-Server, Core2-Server | **Distribution Switch (Director's Office):** Connects Director's Office devices and core routers. Configured for trunking VLANs.                                                                                                                                                                                                                                                                                                                                         |
| Sw-quanly       | Fa0/1-3   | 192.168.99.100/24   | Core2-Server, Quan ly (WLC)                        | **Distribution Switch (Management):** Connects management devices and core routers. Configured for trunking VLANs. Fa0/1 is configured as an access port in VLAN 99.                                                                                                                                                                                                                                                                                                                      |
|                 | Fa0/1     | Access VLAN 99      | (VLAN 99 - Management)                            | **Access Port VLAN 99:** Fa0/1 is configured as an access port assigned to VLAN 99 (Management Network) for connecting management devices like the WLC and RADIUS server.                                                                                                                                                                                                                                                                                                           |
| Sw-tang1        | Fa0/1-8   | 192.168.99.10/24    | Core-Server, Core2-Server, sw-tang4, sw-tang2, wifi tang1 | **Access Switch (Floor 1):** Connects Floor 1 devices and distribution switches. Configured for trunking VLANs and using VLAN 99 as the native VLAN.                                                                                                                                                                                                                                                                                                                          |
| Sw-tang2        | Fa0/1-5   | 192.168.99.20/24    | Sw-tang1, sw-tang3, wifi tang2                    | **Access Switch (Floor 2):** Connects Floor 2 devices and access switches on Floor 1 and 3. Configured for trunking VLANs and using VLAN 99 as the native VLAN.                                                                                                                                                                                                                                                                                                                          |
| Sw-tang3        | Fa0/1-5   | 192.168.99.30/24    | Sw-tang2, Sw-tang4, wifi tang3                    | **Access Switch (Floor 3):** Connects Floor 3 devices and access switches on Floor 2 and 4. Configured for trunking VLANs and using VLAN 99 as the native VLAN.                                                                                                                                                                                                                                                                                                                          |
| Sw-tang4        | Fa0/1-9   | 192.168.99.40/24    | Sw-tang3, Core2-Server, Core-server, sw-tang1, wifi tang4 | **Access Switch (Floor 4):** Connects Floor 4 devices and access switches on Floor 3 and 1, and core routers. Configured for trunking VLANs and using VLAN 99 as the native VLAN.                                                                                                                                                                                                                                                                                           |
| Web server      | Fa0/5     | 192.168.50.2/24     | sw-web-dns                                         | **Web Server (DMZ - VLAN 50):** Public-facing web server hosted in the DMZ zone (VLAN 50).                                                                                                                                                                                                                                                                                                                                                                                         |
| TFTP Server     | Fa0/3     | 192.168.50.5/24     | sw-web-dns                                         | **TFTP Server (VLAN 50):** TFTP server for configuration backup and device management, located in the Server Room (VLAN 50).                                                                                                                                                                                                                                                                                                                                                       |
| DNS server      | Fa0/4     | 192.168.50.1/24     | sw-web-dns                                         | **DNS Server (VLAN 50):** Internal DNS server for the network, located in the Server Room (VLAN 50).                                                                                                                                                                                                                                                                                                                                                                                    |
| RADIUS server   | Fa0/1     | 192.168.99.10/24    | Quan ly (WLC)                                      | **RADIUS Server (VLAN 99):** RADIUS server for centralized Wi-Fi authentication, located in the Management Network (VLAN 99).                                                                                                                                                                                                                                                                                                                                                       |
| Quanly (WLC)    | G/1       | 192.168.99.200/24   | Core2-Server, RADIUS server, PC_Quanly             | **Wireless LAN Controller (WLC - VLAN 99):** Wireless LAN Controller for managing Access Points, located in the Management Network (VLAN 99).                                                                                                                                                                                                                                                                                                                                        |
| WR Giam Doc     | 0/0       | 192.168.99.9/24     | Sw-giamdoc                                         | **Wireless Router (Director's Office - VLAN 60):** Wireless Router for Director's Office, distributing VLAN 60 for wireless clients in the Director's Office.                                                                                                                                                                                                                                                                                                                           |
| AP tang1 - 4    |           | DHCP                | Sw-tang1 -> tang4                                  | **Access Points (Floors 1-4):** Access Points for each floor, providing Wi-Fi access to clients on each floor.  They obtain IP addresses via DHCP and are connected to the corresponding floor switches.                                                                                                                                                                                                                                                                              |

**(Explanation of IP Addressing Plan Table):**

This table provides a detailed overview of the IP addressing scheme for each device and interface in the network. It clearly outlines:

*   **Device Name:** The name of each network device (Routers, Switches, Servers, Wireless Router, Access Points).
*   **Interface:** The specific interface on the device being configured (e.g., Fa0/1, VLAN 10, G/1, 0/0).
*   **IP Address:** The assigned IPv4 address and subnet mask for the interface.  "DHCP" indicates that the interface obtains its IP address dynamically via DHCP.
*   **Connected Devices:** Lists the devices directly connected to the specified interface, indicating network topology.
*   **Note:** Provides additional information and context for each device and interface, including its role, VLAN assignment, and specific configurations like HSRP, Trunking, or Access VLAN.

This table is essential for understanding the network's IP addressing architecture, VLAN assignments, and device roles within the network.

## 3.3. Diagram:

![image](https://github.com/user-attachments/assets/cdbd3e4b-6d1f-4ee6-9bca-18710c01608a)

**(Explanation of Network Diagram):**

The network diagram visually represents the physical and logical topology of the ABC Company network, complementing the IP Addressing Plan table. Key elements of the diagram are:

*   **Network Segmentation:**  The diagram clearly depicts the VLAN segmentation, with different VLANs (VLAN 10, 20, 30, 40, 50, 60, 99) represented by distinct color-coded segments, highlighting the logical separation of departments and network functions.
*   **Device Placement:** Devices are placed within their respective VLAN segments (Floor 1-4 switches in VLANs 10-40, Server Room devices in VLAN 50, Director's Office Wireless Router in VLAN 60, Management devices in VLAN 99), visually representing the physical location and logical network assignment of each device.
*   **Interconnections:** Lines and labels clearly show the physical connections between devices, indicating the network cabling and link aggregation (EtherChannel) between Core Routers and Distribution Switches.
*   **IP Addressing:** IP addresses for key interfaces (Core Routers VLAN interfaces, Server IPs, WLC IP, Wireless Router IP) are labeled on the diagram, linking the visual representation to the detailed IP Addressing Plan.
*   **Redundancy:** The HSRP configuration is visually represented with two Core Routers connected, indicating the redundancy implemented for core routing functions.

The diagram, combined with the IP Addressing Plan, provides a comprehensive visual and tabular representation of the network design.

## 3.4. Device Configuration:

This section provides the Cisco IOS commands used to configure the network devices, including routers and switches, to implement the designed network architecture and functionalities.

### 3.4.1. Hostname - VTY - Console Configuration:

These basic commands are used to set the hostname for easy device identification and configure secure access methods (local login and SSH) for management.

```
Router>en
Router>enable
Router#configure terminal
Router(config)#hostname core-server
core-server(config)#line vty 0 4
core-server(config-line)#login local
core-server(config-line)#exit
```

**(Explanation of Hostname and Access Configuration Commands):**

*   `Router>en` / `Router>enable`: Enters privileged EXEC mode, required for configuration commands.
*   `Router#configure terminal`: Enters global configuration mode, allowing for system-wide configuration changes.
*   `Router(config)#hostname core-server`: Sets the hostname of the router to "core-server". This command is used to change the device's hostname for easier identification in network management and configuration.
*   `core-server(config)#line vty 0 4`: Enters line configuration mode for VTY (Virtual TeleType) lines 0 through 4. VTY lines are used for remote access to the device via Telnet or SSH.
*   `core-server(config-line)#login local`: Configures VTY lines to require local username/password authentication. This means that users attempting to access the device remotely via VTY (e.g., Telnet or SSH) must authenticate using usernames and passwords configured locally on the device.
*   `core-server(config-line)#exit`: Exits line configuration mode and returns to global configuration mode.

**(Rationale):**

*   **Hostname:** Setting a hostname is best practice for device identification and management.
*   **`login local`:** Configuring `login local` on VTY lines enforces local authentication, requiring users to have valid local accounts on the device for remote access, enhancing security.
*   **Console Configuration (Implicit):** While not explicitly shown, console port configuration (similar to VTY) is also typically configured for local access and initial device setup.

**Configuration for other devices is similar.**  The same basic hostname and VTY configuration commands are applied to other network devices (Core2-Server, Switches) for consistent management access and identification.

### 3.4.2. Trunking and Native VLAN Configuration for Devices:

These commands configure trunk ports on switches to carry traffic for multiple VLANs and set the native VLAN for trunk links. Trunking is essential for VLAN segmentation across switches.

1.  **Core-server & Core2-server:**
    ```
    core-server(config)#interface range fa0/1-8
    core-server(config-if-range)#switchport trunk encapsulation dot1q
    core-server(config-if-range)#switchport trunk native vlan 99
    core-server(config-if-range)#switchport mode trunk
    ```

**(Explanation of Trunking Configuration for Core Routers):**

*   `core-server(config)#interface range fa0/1-8`: Enters interface range configuration mode for interfaces FastEthernet 0/1 through FastEthernet 0/8. This command is used to apply trunking configuration to multiple interfaces simultaneously.
*   `core-server(config-if-range)#switchport trunk encapsulation dot1q`: Configures trunking encapsulation to 802.1Q (dot1q), which is the standard encapsulation protocol for VLAN trunking in Ethernet networks. 802.1Q adds VLAN tags to Ethernet frames to identify VLAN membership.
*   `core-server(config-if-range)#switchport trunk native vlan 99`: Sets the native VLAN for the trunk link to VLAN 99. Native VLAN is used for untagged traffic on the trunk link. In this design, VLAN 99 is used as the management VLAN, and setting it as the native VLAN allows management traffic to be transmitted untagged on the trunk.
*   `core-server(config-if-range)#switchport mode trunk`: Configures the interfaces in the range as trunk ports. Trunk ports are used to carry traffic for multiple VLANs between switches and routers.

**(Rationale):**

*   **Trunking:** Configuring interfaces Fa0/1-8 as trunk ports on Core-Server and Core2-Server enables these routers to carry traffic for all VLANs (VLANs 10, 20, 30, 40, 50, 60, 99) across these interfaces, facilitating inter-VLAN routing and network segmentation. Trunking is essential for VLAN intercommunication.
*   **Native VLAN 99:** Setting VLAN 99 as the native VLAN is a common practice when using VLAN 99 for management. It allows management traffic (e.g., VTP, CDP, and potentially management VLAN traffic) to be transmitted untagged on the trunk, simplifying management VLAN configuration. Native VLAN 99 is used for management traffic.

2.  **Sw-tang1 - tang2 - tang3 - tang4 - giamdoc - quanly:**
    ```
    sw-tang1(config)#interface range fa0/1-9
    sw-tang1(config-if-range)#switchport trunk native vlan 99
    sw-tang1(config-if-range)#switchport mode trunk
    ```

**(Explanation of Trunking Configuration for Distribution and Access Switches):**

*   `sw-tang1(config)#interface range fa0/1-9`: Enters interface range configuration mode for interfaces FastEthernet 0/1 through FastEthernet 0/9 on switch Sw-tang1.  Similar range configuration is applied to other switches.
*   `sw-tang1(config-if-range)#switchport trunk native vlan 99`: Sets the native VLAN for the trunk links on these switches to VLAN 99, consistent with the Core Routers. Native VLAN 99 is consistently used for management.
*   `sw-tang1(config-if-range)#switchport mode trunk`: Configures the interfaces in the range as trunk ports. This enables these switches to carry traffic for multiple VLANs to connect access layer switches and distribution switches.

**(Rationale):**

*   **Trunking:** Configuring interfaces Fa0/1-9 as trunk ports on these switches enables them to carry traffic for all VLANs defined in the network, allowing for VLAN segmentation to be extended across the entire switched network infrastructure. Trunking enables VLAN extension across switches.
*   **Native VLAN 99:** Consistently using VLAN 99 as the native VLAN across all trunk links simplifies management VLAN configuration and ensures consistent handling of untagged traffic across the network. Native VLAN 99 consistency is maintained across switches.

### 3.4.3. VTP Configuration:

These commands configure VTP (VLAN Trunking Protocol) on the switches to enable centralized VLAN management. VTP simplifies VLAN management across multiple switches.

1.  **Core-server & Core2-server:**
    ```
    core-server(config)#vtp domain ado
    core-server(config)#vtp mode server
    ```
    ![image](https://github.com/user-attachments/assets/b1f59ee8-43e6-4a74-a85e-9498e12957fa)
    **(Password configuration is omitted as this is for individual practice).**

**(Explanation of VTP Server Mode Configuration for Core Routers):**

*   `core-server(config)#vtp domain ado`: Sets the VTP domain name to "ado". All switches in the same VTP domain share VLAN information.
*   `core-server(config)#vtp mode server`: Configures Core-Server and Core2-Server as VTP servers. VTP servers are responsible for creating, modifying, and deleting VLANs within the VTP domain. VLAN changes are propagated from VTP servers to VTP clients.

**(Rationale):**

*   **VTP Server Mode:** Configuring Core-Server and Core2-Server as VTP servers designates them as the central VLAN management points for the network. Any VLAN configuration changes made on these core routers (VTP servers) will be automatically propagated to other switches in the VTP domain (VTP clients). VTP server mode centralizes VLAN management.
*   **VTP Domain "ado":**  Setting the VTP domain name to "ado" ensures that all switches configured with the same domain name will participate in the same VTP domain and share VLAN information. VTP domain ensures VLAN information sharing within the domain.

2.  **Other Switches:**
    ```
    sw-tang1(config)#vtp domain ado
    sw-tang1(config)#vtp mode client
    ```
    ![image](https://github.com/user-attachments/assets/6d1dc44d-c436-4d03-839f-d426d50c5ce9)
    **(Password configuration is omitted as this is for individual practice).**

**(Explanation of VTP Client Mode Configuration for Distribution and Access Switches):**

*   `sw-tang1(config)#vtp domain ado`: Sets the VTP domain name to "ado", matching the VTP servers.
*   `sw-tang1(config)#vtp mode client`: Configures Sw-tang1, Sw-tang2, Sw-tang3, Sw-tang4, Sw-giamdoc, and Sw-quanly as VTP clients. VTP clients receive VLAN information from VTP servers and automatically learn VLAN configurations. VTP client mode simplifies VLAN configuration on access switches.

**(Rationale):**

*   **VTP Client Mode:** Configuring distribution and access layer switches as VTP clients simplifies VLAN management on these switches. VTP clients automatically learn VLAN configurations from the VTP servers (Core-Server and Core2-Server), eliminating the need to manually configure VLANs on each client switch. VTP client mode automates VLAN learning on client switches.
*   **VTP Domain "ado":**  Ensures that these switches participate in the same VTP domain as the Core Routers, enabling them to receive VLAN information from the Core Routers (VTP servers). VTP domain consistency ensures proper VLAN information propagation.

### 3.4.4. VLAN Configuration:

These commands create VLANs on the Core Routers (VTP servers). VLAN creation on VTP servers propagates VLAN information to VTP clients.

1.  **Core-Server & Core2-Server:**
    ```
    core-server(config)#vlan 10
    core-server(config-vlan)#name tang1
    core-server(config-vlan)#vlan 20
    core-server(config-vlan)#name tang2
    core-server(config-vlan)#vlan 30
    core-server(config-vlan)#name tang3
    core-server(config-vlan)#vlan 40
    core-server(config-vlan)#name tang4
    core-server(config-vlan)#vlan 50
    core-server(config-vlan)#name server
    core-server(config-vlan)#vlan 60
    core-server(config-vlan)#name giamdoc
    core-server(config-vlan)#vlan 99
    core-server(config-vlan)#name quanly
    ```
    ![image](https://github.com/user-attachments/assets/2f2e475a-f6e6-48ac-9c84-3ebf300171b1)

**(Explanation of VLAN Creation Commands on Core Routers):**

*   `core-server(config)#vlan 10`: Creates VLAN 10.  VLAN command creates a new VLAN.
*   `core-server(config-vlan)#name tang1`: Assigns the name "tang1" (Floor 1) to VLAN 10. VLAN name command assigns a descriptive name to the VLAN.
*   **(Repeat for VLANs 20, 30, 40, 50, 60, 99):**  Similar `vlan` and `name` commands are used to create and name VLANs 20 (tang2 - Floor 2), 30 (tang3 - Floor 3), 40 (tang4 - Floor 4), 50 (server - Server Room), 60 (giamdoc - Director's Office), and 99 (quanly - Management). VLANs are created and named according to department/function.

**(Rationale):**

*   **VLAN Creation on VTP Servers:** VLANs are created on the Core Routers (VTP servers) because they are configured in VTP server mode. Creating VLANs on VTP servers automatically propagates VLAN information to all VTP client switches in the "ado" domain, simplifying VLAN deployment across the network. VLAN creation on VTP servers automates VLAN distribution.
*   **VLAN Naming:** VLANs are named descriptively (e.g., "tang1," "server," "quanly") to clearly identify the purpose and department/function associated with each VLAN, improving network documentation and manageability. Descriptive VLAN names enhance network documentation and management.

### 3.4.5. VLAN Interface IP Configuration:

These commands configure VLAN interfaces on the Core Routers and Switches, assigning IP addresses to these logical interfaces, enabling inter-VLAN routing and VLAN-specific network services. VLAN interfaces are needed for inter-VLAN routing and VLAN-specific services.

1.  **Core-Server (192.168.vlan.3) & Core2-Server (192.168.vlan.2):**
    ```
    core-server(config)#interface vlan 10
    core-server(config-if)#ip address 192.168.10.3 255.255.255.0
    core-server(config-if)#interface vlan 20
    core-server(config-if)#ip address 192.168.20.3 255.255.255.0
    core-server(config-if)#interface vlan 30
    core-server(config-if)#ip address 192.168.30.3 255.255.255.0
    core-server(config-if)#interface vlan 40
    core-server(config-if)#ip address 192.168.40.3 255.255.255.0
    core-server(config-if)#interface vlan 50
    core-server(config-if)#ip address 192.168.50.3 255.255.255.0
    core-server(config-if)#interface vlan 99
    core-server(config-if)#ip address 192.168.99.3 255.255.255.0
    ```

**(Explanation of VLAN Interface IP Configuration on Core Routers):**

*   `core-server(config)#interface vlan 10`: Enters interface configuration mode for VLAN interface 10. VLAN interface command creates a logical VLAN interface.
*   `core-server(config-if)#ip address 192.168.10.3 255.255.255.0`: Assigns the IP address 192.168.10.3 and subnet mask 255.255.255.0 to VLAN interface 10. This IP address becomes the gateway IP for devices in VLAN 10 (Floor 1 Network). IP address command assigns IP and subnet mask to the VLAN interface.
*   **(Repeat for VLANs 20, 30, 40, 50, 99):** Similar `interface vlan` and `ip address` commands are used to create and assign IP addresses to VLAN interfaces 20, 30, 40, 50, and 99 on Core-Server and Core2-Server, providing gateway IPs for each VLAN subnet. VLAN interfaces are configured for each VLAN subnet with corresponding IPs.

**(Rationale):**

*   **VLAN Interface Creation:** Creating VLAN interfaces (also known as Switched Virtual Interfaces - SVIs) on the Core Routers enables inter-VLAN routing. VLAN interfaces act as Layer 3 gateways for their respective VLANs, allowing traffic to be routed between different VLANs by the Core Routers. VLAN interfaces enable inter-VLAN routing on core routers.
*   **Gateway IPs:** Assigning IP addresses to VLAN interfaces on the Core Routers sets the gateway IP addresses for devices in each VLAN subnet. For example, devices in VLAN 10 will use 192.168.10.1 (unified HSRP IP - see next section) as their default gateway to reach other networks (including other VLANs and the internet). VLAN interfaces define gateway IPs for VLAN subnets.

2.  **Sw-tang1 - tang2 - tang3 - tang4 - giamdoc - quanly:**
    ```
    sw-tang1(config)#interface vlan 99
    sw-tang1(config-if)#ip address 192.168.99.10 255.255.255.0
    ```
    **(Repeat similarly for other switches).**

**(Explanation of Management VLAN Interface IP Configuration on Distribution and Access Switches):**

*   `sw-tang1(config)#interface vlan 99`: Enters interface configuration mode for VLAN interface 99 on switch Sw-tang1. Similar configuration is applied to other switches.
*   `sw-tang1(config-if)#ip address 192.168.99.10 255.255.255.0`: Assigns the IP address 192.168.99.10 and subnet mask 255.255.255.0 to VLAN interface 99 on Sw-tang1. This provides in-band management IP address for switch Sw-tang1 on the management VLAN (VLAN 99).  Each switch in the management VLAN is assigned a unique IP for management access.

**(Rationale):**

*   **Management VLAN Interfaces:** Creating VLAN interface 99 on distribution and access layer switches and assigning IP addresses enables in-band management access to these switches via the management VLAN (VLAN 99).  Administrators can use these IP addresses to remotely manage and configure the switches using protocols like SSH or Telnet (though SSH is recommended for security). Management VLAN interfaces enable in-band switch management access.
*   **VLAN 99 for Management:**  Using a dedicated management VLAN (VLAN 99) for switch management traffic separates management traffic from user data traffic, enhancing network security and manageability. Management VLAN isolates management traffic for security.

### 3.4.5. HSRP Configuration for Redundancy between Core-Server & Core2-Server:

These commands configure HSRP (Hot Standby Router Protocol) between Core-Server and Core2-Server for router redundancy and high availability. HSRP provides router redundancy for high availability.

1.  **Configure Core-Server as Active for VLANs 10, 20, 30, 40, 50, 99 (Using a unified network IP of "192.168.vlan.1/24"):**

![image](https://github.com/user-attachments/assets/ae2a5912-5276-4994-a8db-1251895a5427)
```
core-server(config-if)#interface vlan 10
core-server(config-if)#standby 1 ip 192.168.10.1
core-server(config-if)#standby 1 priority 200
core-server(config-if)#standby 1 preempt
```
**(Explanation of HSRP Active Configuration for VLAN 10 on Core-Server):**

*   `core-server(config-if)#interface vlan 10`: Enters interface configuration mode for VLAN interface 10 on Core-Server. HSRP is configured on VLAN interfaces.
*   `core-server(config-if)#standby 1 ip 192.168.10.1`: Configures HSRP group 1 for VLAN 10 and sets the virtual IP address to 192.168.10.1. This virtual IP address will be used as the default gateway for devices in VLAN 10. HSRP virtual IP address is configured.
*   `core-server(config-if)#standby 1 priority 200`: Sets the HSRP priority for Core-Server to 200. Higher priority makes this router more likely to become the active router in the HSRP group. Core-Server is set to higher HSRP priority to be the active router.
*   `core-server(config-if)#standby 1 preempt`: Enables HSRP preempt on Core-Server. Preempt allows the router with the higher priority (Core-Server) to take over as the active router if it becomes available, even if another router is currently active. HSRP preempt is enabled on Core-Server to ensure active router is always the higher priority router.

**(Rationale):**

*   **HSRP Group 1 (VLAN 10):** HSRP group 1 is configured for VLAN 10. Each VLAN requiring redundancy needs its own HSRP group.
*   **Virtual IP 192.168.10.1:**  The virtual IP address 192.168.10.1 is configured as the shared gateway IP for VLAN 10. Devices in VLAN 10 will use this virtual IP as their default gateway. Virtual IP provides a consistent gateway for VLAN 10.
*   **Core-Server as Active Router:** Core-Server is configured with a higher priority (200) and preempt enabled, making it the preferred active router for VLAN 10. Core-Server is preferred active router due to higher priority and preempt.

**(Repeat similarly for VLANs 20, 30, 40, 50, 99):** Similar HSRP configuration commands are repeated for VLAN interfaces 20, 30, 40, 50, and 99 on Core-Server, configuring it as the active router for all these VLANs. Core-Server is configured as active for all VLANs.

2.  **Configure Core2-Server as Standby for VLANs 10, 20, 30, 40, 50, 99 (Using a unified network IP of "192.168.vlan.1/24"):**

![image](https://github.com/user-attachments/assets/a253959e-4b7c-4d3b-978f-575af1ce5a1a)

```
core2-server(config)#interface vlan 10
core2-server(config-if)#standby 1 ip 192.168.10.1
core2-server(config-if)#standby 1 priority 100
```

**(Explanation of HSRP Standby Configuration for VLAN 10 on Core2-Server):**

*   `core2-server(config-if)#interface vlan 10`: Enters interface configuration mode for VLAN interface 10 on Core2-Server. HSRP standby is configured on VLAN interfaces.
*   `core2-server(config-if)#standby 1 ip 192.168.10.1`: Configures HSRP group 1 for VLAN 10 and sets the virtual IP address to 192.168.10.1, matching the virtual IP configured on Core-Server for VLAN 10.  Standby router uses the same virtual IP as active router for VLAN 10.
*   `core2-server(config-if)#standby 1 priority 100`: Sets the HSRP priority for Core2-Server to 100. Lower priority makes this router the standby router. Core2-Server is set to lower HSRP priority to be the standby router. **Note:** Preempt is *not* configured on Core2-Server, as it should remain in standby mode unless Core-Server fails.

**(Rationale):**

*   **HSRP Group 1 (VLAN 10):** Core2-Server is also configured for HSRP group 1 on VLAN 10, participating in the same HSRP group as Core-Server. Core2-Server participates in the same HSRP group as Core-Server.
*   **Virtual IP 192.168.10.1:** Core2-Server is configured with the same virtual IP address 192.168.10.1 as Core-Server for VLAN 10. This ensures that both routers share the same virtual gateway IP for VLAN 10, providing seamless failover. Standby router uses the same virtual IP to provide seamless failover.
*   **Core2-Server as Standby Router:** Core2-Server is configured with a lower priority (100) and preempt *not* enabled, making it the standby router for VLAN 10. Core2-Server is configured as standby router due to lower priority and no preempt. It will become active only if Core-Server fails.

**(Repeat similarly for other VLANs):** Similar HSRP configuration commands are repeated for VLAN interfaces 20, 30, 40, 50, and 99 on Core2-Server, configuring it as the standby router for all these VLANs. Core2-Server is configured as standby for all VLANs.

**(Summary of HSRP Configuration):**

HSRP is configured between Core-Server and Core2-Server to provide router redundancy for VLANs 10, 20, 30, 40, 50, and 99. Core-Server is configured as the active router with a higher priority and preempt enabled, while Core2-Server is configured as the standby router with a lower priority and preempt disabled.  A unified virtual IP address (192.168.vlan.1 for each VLAN) is configured for each VLAN, which will be used as the default gateway for devices in those VLANs.  HSRP provides router redundancy and high availability for VLAN routing.

### 3.4.6. SSH Configuration for Remote Access Control of Devices:

These commands enable SSH (Secure Shell) access to the Core Routers and Switches for secure remote management, replacing insecure Telnet with encrypted SSH. SSH provides secure remote management access.

```
core-server(config)#ip domain-name ado
core-server(config)#crypto key generate rsa
core-server(config)#line vty 0 4
core-server(config-line)#login local
core-server(config-line)#transport input ssh
core-server(config-line)#exit
core-server(config)#username quanly privilege 15 password 123
```
**(A user named "quanly" with password "123" has been created).**
**(Repeat similarly for other devices).**

**(Explanation of SSH Configuration Commands):**

*   `core-server(config)#ip domain-name ado`: Configures the IP domain name for the router to "ado".  A domain name is required for generating RSA keys for SSH.
*   `core-server(config)#crypto key generate rsa`: Generates RSA cryptographic keys for SSH. RSA keys are necessary for enabling SSH encryption.
*   `core-server(config)#line vty 0 4`: Enters line configuration mode for VTY lines 0 through 4.
*   `core-server(config-line)#login local`: Configures VTY lines to use local username/password authentication, as explained before.
*   `core-server(config-line)#transport input ssh`: Restricts the transport protocol for VTY lines to SSH only. This disables Telnet access and enforces secure SSH access for remote management. Transport input ssh restricts VTY access to SSH only.
*   `core-server(config-line)#exit`: Exits line configuration mode.
*   `core-server(config)#username quanly privilege 15 password 123`: Creates a local username "quanly" with privilege level 15 (administrator level) and password "123". This creates a local user account for SSH login.

**(Rationale):**

*   **SSH for Secure Remote Access:** Enabling SSH and disabling Telnet enhances the security of remote management access to the network devices. SSH encrypts all communication, protecting management credentials and data from eavesdropping and unauthorized access. SSH is used for secure remote management.
*   **Local Authentication:** Using `login local` with SSH enforces authentication using locally configured usernames and passwords, providing a basic level of access control. Local authentication provides basic SSH access control.
*   **Privilege Level 15 User:** Creating a user with privilege level 15 grants administrative privileges to the "quanly" user, allowing them to perform configuration and management tasks on the device. Privilege level 15 grants administrative access to the user.
*   **RSA Key Generation:** Generating RSA keys is essential for enabling SSH encryption. SSH encryption relies on cryptographic keys.

![image](https://github.com/user-attachments/assets/bf15afa1-e2d4-44cd-8592-1814acb6b9c4)

**(Verification of Successful SSH Login):**

The image shows a successful SSH login from PC\_quanly to Core-Server.  This verifies that SSH access is correctly configured and that the "quanly" user can successfully log in to the Core-Server via SSH for remote management. Successful SSH login verifies secure remote access is configured.

**(Repeat similarly for other devices):**  The same SSH configuration commands are repeated for other network devices (Core2-Server, Switches) to enable SSH access for secure remote management across all devices in the network. SSH is enabled on all network devices for consistent secure management.

### 3.4.7. DHCP Pool Configuration on Core-Servers for Client IP Assignment:

These commands configure DHCP pools on the Core Routers to dynamically assign IP addresses to devices in each VLAN. DHCP pools on core routers provide dynamic IP assignment to VLANs.

![image](https://github.com/user-attachments/assets/3ac5d9d9-cdec-4b2d-9620-766b98b71c58)

```
core-server(config)#ip dhcp pool tang1
core-server(dhcp-config)#network 192.168.10.0 255.255.255.0
core-server(dhcp-config)#default-router 192.168.10.1 (Points to the unified IP between Core-Server & Core2-Server)
core-server(dhcp-config)#dns-server 192.168.50.1
```
**(Explanation of DHCP Pool Configuration for VLAN 10 (tang1) on Core-Server):**

*   `core-server(config)#ip dhcp pool tang1`: Creates a DHCP pool named "tang1" for VLAN 10. DHCP pool command creates a new DHCP scope.
*   `core-server(dhcp-config)#network 192.168.10.0 255.255.255.0`: Defines the network address and subnet mask for the DHCP pool, corresponding to the VLAN 10 subnet (192.168.10.0/24). DHCP network command defines the IP range for the DHCP pool.
*   `core-server(dhcp-config)#default-router 192.168.10.1`: Sets the default gateway IP address for DHCP clients in VLAN 10 to 192.168.10.1, which is the virtual IP address of the HSRP group for VLAN 10 (configured on Core-Server and Core2-Server). DHCP default-router command sets the default gateway for DHCP clients.
*   `core-server(dhcp-config)#dns-server 192.168.50.1`: Sets the DNS server IP address for DHCP clients in VLAN 10 to 192.168.50.1, which is the IP address of the DNS server in the Server Room (VLAN 50).  DHCP dns-server command sets the DNS server IP for DHCP clients.

**(Rationale):**

*   **DHCP for Dynamic IP Assignment:** Configuring DHCP pools on Core-Server enables dynamic IP address assignment for devices connecting to each VLAN. DHCP simplifies IP address management for client devices.
*   **VLAN-Specific DHCP Pools:** Separate DHCP pools are created for each VLAN (VLANs 10, 20, 30, 40, 50, 99), ensuring that devices connecting to each VLAN receive IP addresses, default gateways, and DNS server information appropriate for their respective VLAN subnet. VLAN-specific DHCP pools provide subnet-appropriate IP configurations.
*   **HSRP Virtual IP as Default Gateway:** Using the HSRP virtual IP address (e.g., 192.168.10.1 for VLAN 10) as the default gateway in the DHCP pool ensures that clients in each VLAN use the HSRP virtual IP as their gateway, enabling seamless failover in case of router failure. HSRP virtual IP ensures gateway redundancy for DHCP clients.
*   **Internal DNS Server:** Configuring the internal DNS server IP address (192.168.50.1) in the DHCP pool ensures that LAN clients use the internal DNS server for name resolution, allowing them to resolve domain names for internal and external resources. Internal DNS server is provided to DHCP clients for name resolution.

**(Repeat similarly for other VLANs):** Similar `ip dhcp pool` commands are repeated for VLANs 20, 30, 40, 50, and 99 on Core-Server (and potentially Core2-Server if desired for redundancy), creating VLAN-specific DHCP pools for each VLAN subnet. DHCP pools are configured for each VLAN subnet.

### 3.4.8. TFTP Configuration to Backup Configuration Files for Device Replacement:

These commands demonstrate how to back up the running configuration of a Core Router to a TFTP (Trivial File Transfer Protocol) server for device replacement and disaster recovery. TFTP is used for configuration backup for device replacement.

![image](https://github.com/user-attachments/assets/13814f92-39f2-4010-b18a-7f50d99f6b90)

```
core-server#copy running-config tftp:
Address or name of remote host []? 192.168.50.3
Destination filename [core-server-confg]? core-server.cfg
```
**(Explanation of TFTP Backup Command):**

*   `core-server#copy running-config tftp:`: Executes the `copy running-config tftp:` command in privileged EXEC mode. This command initiates the process of copying the running configuration of the Core-Server router to a TFTP server. Copy running-config tftp command initiates configuration backup to TFTP server.
*   `Address or name of remote host []? 192.168.50.3`: Prompts for the IP address or hostname of the TFTP server. The IP address 192.168.50.3 (TFTP Server in VLAN 50) is entered as the destination TFTP server. TFTP server IP address is specified.
*   `Destination filename [core-server-confg]? core-server.cfg`: Prompts for the destination filename for the backup configuration file on the TFTP server. The filename "core-server.cfg" is entered. Backup filename on TFTP server is specified.

**(Rationale):**

*   **Configuration Backup for Disaster Recovery:** Backing up the running configuration to a TFTP server is a standard practice for device management and disaster recovery.  Configuration backup enables device replacement and disaster recovery.
*   **TFTP Server in Server Room (VLAN 50):** The TFTP server (192.168.50.5) is located in the Server Room VLAN (VLAN 50), which is a secure and centrally managed location for storing network backups. TFTP server is located in a secure zone.
*   **`copy running-config tftp:` Command:** This IOS command is a common and straightforward way to backup Cisco device configurations to a TFTP server. copy running-config tftp command is a standard IOS configuration backup command.

![image](https://github.com/user-attachments/assets/8435ac3c-6ee7-471c-bfc1-758ee591db7f)

**(Verification of Successful Backup):**

The image shows the successful completion of the `copy running-config tftp:` command, indicating that the configuration backup was successfully transferred to the TFTP server. Successful TFTP backup verifies configuration backup process.

**(Repeat similarly for other devices):** Similar `copy running-config tftp:` commands are repeated for other network devices (Core2-Server, Switches) to back up their configurations to the TFTP server, ensuring that configurations for all network devices are backed up for disaster recovery purposes. Configuration backup is performed for all network devices.

### 3.4.8. RADIUS Server Configuration for the Director's Office with Wireless Router:

This section details the RADIUS server configuration and integration with the Wireless Router in the Director's Office to enable centralized Wi-Fi authentication and MAC filtering. RADIUS server enables centralized Wi-Fi authentication and MAC filtering for Director's Office.

**Wireless Router Configuration (Director's Office):**

*   **IP address:** 192.168.99.9/24
*   **DNS:** 192.168.50.1

![image](https://github.com/user-attachments/assets/107bc697-3fb1-458d-8dfe-782c0ac7b417)

**(Explanation of Wireless Router Network Settings):**

*   **IP Address:** 192.168.99.9/24 - The Wireless Router in the Director's Office is assigned a static IP address of 192.168.99.9/24, placing it within the Management VLAN (VLAN 99).  Wireless Router is assigned a static IP in the Management VLAN.
*   **DNS Server:** 192.168.50.1 - The DNS server IP address is set to 192.168.50.1, pointing to the internal DNS server in the Server Room (VLAN 50). Wireless Router uses internal DNS server for name resolution.

**(Rationale):**

*   **Management VLAN for Wireless Router:** Placing the Wireless Router in VLAN 99 (Management VLAN) aligns with the network design, separating management traffic from user data traffic. Wireless Router is placed in Management VLAN for security.
*   **Internal DNS Server:** Using the internal DNS server ensures that the Wireless Router and devices connecting to it use the internal DNS server for name resolution, enabling consistent DNS service across the network. Internal DNS server is used for consistent name resolution.

*   **DHCP:** 192.168.60.0/24
*   **Start - End:** 100-149

![image](https://github.com/user-attachments/assets/bb5492b2-249a-4f7e-a8d4-2182200f4817)

**(Explanation of Wireless Router DHCP Configuration):**

*   **DHCP Server Enabled on Wireless Router:** The Wireless Router is configured to act as a DHCP server for the wireless network in the Director's Office (VLAN 60). Wireless Router provides DHCP for Director's Office wireless clients.
*   **DHCP IP Range:** 192.168.60.100 - 192.168.60.149/24 -  A DHCP IP address range is defined for the Director's Office wireless network (VLAN 60), providing dynamic IP address assignment for wireless clients connecting to this Wireless Router. DHCP IP range is defined for Director's Office wireless clients.

**(Rationale):**

*   **VLAN 60 DHCP:**  The Wireless Router provides DHCP services specifically for VLAN 60 (Director's Office Wireless Network), ensuring that wireless clients connecting to this Wireless Router receive IP addresses within the VLAN 60 subnet. Wireless Router provides VLAN-specific DHCP for Director's Office.
*   **Separate DHCP Scope:**  Using a separate DHCP scope on the Wireless Router for VLAN 60 is appropriate for a smaller, isolated wireless network like the Director's Office wireless network. Separate DHCP scope is used for isolated wireless network.

*   **SSID is: Rin**
*   ![image](https://github.com/user-attachments/assets/dbc33010-24b9-41b0-9c29-2e4abe505e88)

**(Explanation of Wireless Router SSID Configuration):**

*   **SSID:** "Rin" - The Service Set Identifier (SSID) for the Director's Office Wi-Fi network is set to "Rin".  SSID "Rin" is set for Director's Office Wi-Fi network.

**(Rationale):**

*   **SSID for Wi-Fi Network Identification:** The SSID "Rin" is the name of the Wi-Fi network that will be broadcast by the Wireless Router in the Director's Office. Users will see this SSID in their Wi-Fi device lists and use it to connect to the network. SSID identifies the Wi-Fi network.

*   **RADIUS Server: 192.168.99.10**
*   **Shared Secret: rin123**
*   **Security Mode: WPA2 Enterprise**

![image](https://github.com/user-attachments/assets/26be33a2-0218-4069-b01c-a886c08bb30a)

**(Explanation of Wireless Router RADIUS Configuration):**

*   **Security Mode: WPA2 Enterprise:** The Wi-Fi security mode is set to WPA2 Enterprise. WPA2 Enterprise provides stronger security compared to WPA2-PSK by using RADIUS for centralized authentication and encryption. WPA2 Enterprise is selected for enhanced security.
*   **RADIUS Server IP:** 192.168.99.10 - The IP address of the RADIUS server (RADIUS server in VLAN 99) is configured on the Wireless Router. This tells the Wireless Router where to send authentication requests for Wi-Fi users. RADIUS server IP is configured.
*   **Shared Secret:** "rin123" - A shared secret key "rin123" is configured on the Wireless Router and must match the shared secret configured on the RADIUS server.  The shared secret is used for secure communication between the Wireless Router and the RADIUS server. Shared secret is configured for RADIUS communication security.

**(Rationale):**

*   **RADIUS for Centralized Authentication:** Configuring WPA2 Enterprise with RADIUS authentication enables centralized Wi-Fi user authentication via the RADIUS server. Instead of using a pre-shared key (WPA2-PSK), users will authenticate using individual usernames and passwords managed on the RADIUS server. RADIUS enables centralized user-based Wi-Fi authentication.
*   **Enhanced Security and Access Control:** WPA2 Enterprise with RADIUS provides stronger security and more granular access control compared to WPA2-PSK. It allows for user-based authentication, centralized user management, and potentially role-based access control based on RADIUS attributes. WPA2 Enterprise enhances Wi-Fi security and access control granularity.

**RADIUS Server Configuration:**

*   **Client IP: 192.168.99.9 (Points to Wireless Router)**
*   **Secret: rin123 (Matches Shared Secret)**
*   **Create users and passwords: u1, u2, u3 | u1, u2, u3**

![image](https://github.com/user-attachments/assets/5ecf2468-ef5c-47cc-8d87-4b247e9ba226)

**(Explanation of RADIUS Server Configuration):**

*   **RADIUS Client:** Client IP: 192.168.99.9 - The IP address of the Wireless Router in the Director's Office (192.168.99.9) is configured as a RADIUS client on the RADIUS server. This tells the RADIUS server to accept authentication requests from this specific Wireless Router. Wireless Router IP is configured as RADIUS client.
*   **Shared Secret:** Secret: "rin123" - The shared secret key "rin123" is configured on the RADIUS server, matching the shared secret configured on the Wireless Router.  The shared secret is used to secure communication between the RADIUS server and the Wireless Router. Shared secret is configured to match Wireless Router shared secret.
*   **User Accounts:** User accounts "u1," "u2," and "u3" are created on the RADIUS server with passwords "u1," "u2," and "u3" respectively. These user accounts will be used for Wi-Fi authentication by users connecting to the Director's Office Wi-Fi network. User accounts are created on RADIUS server for Wi-Fi authentication.

**(Rationale):**

*   **RADIUS Server for Authentication:** The RADIUS server is configured to authenticate Wi-Fi users connecting to the Wireless Router in the Director's Office. RADIUS server handles Wi-Fi user authentication.
*   **Centralized User Management:** User accounts for Wi-Fi access are managed centrally on the RADIUS server. This allows administrators to create, manage, and control Wi-Fi user access from a central location. RADIUS provides centralized Wi-Fi user management.
*   **Shared Secret for Security:** The shared secret ensures secure communication between the Wireless Router and the RADIUS server, protecting authentication credentials during transmission. Shared secret secures RADIUS communication.

**Testing RADIUS Authentication:**

On the device to be connected, select WPA2 Enterprise protocol and enter the corresponding data:

*   **SSID:** SSID (set in Wireless Router)
*   **User ID:** Username (set in RADIUS)
*   **Password:** (set in RADIUS)

![image](https://github.com/user-attachments/assets/435a1c06-66b7-4f86-85e8-635dbdc69b78)

**(Explanation of Testing RADIUS Authentication):**

To test RADIUS authentication, a wireless client device (e.g., a laptop or smartphone) is configured to connect to the "Rin" Wi-Fi network (SSID set on the Wireless Router) using WPA2 Enterprise security.  Users are prompted to enter their username and password, which should be credentials of a user account created on the RADIUS server (e.g., "u1," "u2," or "u3").

**(Verification of RADIUS Authentication):**

Successful connection to the Wi-Fi network using WPA2 Enterprise and RADIUS credentials verifies that RADIUS authentication is working correctly.  Users are able to authenticate to Wi-Fi network using RADIUS credentials.

### 3.4.9. MAC Filter Configuration for the Director's Office with Wireless Router (Allow MAC List here):

This section describes the configuration of MAC address filtering on the Wireless Router in the Director's Office to restrict Wi-Fi access to only authorized devices, adding an extra layer of security. MAC filtering restricts Wi-Fi access to authorized devices based on MAC addresses.

**In Wireless Router:**

*   **MAC 01: MAC address of Laptop_giamdoc**
*   **MAC 02: MAC address of DT_giamdoc**

![image](https://github.com/user-attachments/assets/8c17ddf7-52d0-4c3c-8fef-48b214d8b694)

**(Explanation of MAC Address List for Filtering):**

*   **Allowed MAC Addresses:** A list of allowed MAC addresses is configured on the Wireless Router. In this example, MAC addresses for "Laptop_giamdoc" (MAC 01) and "DT_giamdoc" (MAC 02) are added to the allowed list.  Only these MAC addresses will be permitted to connect to the Wi-Fi network.  Only listed MAC addresses are permitted for Wi-Fi access.

**(Rationale):**

*   **MAC Filtering for Access Control:** MAC address filtering provides an additional layer of access control for the Director's Office Wi-Fi network, restricting network access to only devices with MAC addresses explicitly added to the allowed list. MAC filtering adds an extra layer of access control.
*   **Enhanced Security for Sensitive Area:** MAC filtering is particularly useful in sensitive areas like the Director's Office, where stricter access control and device authorization are required. MAC filtering enhances security in sensitive areas like Director's Office.

**Select Option: "Permit PCs listed below to access wireless network" to only allow the MAC Addresses listed below to connect to the Wireless Router.**

**(Explanation of MAC Filtering Mode):**

*   **"Permit PCs listed below to access wireless network":**  This option (or similar wording depending on the Wireless Router interface) is selected in the Wireless Router's MAC filtering configuration.  This configures the MAC filter in "allow list" mode, meaning that only devices with MAC addresses listed in the allowed list will be permitted to connect to the Wi-Fi network.  MAC filtering is set to "allow list" mode to only permit listed devices.

**(Rationale):**

*   **Allow List (Whitelist) Approach:** Using an allow list (whitelist) for MAC filtering is generally more secure than a deny list (blacklist) approach.  An allow list explicitly defines which devices are permitted, blocking all other devices by default.  Allow list is more secure than deny list for MAC filtering.
*   **Restricted Access for Director's Office:**  This configuration ensures that only authorized devices (Laptop\_giamdoc and DT\_giamdoc) are allowed to connect to the Director's Office Wi-Fi network, further enhancing security and access control in this sensitive area. MAC filtering restricts Wi-Fi access in Director's Office to authorized devices.

### 3.4.10. WLC Configuration to Distribute WLANs to APs for Each Floor:

This section details the configuration of the Wireless LAN Controller (WLC) to manage Access Points (APs) and distribute WLANs (Wireless LANs - Wi-Fi networks) to APs on each floor, enabling centralized Wi-Fi management and VLAN-based wireless network segmentation. WLC centralizes Wi-Fi management and enables VLAN-based wireless segmentation.

**First, log in to the WLC via a computer:**

![image](https://github.com/user-attachments/assets/9f0d5eab-77c4-41d5-bfc6-67ac873e4d56)

**(Explanation of WLC Login):**

The first step is to access the WLC's web-based management interface (GUI) via a web browser.  This typically involves browsing to the WLC's management IP address (192.168.99.200 in this case, as defined in the IP Addressing Plan).  WLC is accessed via web browser for configuration.

**Next, navigate to "CONTROLLER" ----> "INTERFACE" and create a new interface to set up the network for the WLAN:**

![image](https://github.com/user-attachments/assets/b05278c5-cbea-4819-a4a5-cfc4b3f153b5)

**Interface Configuration on WLC for VLANs:**

*   **Interface Name: tang1** (Interface name, here we configure Floor 1 as an example) -  A descriptive name "tang1" is given to the interface, representing the VLAN for Floor 1. Descriptive interface names improve WLC configuration clarity.
*   **Port Number: 1** (Enter the port number the WLC is connected to) -  The physical port number on the WLC to which the VLAN interface is associated (Port 1 in this example). Specifies the physical port for VLAN interface.
*   **VLAN Identifier: 10** (Enter the corresponding VLAN, Floor 1 is VLAN 10) -  The VLAN ID for the interface is set to 10, associating this interface with VLAN 10 (Floor 1 Network). VLAN ID associates interface with VLAN 10.
*   **IP Address: 192.168.10.100** (Set IP for this Interface) - A static IP address of 192.168.10.100/24 is assigned to the VLAN 10 interface on the WLC.  This IP address is used for management of the WLC interface on VLAN 10. Static IP is assigned to WLC VLAN interface.
*   **Netmask: 255.255.255.0** - The subnet mask for the IP address.
*   **Gateway: 192.168.10.1** (Points to the common IP of the 2 Core Servers) - The default gateway IP address is set to 192.168.10.1, which is the HSRP virtual IP address for VLAN 10 (configured on Core Routers).  Gateway IP points to HSRP virtual IP for VLAN 10.
*   **Primary DHCP Server: 192.168.10.1** (Since Core Server provides DHCP, point to it) -  The DHCP server IP address is also set to 192.168.10.1, although in this network design, the DHCP server is actually running on the Core Routers (which have VLAN interfaces in each VLAN subnet). This setting might be for internal WLC management purposes or if the WLC were to act as a DHCP relay. DHCP server IP points to HSRP virtual IP (though Core Routers are DHCP servers).

**(Rationale):**

*   **VLAN Interfaces on WLC:** Creating VLAN interfaces on the WLC allows the WLC to participate in and manage wireless networks within specific VLANs (VLANs 10, 20, 30, 40 for Floors 1-4). VLAN interfaces on WLC enable VLAN-based wireless management.
*   **VLAN-Specific IP Addresses:** Assigning IP addresses to VLAN interfaces on the WLC allows the WLC to be managed within each VLAN subnet. WLC management IP is configured for each VLAN interface.
*   **Gateway and DHCP Server Settings:** Setting the gateway and DHCP server IP addresses ensures that the WLC VLAN interface has proper routing and DHCP server information configured. Gateway and DHCP server settings are configured for WLC VLAN interfaces.

**(Repeat similarly for Interfaces for Floors 2-3-4):** Similar interface configuration steps are repeated to create VLAN interfaces on the WLC for VLANs 20 (tang2 - Floor 2), 30 (tang3 - Floor 3), and 40 (tang4 - Floor 4), configuring VLAN-specific interfaces for each floor's wireless network. VLAN interfaces are created for each floor VLAN.

**Next, WLANs Section:**

Next, navigate to "WLANs" ----> "Go" and create new WLANs for APs to get configurations from and provide to clients:

![image](https://github.com/user-attachments/assets/8dfbcec0-807a-4ee2-8747-67c29d5fb5e9)

**WLAN Configuration on WLC for Each Floor:**

*   **WLAN Creation:** New WLANs (Wireless LANs - Wi-Fi networks) are created on the WLC, one for each floor (e.g., "tang1" for Floor 1). WLANs define Wi-Fi network settings for each floor.
*   **SSID Setting:** Set the desired SSID (Service Set Identifier) for each WLAN (e.g., "tang1-WLAN" for Floor 1). SSID defines the Wi-Fi network name for each floor.

*   **Interface/Interface Group:** Select the corresponding interface configured above.

**(Explanation of WLAN Interface Assignment):**

*   **Interface/Interface Group Selection:** When creating each WLAN, the corresponding VLAN interface (created in the previous step) is selected as the "Interface" or "Interface Group". For example, for the "tang1-WLAN" WLAN, the "tang1" VLAN interface (VLAN 10 interface) is selected. WLAN Interface assignment links WLAN to specific VLAN.

**(Rationale):**

*   **VLAN-to-WLAN Mapping:** Mapping each WLAN to a specific VLAN interface on the WLC is crucial for VLAN-based wireless network segmentation. This configuration ensures that wireless clients connecting to a specific WLAN are placed in the corresponding VLAN. VLAN-to-WLAN mapping enables wireless network segmentation.
*   **WLAN Distribution to APs (via AP Groups - see next section):**  These WLAN configurations will be distributed to Access Points (APs) managed by the WLC, allowing the APs to broadcast these WLANs and provide Wi-Fi access to clients on each floor within their respective VLANs. WLC distributes WLAN configurations to APs for each floor.

**Security Section:**

*   **Layer 2 Security: Select option WPA + WPA2.** Open the WPA2 Encryption section and check AES to enhance security for our WLAN. Check PSK to set a password.

![image](https://github.com/user-attachments/assets/2f73d21b-a395-4e7a-83c5-0d2bfc0bc027)

**(Explanation of WLAN Security Configuration - WPA2-PSK):**

*   **Layer 2 Security:** "WPA + WPA2" - Layer 2 security is configured for the WLANs using WPA2 (Wi-Fi Protected Access 2) with PSK (Pre-Shared Key) authentication. WPA2-PSK is selected for Wi-Fi security.
*   **WPA2 Encryption: AES:**  Within WPA2 settings, AES (Advanced Encryption Standard) encryption is selected. AES is a strong encryption algorithm used with WPA2 to encrypt Wi-Fi traffic, protecting data confidentiality. AES encryption is enabled for WPA2 security.
*   **PSK (Pre-Shared Key):** PSK is checked to enable Pre-Shared Key authentication.  A password (PSK) is set for each WLAN.  Users connecting to these WLANs will need to enter this pre-shared key (password) to authenticate and gain access. PSK password is set for Wi-Fi authentication.

**(Rationale):**

*   **WPA2-PSK Security:** Implementing WPA2-PSK security provides a standard level of Wi-Fi security for the WLANs, protecting wireless traffic with encryption and requiring password-based authentication for access. WPA2-PSK provides standard Wi-Fi security.
*   **AES Encryption:** Using AES encryption enhances the security of the WPA2-PSK implementation, providing strong encryption for wireless data transmission. AES encryption strengthens WPA2 security.

**Advanced Section:**

*   Check FlexConnect to help enable local switching for access points (APs) below.
*   ![image](https://github.com/user-attachments/assets/8e6348de-41f6-476c-b54b-c58bcf57af86)

**(Explanation of FlexConnect Configuration):**

*   **FlexConnect Enabled:** The "FlexConnect" option is checked in the Advanced settings of the WLAN configuration. FlexConnect mode is enabled for APs.

**(Rationale):**

*   **FlexConnect Mode for APs:** Enabling FlexConnect mode for the WLANs allows the Access Points (APs) to perform local switching of client traffic and provides more flexibility in managing APs in distributed deployments. FlexConnect enables local switching on APs. In this lab, it might be used to allow APs to operate even if the WLC connection is temporarily lost, or for optimized traffic forwarding in certain scenarios.

**(Repeat similarly for other WLANs):** Similar WLAN configuration steps are repeated to create WLANs for Floors 2, 3, and 4, configuring VLAN-specific WLANs for each floor's wireless network. WLANs are created for each floor VLAN.

### 3.4.11. AP Group Configuration in WLC to Distribute WLANs to APs for Each Floor:

This section describes the configuration of AP Groups on the WLC to distribute the VLAN-specific WLANs to the Access Points (APs) on each floor, completing the wireless network segmentation and WLAN deployment process. AP Groups on WLC distribute WLANs to APs for each floor.

To distribute networks to floor APs, navigate to "WLANs" ----> "AP Groups" and create a new AP Group for APs to retrieve configurations from and distribute WLANs for corresponding floors:

![image](https://github.com/user-attachments/assets/a396e752-456d-47f2-9a19-5b55e6bd7bad)

**(Explanation of AP Group Creation):**

*   **AP Group Creation:** New AP Groups are created on the WLC, one for each floor (e.g., "Floor 1 AP Group" for Floor 1 APs). AP Groups are used to group APs for configuration management.
*   **Purpose:** AP Groups allow for grouping Access Points (APs) based on their location or function (in this case, by floor). This simplifies WLAN distribution and configuration management, allowing you to apply specific WLAN configurations to groups of APs instead of configuring each AP individually. AP Groups simplify AP configuration management.

After creating the Group, enter the newly created Group and add the WLAN SSID of the corresponding floor.

Next is APs, when an AP joins the WLC, its name will appear here. Add the corresponding AP to the Group we want.

For example, here is Group 1, for Floor 1, so add the AP named "wifi tang 1".

![image](https://github.com/user-attachments/assets/a7a1aabf-8a60-4918-a892-09a047bd785a)
![image](https://github.com/user-attachments/assets/8c2f1e51-c890-4381-af46-57b3430d3be1)

**(Explanation of AP Group and WLAN Assignment):**

*   **WLAN Assignment to AP Group:** Within each AP Group (e.g., "Floor 1 AP Group"), the corresponding WLAN (e.g., "tang1-WLAN") is assigned to that AP Group. This links the WLAN configuration to the AP Group. WLANs are assigned to AP Groups to distribute WLAN configurations.
*   **AP Membership in AP Group:** Access Points (APs) are added to their respective AP Groups based on their physical location (e.g., the "wifi tang 1" AP is added to the "Floor 1 AP Group").  Adding APs to AP Groups applies the AP Group configuration to the APs.

**(Rationale):**

*   **WLAN Distribution via AP Groups:** AP Groups are used to distribute the VLAN-specific WLAN configurations to the Access Points (APs) on each floor. By assigning the "tang1-WLAN" WLAN to the "Floor 1 AP Group", all APs that are members of this group will broadcast the "tang1-WLAN" SSID and provide Wi-Fi access for VLAN 10 (Floor 1 Network). AP Groups distribute VLAN-specific WLANs to floor APs.
*   **Simplified WLAN Management:** AP Groups simplify WLAN management by allowing administrators to manage WLAN configurations at the group level instead of configuring each AP individually.  WLAN management is simplified through AP Groups.
*   **Scalable WLAN Deployment:** AP Groups facilitate scalable WLAN deployments.  As you add more APs to each floor, you can simply add them to the corresponding AP Group, and they will automatically inherit the WLAN configurations defined for that group. AP Groups enable scalable WLAN deployments.
*   **Floor-Specific WLANs:**  This AP Group configuration ensures that each floor has its own dedicated WLAN (SSID) and that wireless clients connecting to the APs on each floor are placed in the correct VLAN (VLAN 10 for Floor 1, VLAN 20 for Floor 2, etc.), achieving VLAN-based wireless network segmentation as required. AP Groups enable floor-specific VLAN-based wireless networks.

**Verification of AP Configuration and Client Connectivity:**

And then, the APs of each floor will only receive a single Providing WLAN. APs receive VLAN-specific WLANs based on AP Group assignment.

For Client devices, just enter the corresponding data and they can connect to the clearly segmented VLAN Wi-Fi network. Clients can connect to VLAN-segmented Wi-Fi networks.

As in the example image above, AP IP is 192.168.99.5/24, but it assigns 192.168.10.9/24. This is because it will retrieve the configuration from the WLC to use. APs receive VLAN-specific IPs based on WLC configuration, demonstrating VLAN segmentation.

![image](https://github.com/user-attachments/assets/9086a2ff-ad90-4278-8b69-b01c511ab3b2)

**(Verification of Client Connectivity and VLAN Assignment):**

The final image shows a client device connected to the "tang1-WLAN" Wi-Fi network (SSID for Floor 1).  Although the Access Point itself has an IP address in the Management VLAN (192.168.99.5/24), the client device connected to the "tang1-WLAN" SSID is assigned an IP address in the VLAN 10 subnet (192.168.10.9/24). This demonstrates that:

*   **WLAN Distribution is Successful:** The WLAN configuration ("tang1-WLAN") is successfully distributed to the Access Point (wifi tang 1).
*   **VLAN Segmentation is Working:** Wireless clients connecting to "tang1-WLAN" are correctly placed in VLAN 10 (Floor 1 Network), achieving VLAN-based wireless network segmentation as designed. Clients connecting to different floor WLANs will be placed in their respective VLANs.
*   **DHCP IP Assignment is Functional:** Clients are receiving IP addresses via DHCP from the DHCP pool configured for VLAN 10, confirming DHCP functionality for wireless clients. DHCP IP assignment is working for wireless clients within VLAN 10.

**End**

</details>





# Introduction
<!-- Vietnamese -->
<details>
  <summary><h2>🇻🇳 Tiếng Việt</h2></summary>

## Giới thiệu

Repository này chứa các file cấu hình (packet tracer files - `.pkt`) và tài liệu thiết kế cho các bài lab mạng Cisco, bao gồm nhiều chủ đề như:

*   **Cisco Security:** Các cấu hình liên quan đến bảo mật mạng Cisco (CCNA Security).
*   **OSPF (Open Shortest Path First):** Cấu hình định tuyến OSPF cơ bản và nâng cao (nhiều subnet).
*   **RIP (Routing Information Protocol):** Cấu hình định tuyến RIP.
*   **Switchport VLAN:** Cấu hình VLAN cơ bản và trunking.
*   **VTP (VLAN Trunking Protocol):** Cấu hình VTP (quản lý VLAN tập trung).
*   **Webserver and AP (Access Point):** Cấu hình webserver và access point.
*   **SSH (Secure Shell):** Cấu hình SSH (truy cập/quản lý thiết bị từ xa, mã hóa).
*   **HSRP (Hot Standby Router Protocol):** Cấu hình dự phòng gateway, tăng tính sẵn sàng của mạng.
*   **Load Balancing:** Cấu hình cân bằng tải (phân phối lưu lượng, tăng khả năng chịu tải).
*   **TFTP - Backup & Restore:** Cấu hình backup và restore cấu hình thiết bị.
*   **RADIUS (Remote Authentication Dial-In User Service):** Cấu hình RADIUS server (xác thực/ủy quyền tập trung).

## Nội dung

*   **`Cisco Security Project (CCNA).pkt`:** File Packet Tracer chứa các cấu hình bảo mật Cisco. Các lệnh cấu hình có thể bao gồm:
    *   `username <username> privilege <level> secret <password>` (Tạo user)
    *   `enable secret <password>` (Đặt mật khẩu enable)
    *   `line vty 0 4`
        *   `login local` (Yêu cầu đăng nhập bằng user local)
        *   `transport input ssh` (Chỉ cho phép kết nối SSH)
    *   `ip access-list standard <acl-name>` (Tạo access list)
        *   `permit <ip_address> <wildcard>`
        * `deny any`
    *   `ip access-group <acl-name> in` (Áp dụng access list vào interface)
    *   `service password-encryption` (Mã hoá mật khẩu)
    *   `security passwords min-length <length>` (Độ dài tối thiểu mật khẩu)
    *	`login block-for <seconds> attempts <number> within <seconds>` (Chống brute-force)
    *	`ip ssh version 2` (Chỉ sử dụng SSH version 2)
    * `crypto key generate rsa` (Tạo key RSA cho SSH, nên chỉ định `modulus <bitsize>`, ví dụ: `modulus 2048`)

*   **`OSPF Routing Basic.pkt`:** Cấu hình OSPF cơ bản. Các lệnh:
    *   `router ospf <process-id>`
    *   `network <network-address> <wildcard-mask> area <area-id>`
    *   `show ip ospf neighbor` (Kiểm tra neighbor)
    *   `show ip route ospf` (Xem route OSPF)
    *   `show ip ospf interface brief`

*   **`OSPF Routing With 18 Subnets.pkt`:** Cấu hình OSPF với nhiều subnet.  Cấu hình area, redistribute, default route (nếu cần).

*   **`Rip Routing With 22 Subnets.pkt`:** Cấu hình RIP với nhiều subnet.
    *   `router rip`
    *   `version 2`
    *   `network <network-address>` (classful network address)
    *   `no auto-summary`
    *   `show ip route rip`
    * `passive-interface <interface>` (nếu không muốn gửi update qua interface nào đó)

*   **`Swport Vlan Basic.pkt`:** Cấu hình VLAN cơ bản.
    *   `vlan <vlan-id>`
    *   `name <vlan-name>`
    *   `interface <interface-name>`
    *   `switchport mode access`
    *   `switchport access vlan <vlan-id>`
    *   `show vlan brief`

*   **`Swport Vlan Trunking.pkt`:** Cấu hình trunking.
    *   `interface <interface-name>`
    *   `switchport mode trunk`
    *   `switchport trunk encapsulation dot1q`
    *   `switchport trunk allowed vlan <vlan-list>` (hoặc `switchport trunk allowed vlan add/remove/except`)
    *   `show interfaces trunk`

*   **`VLAN and Trunking With OSPF For 18 Subnets.pkt`:** Kết hợp VLAN, trunking và OSPF.

*   **`VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt`:** Cấu hình VLAN, trunking, VTP, OSPF, webserver và AP.
    *   `vtp mode {server | client | transparent}`
    *   `vtp domain <domain-name>`
    *   `vtp password <password>`
    *   `ip address <ip-address> <subnet-mask>` (cho interface, webserver)
    *   Cấu hình DHCP (nếu cần).
    * Cấu hình Wireless LAN Controller (WLC) và AP.

*   **`HSRP.pkt` (Ví dụ):** File này mô phỏng cấu hình HSRP để cung cấp dự phòng gateway.
    *   Trên Router chính (Active):
        *   `interface <interface-name>`
        *   `ip address <ip-address> <subnet-mask>`
        *   `standby <group-number> ip <virtual-ip-address>`
        *   `standby <group-number> priority <priority-value>` (Cao hơn trên router chính)
        *   `standby <group-number> preempt` (Cho phép router ưu tiên cao hơn chiếm quyền)
        *   `standby <group-number> track <interface-name> [decrement-value]` (Giảm priority nếu interface bị down)
    *   Trên Router dự phòng (Standby):  Tương tự như trên, nhưng `priority` thấp hơn.
    *  Kiểm tra: `show standby`, `show standby brief`

*   **`Load Balancing.pkt` (Ví dụ):** File này *có thể* chứa cấu hình cân bằng tải, tuy nhiên cần file cụ thể để biết chi tiết.  Cấu hình cân bằng tải phụ thuộc lớn vào thiết bị hoặc phần mềm được sử dụng. Ví dụ:
    * **Trên Router Cisco (PBR - Policy-Based Routing):**
        *  `route-map <map-name> permit 10`
        *  `match ip address <access-list>`
        *  `set ip next-hop <next-hop-1> <next-hop-2>`
        *  `ip access-list extended <access-list>` (định nghĩa traffic cần cân bằng tải).
        *  Áp dụng route-map vào interface: `ip policy route-map <map-name>`
    * **Trên Load Balancer chuyên dụng/Phần mềm (HAProxy, Nginx):** Cấu hình sẽ rất khác, và thường được thực hiện thông qua file cấu hình riêng của phần mềm đó.

* **`Backup_Restore.pkt` (Ví dụ):** File này mô phỏng backup/restore cấu hình sử dụng TFTP.
    *   **Bước 1: Cấu hình TFTP Server:**
        *   Trong Packet Tracer, thêm một server và cấu hình dịch vụ TFTP (bật dịch vụ).
        *   Gán địa chỉ IP cho server.
    *   **Bước 2: Backup (Trên Router/Switch):**
        *   `copy running-config tftp` (hoặc `copy startup-config tftp`)
        *   `Address or name of remote host []?`  Nhập địa chỉ IP của TFTP server.
        *   `Destination filename [router-config]?` Nhập tên file muốn lưu (hoặc nhấn Enter để dùng tên mặc định).
    *   **Bước 3: Restore (Trên Router/Switch):**
        *   `copy tftp running-config` (hoặc `copy tftp startup-config`)
        *   `Address or name of remote host []?` Nhập địa chỉ IP của TFTP server.
        *   `Source filename []?` Nhập tên file đã backup.
        *   `Destination filename [running-config]?` (Nhấn Enter)
        *   Xác nhận ghi đè cấu hình (nếu có).
    *  **Lưu ý:**  Đảm bảo router/switch có thể "nhìn thấy" (ping được) TFTP server.

* **`RADIUS.pkt` (Ví dụ):** File này mô phỏng xác thực RADIUS.
    *   **Bước 1: Cấu hình RADIUS Server:**
        *   Trong Packet Tracer, thêm một server, vào Services -> AAA.
        *   Bật dịch vụ RADIUS.
        *   Thêm Client:  `Client Name` (tên bất kỳ), `Client IP` (IP của router/switch), `Secret` (mật khẩu chung), `Server Type` (RADIUS).
        *   Thêm User: `Username`, `Password`, các dịch vụ (ví dụ, bật `PAP` hoặc `CHAP`).
    *   **Bước 2: Cấu hình Router/Switch (RADIUS Client):**
        *   `aaa new-model` (bật AAA)
        *   `radius server <server-name>` (tên tự đặt)
        *   `address ipv4 <server-ip>` (IP của RADIUS server)
        *   `key <shared-secret>` (khớp với `Secret` trên server)
        *   `aaa authentication login default group radius local` (xác thực login bằng RADIUS, nếu RADIUS down thì dùng user local)
        *   `aaa authorization exec default group radius local` (ủy quyền các lệnh exec bằng RADIUS, fallback về local nếu RADIUS down)
        *   `aaa authorization network default group radius` (ủy quyền các dịch vụ mạng khác - nếu cần).
        *   `line vty 0 4`
        *     `login authentication default`
        *     `authorization exec default` (nếu muốn ủy quyền cả exec)
    * **Bước 3: Kiểm tra**
        * Thử truy cập vào router/switch bằng user đã cấu hình trên RADIUS server.
        * `debug radius` (trên router/switch để xem quá trình xác thực).
        * `show aaa servers`

## Hướng dẫn

1.  **Cài đặt Cisco Packet Tracer:** Cài đặt Cisco Packet Tracer.
2.  **Mở file:** Mở file `.pkt` tương ứng.
3.  **Khám phá:** Dùng các lệnh `show` (ví dụ: `show running-config`, `show ip interface brief`, `show vlan brief`, `show ip route`).  Chạy các lệnh `debug` để xem chi tiết quá trình (ví dụ: `debug ip ospf events`, `debug radius`).
4.  **Thay đổi và Thử nghiệm:**  Thay đổi cấu hình, thêm/bớt thiết bị, và kiểm tra lại.

</details>

<!-- English -->
<details>
  <summary><h2>🇬🇧 English</h2></summary>

## Introduction

This repository contains Packet Tracer files (`.pkt`) and design documents for Cisco network labs, covering various topics such as:

*   **Cisco Security:** Cisco network security configurations (CCNA Security).
*   **OSPF (Open Shortest Path First):** Basic and advanced OSPF routing.
*   **RIP (Routing Information Protocol):** RIP routing configuration.
*   **Switchport VLAN:** Basic VLAN and trunking configurations.
*   **VTP (VLAN Trunking Protocol):** VTP configuration.
*   **Webserver and AP (Access Point):** Webserver and access point configuration.
*   **SSH (Secure Shell):**  SSH configuration (remote access/management, encryption).
*   **HSRP (Hot Standby Router Protocol):** Gateway redundancy configuration, improving network availability.
*   **Load Balancing:** Load balancing configuration (traffic distribution, increased availability).
*   **TFTP - Backup & Restore:** Device configuration backup and restore.
*   **RADIUS (Remote Authentication Dial-In User Service):** RADIUS server configuration (centralized authentication/authorization).

## Contents

*   **`Cisco Security Project (CCNA).pkt`:** Packet Tracer file with Cisco security configs.  Possible commands:
    *   `username <username> privilege <level> secret <password>`
    *   `enable secret <password>`
    *   `line vty 0 4`
        *   `login local`
        *   `transport input ssh`
    *   `ip access-list standard <acl-name>`
        *   `permit <ip_address> <wildcard>`
        *   `deny any`
    *   `ip access-group <acl-name> in`
    *   `service password-encryption`
    *   `security passwords min-length <length>`
    *	`login block-for <seconds> attempts <number> within <seconds>`
    *	`ip ssh version 2`
    *   `crypto key generate rsa` (Generate RSA key for SSH; consider specifying `modulus <bitsize>`, e.g., `modulus 2048`)

*   **`OSPF Routing Basic.pkt`:** Basic OSPF configuration. Commands:
    *   `router ospf <process-id>`
    *   `network <network-address> <wildcard-mask> area <area-id>`
    *   `show ip ospf neighbor`
    *   `show ip route ospf`
    *   `show ip ospf interface brief`

*   **`OSPF Routing With 18 Subnets.pkt`:** OSPF with multiple subnets. Area configuration, redistribution, default route (if needed).

*   **`Rip Routing With 22 Subnets.pkt`:** RIP with multiple subnets.
    *   `router rip`
    *   `version 2`
    *   `network <network-address>` (classful)
    *   `no auto-summary`
    *   `show ip route rip`
    *   `passive-interface <interface>`

*   **`Swport Vlan Basic.pkt`:** Basic VLAN configuration.
    *   `vlan <vlan-id>`
    *   `name <vlan-name>`
    *   `interface <interface-name>`
    *   `switchport mode access`
    *   `switchport access vlan <vlan-id>`
    *  `show vlan brief`

*   **`Swport Vlan Trunking.pkt`:** Trunking configuration.
    *   `interface <interface-name>`
    *   `switchport mode trunk`
    *   `switchport trunk encapsulation dot1q`
    *   `switchport trunk allowed vlan <vlan-list>`
    *   `show interfaces trunk`

*   **`VLAN and Trunking With OSPF For 18 Subnets.pkt`:** Combines VLAN, trunking, and OSPF.

*   **`VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt`:** VLAN, trunking, VTP, OSPF, webserver, and AP.
    *   `vtp mode {server | client | transparent}`
    *   `vtp domain <domain-name>`
    *   `vtp password <password>`
    *   `ip address <ip-address> <subnet-mask>` (for interfaces, webserver)
    *   DHCP configuration (if needed).
    *  Wireless LAN Controller (WLC) and AP configuration.
*   **`HSRP.pkt` (Example):** This file simulates HSRP configuration to provide gateway redundancy.
    *   On the primary (Active) router:
        *   `interface <interface-name>`
        *   `ip address <ip-address> <subnet-mask>`
        *   `standby <group-number> ip <virtual-ip-address>`
        *   `standby <group-number> priority <priority-value>` (Higher on the primary router)
        *   `standby <group-number> preempt` (Allows higher priority router to take over)
        *   `standby <group-number> track <interface-name> [decrement-value]` (Decrease priority if the interface goes down)
    *   On the backup (Standby) router: Similar to above, but with a lower `priority`.
    *   Verification: `show standby`, `show standby brief`

*   **`Load Balancing.pkt` (Example):** *Could* contain load balancing, but specific file is needed for details.  Highly dependent on the device/software.  Examples:
    *   **Cisco Router (PBR):**
        *   `route-map <map-name> permit 10`
        *   `match ip address <access-list>`
        *   `set ip next-hop <next-hop-1> <next-hop-2>`
        *   `ip access-list extended <access-list>` (define traffic to load balance).
        *   Apply route-map to interface: `ip policy route-map <map-name>`
    *   **Dedicated Load Balancer/Software (HAProxy, Nginx):** Configuration is very different, typically in a separate configuration file.

*   **`Backup_Restore.pkt` (Example):** Simulates configuration backup/restore using TFTP.
    *   **Step 1: Configure TFTP Server:**
        *   In Packet Tracer, add a server and configure the TFTP service (enable the service).
        *   Assign an IP address to the server.
    *   **Step 2: Backup (On Router/Switch):**
        *   `copy running-config tftp` (or `copy startup-config tftp`)
        *   `Address or name of remote host []?` Enter the IP address of the TFTP server.
        *   `Destination filename [router-config]?` Enter the desired filename (or press Enter to use the default).
    *   **Step 3: Restore (On Router/Switch):**
        *   `copy tftp running-config` (or `copy tftp startup-config`)
        *   `Address or name of remote host []?` Enter the IP address of the TFTP server.
        *   `Source filename []?` Enter the name of the backed-up file.
        *   `Destination filename [running-config]?` (Press Enter)
        *   Confirm configuration overwrite (if prompted).
    *   **Note:** Ensure the router/switch can reach (ping) the TFTP server.

*   **`RADIUS.pkt` (Example):** Simulates RADIUS authentication.
    *   **Step 1: Configure RADIUS Server:**
        *   In Packet Tracer, add a server, go to Services -> AAA.
        *   Enable the RADIUS service.
        *   Add a Client: `Client Name` (any name), `Client IP` (router/switch IP), `Secret` (shared password), `Server Type` (RADIUS).
        *   Add a User: `Username`, `Password`, services (e.g., enable `PAP` or `CHAP`).
    *   **Step 2: Configure Router/Switch (RADIUS Client):**
        *   `aaa new-model` (enable AAA)
        *   `radius server <server-name>` (a name you choose)
        *   `address ipv4 <server-ip>` (RADIUS server IP)
        *   `key <shared-secret>` (matches the `Secret` on the server)
        *   `aaa authentication login default group radius local` (authenticate logins using RADIUS, fallback to local if RADIUS is down)
        *   `aaa authorization exec default group radius local` (authorize exec commands using RADIUS, fallback to local)
        *    `aaa authorization network default group radius` (Authorize other network services - if needed).
        *   `line vty 0 4`
        *     `login authentication default`
        *     `authorization exec default`  (if you want to also authorize exec)

    * **Step 3: Verification:**
        *   Try to access the router/switch using the user configured on the RADIUS server.
        *   `debug radius` (on the router/switch to see the authentication process).
        *   `show aaa servers`
## Instructions

1.  **Install Cisco Packet Tracer:** Install Cisco Packet Tracer.
2.  **Open File:** Open the relevant `.pkt` file.
3.  **Explore:** Use `show` commands (e.g., `show running-config`, `show ip interface brief`, `show vlan brief`, `show ip route`). Run `debug` commands to see detailed processes (e.g., `debug ip ospf events`, `debug radius`).
4.  **Modify and Experiment:** Change configurations, add/remove devices, and re-test.

</details>

<!-- Japanese -->
<details>
  <summary><h2>🇯🇵 日本語</h2></summary>

## 概要

このリポジトリには、Cisco ネットワークラボ用の Packet Tracer ファイル (`.pkt`) と設計ドキュメントが含まれており、以下のようなさまざまなトピックをカバーしています。

*   **Cisco Security:** Cisco ネットワークセキュリティ設定 (CCNA Security)。
*   **OSPF (Open Shortest Path First):** 基本および高度な OSPF ルーティング。
*   **RIP (Routing Information Protocol):** RIP ルーティング設定。
*   **Switchport VLAN:** 基本的な VLAN とトランキング設定。
*   **VTP (VLAN Trunking Protocol):** VTP 設定。
*   **Webserver and AP (Access Point):** Web サーバーとアクセスポイントの設定。
*   **SSH (Secure Shell):** SSH 設定 (リモートアクセス/管理、暗号化)。
*   **HSRP (Hot Standby Router Protocol):** ゲートウェイ冗長化設定により、ネットワークの可用性を向上させます。
*   **Load Balancing:** ロードバランシング設定 (トラフィック分散、可用性向上)。
*   **TFTP - バックアップ/リストア (Backup & Restore):** デバイス設定のバックアップとリストア。
*   **RADIUS (Remote Authentication Dial-In User Service):** RADIUS サーバー設定 (集中認証/認可)。

## 内容

*   **`Cisco Security Project (CCNA).pkt`:** Cisco セキュリティ設定を含む Packet Tracer ファイル。考えられるコマンド:
    *   `username <username> privilege <level> secret <password>`
    *   `enable secret <password>`
    *   `line vty 0 4`
        *   `login local`
        *   `transport input ssh`
    *   `ip access-list standard <acl-name>`
        *  `permit <ip_address> <wildcard>`
        * `deny any`
    *   `ip access-group <acl-name> in`
    *   `service password-encryption`
    *   `security passwords min-length <length>`
    *	`login block-for <seconds> attempts <number> within <seconds>`
    *	`ip ssh version 2`
    *   `crypto key generate rsa` (SSH 用の RSA キーを生成します。`modulus <bitsize>` (例: `modulus 2048`) の指定を検討してください)

*   **`OSPF Routing Basic.pkt`:** 基本的な OSPF 設定。コマンド:
    *   `router ospf <process-id>`
    *   `network <network-address> <wildcard-mask> area <area-id>`
    *   `show ip ospf neighbor`
    *   `show ip route ospf`
    *   `show ip ospf interface brief`

*   **`OSPF Routing With 18 Subnets.pkt`:** 複数のサブネットを持つ OSPF。エリア設定、再配布、デフォルトルート (必要な場合)。

*   **`Rip Routing With 22 Subnets.pkt`:** 複数のサブネットを持つ RIP。
    *   `router rip`
    *   `version 2`
    *   `network <network-address>` (クラスフル)
    *   `no auto-summary`
    *   `show ip route rip`
     *   `passive-interface <interface>`

*   **`Swport Vlan Basic.pkt`:** 基本的な VLAN 設定。
    *   `vlan <vlan-id>`
    *   `name <vlan-name>`
    *   `interface <interface-name>`
    *   `switchport mode access`
    *   `switchport access vlan <vlan-id>`
    *   `show vlan brief`

*   **`Swport Vlan Trunking.pkt`:** トランキング設定。
    *   `interface <interface-name>`
    *   `switchport mode trunk`
    *   `switchport trunk encapsulation dot1q`
    *   `switchport trunk allowed vlan <vlan-list>`
    *   `show interfaces trunk`

*   **`VLAN and Trunking With OSPF For 18 Subnets.pkt`:** VLAN、トランキング、OSPF を組み合わせたもの。

*   **`VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt`:** VLAN、トランキング、VTP、OSPF、Web サーバー、AP。
    *   `vtp mode {server | client | transparent}`
    *   `vtp domain <domain-name>`
    *   `vtp password <password>`
    *   `ip address <ip-address> <subnet-mask>` (インターフェイス、Web サーバー用)
    *   DHCP 設定 (必要な場合)。
    *   ワイヤレス LAN コントローラー (WLC) と AP の設定。

*   **`HSRP.pkt` (例):** このファイルは、ゲートウェイの冗長性を提供するための HSRP 設定をシミュレートします。
    *   プライマリ (アクティブ) ルーターの場合:
        *   `interface <interface-name>`
        *   `ip address <ip-address> <subnet-mask>`
        *   `standby <group-number> ip <virtual-ip-address>`
        *   `standby <group-number> priority <priority-value>` (プライマリルーターの方が高い)
        *   `standby <group-number> preempt` (優先度の高いルーターが引き継ぐことを許可する)
        *   `standby <group-number> track <interface-name> [decrement-value]` (インターフェースがダウンした場合に優先度を下げる)
    *   バックアップ (スタンバイ) ルーターの場合: 上記と同様ですが、`priority` は低くなります。
    *  確認： `show standby`、`show standby brief`

*   **`Load Balancing.pkt` (例):** ロードバランシングが含まれている*可能性*がありますが、詳細については特定のファイルが必要です。デバイス/ソフトウェアに大きく依存します。例:
    *   **Cisco ルーター (PBR):**
        *   `route-map <map-name> permit 10`
        *   `match ip address <access-list>`
        *   `set ip next-hop <next-hop-1> <next-hop-2>`
        *   `ip access-list extended <access-list>` (ロードバランシングするトラフィックを定義)。
        *   インターフェイスにルートマップを適用: `ip policy route-map <map-name>`
    *   **専用ロードバランサー/ソフトウェア (HAProxy、Nginx):** 設定は大きく異なり、通常は別の設定ファイルで行われます。

*   **`Backup_Restore.pkt` (例):** TFTP を使用した設定のバックアップ/リストアをシミュレートします。
    *   **ステップ 1: TFTP サーバーの設定:**
        *   Packet Tracer で、サーバーを追加し、TFTP サービスを設定します (サービスを有効にします)。
        *   サーバーに IP アドレスを割り当てます。
    *   **ステップ 2: バックアップ (ルーター/スイッチ上):**
        *   `copy running-config tftp` (または `copy startup-config tftp`)
        *   `Address or name of remote host []?` TFTP サーバーの IP アドレスを入力します。
        *   `Destination filename [router-config]?` 目的のファイル名を入力します (または、Enter キーを押してデフォルトを使用します)。
    *   **ステップ 3: リストア (ルーター/スイッチ上):**
        *   `copy tftp running-config` (または `copy tftp startup-config`)
        *   `Address or name of remote host []?` TFTP サーバーの IP アドレスを入力します。
        *   `Source filename []?` バックアップされたファイルの名前を入力します。
        *   `Destination filename [running-config]?` (Enter キーを押す)
        *   設定の上書きを確認します (プロンプトが表示された場合)。
    *   **注:** ルーター/スイッチが TFTP サーバーに到達できる (ping できる) ことを確認してください。

*   **`RADIUS.pkt` (例):** RADIUS 認証をシミュレートします。
    *   **ステップ 1: RADIUS サーバーの設定:**
        *   Packet Tracer でサーバーを追加し、[Services] -> [AAA] に移動します。
        *   RADIUS サービスを有効にします。
        *   クライアントを追加します: `Client Name` (任意の名前)、`Client IP` (ルーター/スイッチの IP)、`Secret` (共有パスワード)、`Server Type` (RADIUS)。
        *   ユーザーを追加します: `Username`、`Password`、サービス (例: `PAP` または `CHAP` を有効にする)。
    *   **ステップ 2: ルーター/スイッチ (RADIUS クライアント) の設定:**
        *   `aaa new-model` (AAA を有効にする)
        *   `radius server <server-name>` (自分で選択した名前)
        *   `address ipv4 <server-ip>` (RADIUS サーバーの IP)
        *   `key <shared-secret>` (サーバー上の `Secret` と一致する)
        *   `aaa authentication login default group radius local` (RADIUS を使用してログインを認証し、RADIUS がダウンしている場合はローカルにフォールバックする)
        *   `aaa authorization exec default group radius local`  (RADIUS を使用して exec コマンドを認証し、ローカルにフォールバックします)
        *  `aaa authorization network default group radius` (他のネットワークサービスを認証します - 必要な場合)。
        *   `line vty 0 4`
        *     `login authentication default`
        *     `authorization exec default` (exec も認証する場合)
    * **ステップ 3: 確認:**
        *    RADIUS サーバーで設定したユーザーを使用して、ルーター/スイッチにアクセスしてみてください。
        *   `debug radius` (ルーター/スイッチ上で認証プロセスを確認する)。
        *   `show aaa servers`
## 説明書

1.  **Cisco Packet Tracer のインストール:** Cisco Packet Tracer をインストールします。
2.  **ファイルを開く:** 関連する `.pkt` ファイルを開きます。
3.  **確認:** `show` コマンド (例: `show running-config`, `show ip interface brief`, `show vlan brief`, `show ip route`) を使用します。  `debug` コマンドを実行して、詳細なプロセスを確認します (例: `debug ip ospf events`, `debug radius`)。
4. **変更と実験:** 設定を変更したり、デバイスを追加/削除したり、再テストしたりします。

</details>

# Another LAB

<details>
  <summary>AccessPoint - Static Routing on MuiltiSubnets.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/7a258009-aaad-4977-992e-156fa66aa62c)

</details>



<details>
  <summary>Bigest Static Route With Server.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/49b9257e-188a-4e19-a0a0-7941df129157)


</details>



<details>
  <summary>Basic HSRP.pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/e972c42a-1351-4832-b366-9fffa2277947)

</details>



<details>
  <summary>HSRP - Ripv2 - Vlan trunking.pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/3b436fcd-331a-42d7-ad03-ae243af08258)


</details>


<details>
  <summary>HSRP - SSH - TFTP - VLAN Trunking.pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/57740d96-85b6-4c8e-b6a4-60b1e257c9ba)

</details>




<details>
  <summary>HSRP and OSPF - Ripv2 Routing with VlanTrunking .pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/fb37eff0-3f1d-420b-ad6e-d5c2b95c692c)


</details>



<details>
  <summary>SWLayer3 and SwithL3 - VTP.pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/fe91f171-6e86-4f1f-b0d6-58e91af0d6d9)


</details>


<details>
  <summary>Static Route.pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/da5df2b3-7d5b-43e0-92b0-75ab53125463)



</details>



<details>
  <summary>Static Route With 10 subnets.pkt</summary>
  
# Picture 1
![image](https://github.com/user-attachments/assets/3799540e-536d-4b44-8a0f-f655fd99165e)


</details>




<details>
  <summary>OSPF Routing With 18 Subnets.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/0b2b5ba7-dc11-49ef-ae30-32e39b633ed2)

</details>


<details>
  <summary>Rip Routing With 22 Subnets.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/3254187c-f694-43d7-99bc-886acc9dd64b)

</details>



<details>
  <summary>Swport Vlan Basic.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/3c55d47d-b7ca-4706-8ec5-5497a660a91e)

</details>



<details>
  <summary>Swport Vlan Trunking.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/3c09b939-adf5-4f5e-8538-ffd8f2b6b20c)

</details>


<details>
  <summary>VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/f25261ce-a2e4-4404-a72a-fc8964479c12)


</details>


<details>
  <summary>VLAN and Trunking With OSPF For 18 Subnets.pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/3f867478-9133-47ba-8016-f617d09ee866)


</details>



