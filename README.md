# Cisco Lab Configurations and Network Designs ᓚᘏᗢ

# Cisco model

[Cisco Security Project (CCNA).pdf](https://github.com/user-attachments/files/19056685/Cisco.Security.Project.CCNA.pdf)



![image](https://github.com/user-attachments/assets/cdbd3e4b-6d1f-4ee6-9bca-18710c01608a)


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

# LAB
<details>
  <summary>Cisco Security Project (CCNA).pkt</summary>

# Picture 1
![image](https://github.com/user-attachments/assets/05e84cb1-5fb4-4f66-b3a0-8b463bec4d99)
![image](https://github.com/user-attachments/assets/2751b086-66d1-4640-ad0f-8a34fe6bda64)

</details>


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



