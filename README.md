# Cisco Lab Configurations and Network Designs

<!-- Vietnamese -->
<details>
  <summary>🇻🇳 Tiếng Việt</summary>

## Giới thiệu

Repository này chứa các file cấu hình (packet tracer files - `.pkt`) và tài liệu thiết kế cho các bài lab mạng Cisco, bao gồm nhiều chủ đề như:

*   **Cisco Security:** Các cấu hình liên quan đến bảo mật mạng Cisco (có thể là các bài lab về CCNA Security).
*   **OSPF (Open Shortest Path First):** Cấu hình định tuyến OSPF cơ bản và nâng cao (với nhiều subnet).
*   **RIP (Routing Information Protocol):** Cấu hình định tuyến RIP.
*   **Switchport VLAN:** Cấu hình VLAN cơ bản và trunking trên switch.
*   **VTP (VLAN Trunking Protocol):** Cấu hình VTP để quản lý VLAN tập trung.
*   **Webserver and AP (Access Point):** Cấu hình tích hợp webserver và access point.

## Nội dung

*   **`Cisco Security Project (CCNA).pkt`:**  File Packet Tracer chứa các cấu hình bảo mật Cisco (có thể liên quan đến CCNA Security).  Các lệnh cấu hình có thể bao gồm:
    *   `username <username> privilege <level> secret <password>` (Tạo user)
    *   `enable secret <password>` (Đặt mật khẩu enable)
    *   `line vty 0 4`
    *   `login local` (Yêu cầu đăng nhập bằng user local)
    *   `transport input ssh` (Chỉ cho phép kết nối SSH)
    *   `ip access-list standard <acl-name>` (Tạo access list)
    *   `ip access-group <acl-name> in` (Áp dụng access list vào interface)
    *   `service password-encryption`
    *   `security passwords min-length <length>`
    *	`login block-for <seconds> attempts <number> within <seconds>`
  	*	`ip ssh version 2`
*   **`OSPF Routing Basic.pkt`:** Cấu hình OSPF cơ bản. Các lệnh:
    *   `router ospf <process-id>`
    *   `network <network-address> <wildcard-mask> area <area-id>`
    *   `show ip ospf neighbor` (Kiểm tra neighbor)
    *   `show ip route ospf` (Xem route OSPF)
*   **`OSPF Routing With 18 Subnets.pkt`:** Cấu hình OSPF với nhiều subnet.  Các lệnh tương tự như trên, nhưng có thể có cấu hình area phức tạp hơn.
*   **`Rip Routing With 22 Subnets.pkt`:** Cấu hình RIP với nhiều subnet.  Các lệnh:
    *   `router rip`
    *   `version 2`
    *   `network <network-address>` (Chú ý: RIP sử dụng classful network address)
    *   `no auto-summary` (Rất quan trọng khi dùng RIPv2)
    *   `show ip route rip` (Xem route RIP)
*   **`Swport Vlan Basic.pkt`:** Cấu hình VLAN cơ bản trên switch.  Các lệnh:
    *   `vlan <vlan-id>`
    *   `name <vlan-name>`
    *   `interface <interface-name>`
    *   `switchport mode access`
    *   `switchport access vlan <vlan-id>`
    *   `show vlan brief`
*   **`Swport Vlan Trunking.pkt`:** Cấu hình trunking trên switch.  Các lệnh:
    *   `interface <interface-name>`
    *   `switchport mode trunk`
    *   `switchport trunk encapsulation dot1q`
    *   `switchport trunk allowed vlan <vlan-list>`
    *   `show interfaces trunk`
*   **`VLAN and Trunking With OSPF For 18 Subnets.pkt`:** Kết hợp cấu hình VLAN, trunking, và OSPF.
*   **`VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt`:** Cấu hình toàn diện, bao gồm VLAN, trunking, VTP, OSPF, webserver, và access point.  Các lệnh bổ sung có thể bao gồm:
    *   `vtp mode {server | client | transparent}`
    *   `vtp domain <domain-name>`
    *   `vtp password <password>`
    *   `ip address <ip-address> <subnet-mask>` (Cấu hình IP cho interface, webserver)
    * Cấu hình DHCP pool, cấu hình WLC, và cấu hình AP (tùy thuộc vào mô phỏng).

## Hướng dẫn

1.  **Cài đặt Cisco Packet Tracer:** Bạn cần cài đặt Cisco Packet Tracer để mở và xem các file `.pkt`.
2.  **Mở file:** Mở file `.pkt` tương ứng trong Packet Tracer.
3.  **Khám phá cấu hình:** Sử dụng các lệnh `show` để xem cấu hình của các thiết bị (router, switch).  Ví dụ: `show running-config`, `show ip interface brief`, `show vlan brief`, `show ip route`, v.v.

</details>

<!-- English -->
<details>
  <summary>🇬🇧 English</summary>

## Introduction

This repository contains Packet Tracer files (`.pkt`) and design documents for Cisco network labs, covering various topics such as:

*   **Cisco Security:** Configurations related to Cisco network security (possibly CCNA Security labs).
*   **OSPF (Open Shortest Path First):** Basic and advanced OSPF routing configurations (with multiple subnets).
*   **RIP (Routing Information Protocol):** RIP routing configuration.
*   **Switchport VLAN:** Basic VLAN and trunking configurations on switches.
*   **VTP (VLAN Trunking Protocol):** VTP configuration for centralized VLAN management.
*   **Webserver and AP (Access Point):** Integrated webserver and access point configuration.

## Contents

*   **`Cisco Security Project (CCNA).pkt`:**  Packet Tracer file containing Cisco security configurations (potentially related to CCNA Security).  Possible commands include:
    *   `username <username> privilege <level> secret <password>`
    *   `enable secret <password>`
    *   `line vty 0 4`
    *   `login local`
    *   `transport input ssh`
    *   `ip access-list standard <acl-name>`
    *   `ip access-group <acl-name> in`
    *   `service password-encryption`
    *   `security passwords min-length <length>`
    * `login block-for <seconds> attempts <number> within <seconds>`
    * `ip ssh version 2`
*   **`OSPF Routing Basic.pkt`:** Basic OSPF configuration. Commands:
    *   `router ospf <process-id>`
    *   `network <network-address> <wildcard-mask> area <area-id>`
    *   `show ip ospf neighbor`
    *   `show ip route ospf`
*   **`OSPF Routing With 18 Subnets.pkt`:** OSPF configuration with multiple subnets. Similar commands as above, but may involve more complex area configurations.
*   **`Rip Routing With 22 Subnets.pkt`:** RIP configuration with multiple subnets. Commands:
    *   `router rip`
    *   `version 2`
    *   `network <network-address>` (Note: RIP uses classful network addresses)
    *   `no auto-summary` (Crucial when using RIPv2)
    *   `show ip route rip`
*   **`Swport Vlan Basic.pkt`:** Basic VLAN configuration on a switch. Commands:
    *   `vlan <vlan-id>`
    *   `name <vlan-name>`
    *   `interface <interface-name>`
    *   `switchport mode access`
    *   `switchport access vlan <vlan-id>`
    * `show vlan brief`
*   **`Swport Vlan Trunking.pkt`:** Trunking configuration on a switch.  Commands:
    *   `interface <interface-name>`
    *   `switchport mode trunk`
    *   `switchport trunk encapsulation dot1q`
    *   `switchport trunk allowed vlan <vlan-list>`
    *   `show interfaces trunk`
*   **`VLAN and Trunking With OSPF For 18 Subnets.pkt`:** Combines VLAN, trunking, and OSPF configurations.
*   **`VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt`:** Comprehensive configuration, including VLAN, trunking, VTP, OSPF, webserver, and access point.  Additional commands may include:
    *   `vtp mode {server | client | transparent}`
    *   `vtp domain <domain-name>`
    *   `vtp password <password>`
    *   `ip address <ip-address> <subnet-mask>` (IP configuration for interfaces, webserver)
    *  DHCP pool configuration, WLC configuration, and AP configuration (depending on the simulation).

## Instructions

1.  **Install Cisco Packet Tracer:** You need to install Cisco Packet Tracer to open and view the `.pkt` files.
2.  **Open the file:** Open the corresponding `.pkt` file in Packet Tracer.
3.  **Explore the configuration:** Use `show` commands to view the configuration of the devices (routers, switches).  For example: `show running-config`, `show ip interface brief`, `show vlan brief`, `show ip route`, etc.

</details>

<!-- Japanese -->
<details>
  <summary>🇯🇵 日本語</summary>

## 概要

このリポジトリには、以下のようなさまざまなトピックをカバーする Cisco ネットワークラボ用の Packet Tracer ファイル (`.pkt`) と設計ドキュメントが含まれています。

*   **Cisco Security:** Cisco ネットワークセキュリティに関連する設定 (CCNA Security ラボの可能性があります)。
*   **OSPF (Open Shortest Path First):** 基本および高度な OSPF ルーティング設定 (複数のサブネットを使用)。
*   **RIP (Routing Information Protocol):** RIP ルーティング設定。
*   **Switchport VLAN:** スイッチ上の基本的な VLAN およびトランキング設定。
*   **VTP (VLAN Trunking Protocol):** 一元化された VLAN 管理のための VTP 設定。
*   **Webserver and AP (Access Point):** 統合された Web サーバーとアクセスポイントの設定。

## 内容

*   **`Cisco Security Project (CCNA).pkt`:** Cisco セキュリティ設定を含む Packet Tracer ファイル (CCNA Security に関連する可能性があります)。考えられるコマンドは次のとおりです。
    *   `username <username> privilege <level> secret <password>`
    *   `enable secret <password>`
    *   `line vty 0 4`
    *   `login local`
    *   `transport input ssh`
    *   `ip access-list standard <acl-name>`
    *   `ip access-group <acl-name> in`
    *   `service password-encryption`
    *   `security passwords min-length <length>`
    *   `login block-for <seconds> attempts <number> within <seconds>`
    *	`ip ssh version 2`
*   **`OSPF Routing Basic.pkt`:** 基本的な OSPF 設定。コマンド:
    *   `router ospf <process-id>`
    *   `network <network-address> <wildcard-mask> area <area-id>`
    *   `show ip ospf neighbor`
    *   `show ip route ospf`
*   **`OSPF Routing With 18 Subnets.pkt`:** 複数のサブネットを使用した OSPF 設定。上記と同様のコマンドですが、より複雑なエリア設定が含まれる場合があります。
*   **`Rip Routing With 22 Subnets.pkt`:** 複数のサブネットを使用した RIP 設定。コマンド:
    *   `router rip`
    *   `version 2`
    *   `network <network-address>` (注: RIP はクラスフルネットワークアドレスを使用します)
    *   `no auto-summary` (RIPv2 を使用する場合は重要)
    *   `show ip route rip`
*   **`Swport Vlan Basic.pkt`:** スイッチ上の基本的な VLAN 設定。コマンド:
    *   `vlan <vlan-id>`
    *   `name <vlan-name>`
    *   `interface <interface-name>`
    *   `switchport mode access`
    *   `switchport access vlan <vlan-id>`
    *   `show vlan brief`
*   **`Swport Vlan Trunking.pkt`:** スイッチ上のトランキング設定。コマンド:
    *   `interface <interface-name>`
    *   `switchport mode trunk`
    *   `switchport trunk encapsulation dot1q`
    *   `switchport trunk allowed vlan <vlan-list>`
    *   `show interfaces trunk`
*   **`VLAN and Trunking With OSPF For 18 Subnets.pkt`:** VLAN、トランキング、および OSPF 設定を組み合わせたもの。
*   **`VLAN Trunking with VTP - OSPF - Web and AP For 24 Subnets.pkt`:** VLAN、トランキング、VTP、OSPF、Web サーバー、およびアクセスポイントを含む包括的な設定。追加のコマンドには、次のものが含まれる場合があります。
    *   `vtp mode {server | client | transparent}`
    *   `vtp domain <domain-name>`
    *   `vtp password <password>`
    *   `ip address <ip-address> <subnet-mask>` (インターフェイス、Web サーバーの IP 設定)
    *   DHCP プール設定、WLC 設定、および AP 設定 (シミュレーションによって異なります)。

## 説明書

1.  **Cisco Packet Tracer のインストール:** `.pkt` ファイルを開いて表示するには、Cisco Packet Tracer をインストールする必要があります。
2.  **ファイルを開く:** Packet Tracer で対応する `.pkt` ファイルを開きます。
3.  **設定の確認:** `show` コマンドを使用して、デバイス (ルーター、スイッチ) の設定を表示します。例: `show running-config`, `show ip interface brief`, `show vlan brief`, `show ip route` など。

</details>
