# SPINE1

## Management Interfaces

### Management Interfaces Summary

IPv4

| Management Interface | description | VRF | IP Address | Gateway |
| -------------------- | ----------- | --- | ---------- | ------- |
| Management1 | oob_management | MGMT | 192.168.100.31/24 | 192.168.100.1 |

IPv6

| Management Interface | description | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | --- | ------------ | ------------ |
| Management1 | oob_management | MGMT | ||

### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   vrf MGMT
   ip address 192.168.100.31/24
```

## Hardware Counters

No Hardware Counters defined

## Aliases

alias shimet show bgp evpn route-type imet detail | awk '/for imet/ { print "VNI: " $7 ", VTEP: " $8, "RD: " $11 }'
alias shmacip show bgp evpn route-type mac-ip detail | awk '/for mac-ip/ { if (NF == 11) { print "RD: " $11, "VNI: " $7, "MAC: " $8 } else { print "RD: " $12, "VNI: " $7, "MAC: " $8, "IP: " $9 } }' | sed -e s/,//g
alias shprefix show bgp evpn route-type ip-prefix ipv4 detail | awk '/for ip-prefix/ { print "ip-prefix: " $7, "RD: " $10 }'

!
## TerminAttr Daemon

### TerminAttr Daemon Summary

| CV Compression | Ingest gRPC URL | Ingest Authentication Key | Smash Excludes | Ingest Exclude | Ingest VRF |  NTP VRF |
| -------------- | --------------- | ------------------------- | -------------- | -------------- | ---------- | -------- |
| gzip | 192.168.100.240:9910 | magickey04292020 | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | MGMT | MGMT |

### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -ingestgrpcurl=192.168.100.240:9910 -cvcompression=gzip -ingestauth=key,magickey04292020 -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -ingestvrf=MGMT -taillogs
   no shutdown
```

## Internal VLAN allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## IP IGMP Snooping


## Logging

No logging settings defined

## Domain Lookup


### DNS Domain Lookup Summary

| Source interface | vrf |
| ---------------- | --- |
| Management1 | MGMT  |

### DNS Domain Lookup Device Configuration

```eos
ip domain lookup vrf MGMT source-interface Management1
```

## Name Servers

### Name Servers Summary

| Name Server | Source VRF |
| ----------- | ---------- |
| 192.168.70.1 | MGMT |

### Name Servers Device Configuration

```eos
ip name-server vrf MGMT 192.168.70.1
```

## DNS Domain


### DNS domain: ohvlab.local

### DNS Domain Device Configuration

```eos
dns domain ohvlab.local
!
```

## NTP

### NTP Summary

Local Interface: Management1

VRF: MGMT


| Node | Primary |
| ---- | ------- |
| 192.232.20.87 | true |
| 216.239.35.4 | - |

### NTP Device Configuration

```eos
!
ntp local-interface vrf MGMT Management1
ntp server vrf MGMT 192.232.20.87 prefer
ntp server vrf MGMT 216.239.35.4
```

## Router L2 VPN

Router L2 VPN not defined

## SFlow

No sFlow defined

## Spanning Tree

### Spanning Tree Summary

Mode: none


### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```


TACACS Servers Not Configured


IP TACACS source interfaces not defined


### AAA Server Groups

| Server Group Name | Type  | VRF | IP address |
| ------------------| ----- | --- | ---------- |
| RADIUS-GROUP | radius |  MGMT | 192.168.100.254 |

### AAA Server Groups Device Configuration

```eos
!
aaa group server radius RADIUS-GROUP
   server 192.168.100.254 vrf MGMT
```

## AAA Authentication

### AAA Authentication Summary

| Type | Sub-type | User Stores |
| ---- | -------- | ---------- |
| Login | Default | group RADIUS-GROUP local |

### AAA Authentication Device Configuration

```eos
!
aaa authentication login default group RADIUS-GROUP local
aaa authentication dot1x default group RADIUS-GROUP
!
```

## AAA Authorization

AAA authorization not defined

## AAA Accounting

AAA accounting not defined

## Local Users

### Local Users Summary

| User | Privilege | role |
| ---- | --------- | ---- |
| admin | 15 | network-admin |
| arista | 15 | N/A |
| cvpadmin | 15 | N/A |

### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 $6$xTFjLEjlpX/ZvgNp$3ARB.DYuWuJDHzph652u7BAkyQ6jni/NZqKRUQBDJxUL83QuL6/HBY4tL/UXuKr1n00yjwNHtUBn.UbixdLai0
username arista privilege 15 secret sha512 $6$RO7KPjCB0BtlFgcd$/7Lv7Pjj3/OUOIUmqk0NmB8218tnq3Qcjb20pF4Xb3VaoMEuXShWVpFGU.YTYBuQ5.e3SXOLrIEfXpFegrQDX.
username cvpadmin privilege 15 secret sha512 $6$u5wM2GSl324m5EF0$AM98W2MI4ISBciPXm6be8Q3RTykF3dCd2W3btVvhcBBKvKHjfbkeJfesbEWMcrYlbzzZbWdBcxF6U/Pe3xBYF1
```

## VLANs

No VLANs defined

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT |  disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

## Port-Channel Interfaces

No Port-Channels defined

## Ethernet Interfaces

### Ethernet Interfaces Summary

| Interface | Description | MTU | Type | Mode | Allowed VLANs (Trunk) | Trunk Group | VRF | IP Address | Channel-Group ID | Channel-Group Type |
| --------- | ----------- | --- | ---- | ---- | --------------------- | ----------- | --- | ---------- | ---------------- | ------------------ |
| Ethernet1 | P2P_LINK_TO_LEAF1A_Ethernet1 | 9216 | routed | access | - | - | - | 10.2.1.16/31 | - | - |
| Ethernet2 | P2P_LINK_TO_LEAF2A_Ethernet1 | 9216 | routed | access | - | - | - | 10.2.1.72/31 | - | - |
| Ethernet3 | P2P_LINK_TO_LEAF2B_Ethernet1 | 9216 | routed | access | - | - | - | 10.2.1.76/31 | - | - |

*Inherited from Port-Channel Interface

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_LEAF1A_Ethernet1
   mtu 9216
   no switchport
   ip address 10.2.1.16/31
!
interface Ethernet2
   description P2P_LINK_TO_LEAF2A_Ethernet1
   mtu 9216
   no switchport
   ip address 10.2.1.72/31
!
interface Ethernet3
   description P2P_LINK_TO_LEAF2B_Ethernet1
   mtu 9216
   no switchport
   ip address 10.2.1.76/31
```

## Loopback Interfaces

### Loopback Interfaces Summary

IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | Global Routing Table | 1.1.1.1/32 |

IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | Global Routing Table | - |

### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   ip address 1.1.1.1/32
```

## VLAN Interfaces

No VLAN interfaces defined

## VXLAN Interface

No VXLAN interface defined

## Virtual Router MAC Address & Virtual Source NAT


## IPv6 Extended Access-lists

IPv6 Extended Access-lists not defined

## IPv6 Standard Access-lists

IPv6 Standard Access-lists not defined

## Extended Access-lists

Extended Access-lists not defined

## Standard Access-lists

Standard Access-lists not defined

## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Fowarding Address / Interface |
| --- | ------------------ | ----------------------------- |
| MGMT | 0.0.0.0/0 | 192.168.100.1 |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 192.168.100.1
```

## Event Handler

No Event Handler Defined

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| MGMT | False |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```

## Prefix Lists

### Prefix Lists Summary

**PL-LOOPBACKS-EVPN-OVERLAY:**

| Sequence | Action |
| -------- | ------ |
| 10 | permit 1.1.1.0/24 le 32 |

### Prefix Lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 1.1.1.0/24 le 32
```

## IPv6 Prefix Lists

IPv6 Prefix lists not defined

## IPv6 Routing

### IPv6 Routing Summary

| VRF | IPv6 Routing Enabled |
| --- | -------------------- |
| MGMT | False |

### IPv6 Routing Device Configuration

```eos
```

## MLAG

MLAG not defined

## Route Maps

### Route Maps Summary

**RM-CONN-2-BGP:**

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

### Route Maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

## Peer Filters

### Peer Filters Summary

**LEAF-AS-RANGE:**

| Sequence | Match |
| -------- | ----- |
| 10 | as-range 65001-65199 result accept |

### Peer Filters Device Configuration

```eos
!
peer-filter LEAF-AS-RANGE
   10 match as-range 65001-65199 result accept
```

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

*No device configuration required - default values

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65001|  1.1.1.1 |

| BGP Tuning |
| ---------- |
| update wait-for-convergence |
| update wait-install |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 2 ecmp 2 |

### Router BGP Peer Groups

**EVPN-OVERLAY-PEERS**:

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| next-hop unchanged | true |
| source | Loopback0 |
| bfd | true |
| ebgp multihop | 3 |
| send community | true |
| maximum routes | 0 (no limit) |

**IPv4-UNDERLAY-PEERS**:

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS |
| -------- | ---------
| 1.1.1.7 | 65002 |
| 1.1.1.21 | 65003 |
| 1.1.1.22 | 65003 |
| 10.2.1.17 | 65002 |
| 10.2.1.73 | 65003 |
| 10.2.1.77 | 65003 |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs



#### Router BGP EVPN VRFs


### Router BGP Device Configuration

```eos
!
router bgp 65001
   router-id 1.1.1.1
   update wait-for-convergence
   update wait-install
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 2 ecmp 2
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 1.1.1.7 peer group EVPN-OVERLAY-PEERS
   neighbor 1.1.1.7 remote-as 65002
   neighbor 1.1.1.21 peer group EVPN-OVERLAY-PEERS
   neighbor 1.1.1.21 remote-as 65003
   neighbor 1.1.1.22 peer group EVPN-OVERLAY-PEERS
   neighbor 1.1.1.22 remote-as 65003
   neighbor 10.2.1.17 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.2.1.17 remote-as 65002
   neighbor 10.2.1.73 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.2.1.73 remote-as 65003
   neighbor 10.2.1.77 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.2.1.77 remote-as 65003
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
      no neighbor IPv4-UNDERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
```

## Router Multicast

Routing multicast not defined

## Router PIM Sparse Mode

Router PIM sparse mode not defined

## VM Tracer Sessions

No VM tracer session defined

## Management Security

Management Security not defined

## Platform

No Platform parameters defined
