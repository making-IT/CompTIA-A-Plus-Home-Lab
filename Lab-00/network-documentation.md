# Home Lab Network Documentation

## Network Architecture

### Host Machine
- Hostname: [YOUR-COMPUTER-NAME]
- Host OS: Windows [10/11]
- Host-Only IP: 192.168.56.1

### Networks
| Network Name | Type | Subnet | Purpose |
|---|---|---|---|
| Default NAT | NAT | 10.0.2.0/24 | Internet access for VMs |
| LabLAN | Host-Only | 192.168.56.0/24 | Internal lab network |

### IP Address Assignments
| Hostname | Role | IP Address | OS | Status |
|---|---|---|---|---|
| Host | Physical Machine | 192.168.56.1 | Windows | Active |
| osTicket-Server | Help Desk Server | 192.168.56.10 | Ubuntu Server 22.04 | Pending |
| Win10-PC01 | Client Workstation | 192.168.56.100 | Windows 10 | Pending |
| Win11-PC01 | Client Workstation | 192.168.56.101 | Windows 11 | Pending |
| Ubuntu-PC01 | Client Workstation | 192.168.56.102 | Ubuntu 22.04 | Pending |
| Mint-PC01 | Client Workstation | 192.168.56.103 | Linux Mint 21 | Pending |

               ┌──────────────┐
               │   INTERNET   │
               └──────┬───────┘
                      │
          ┌───────────┴───────────┐
          │   NAT (10.0.2.0/24)   │   ← Each VM gets its own NAT
          │   Gateway: 10.0.2.2   │     for internet access
          └───────────┬───────────┘
                      │
    ┌─────┬─────┬─────┼─────┬─────┐
    │     │     │     │     │     │
  ┌─┴─┐┌─┴─┐┌─┴─┐┌──┴─┐┌─┴──┐┌─┴──┐
  │SVR ││W10 ││W11 ││UBU ││MINT││HOST│
  │ .10││.100││.101││.102││.103││ .1 │
  └─┬──┘└─┬──┘└─┬──┘└─┬──┘└─┬──┘└─┬──┘
    │     │     │     │     │     │
  ┌─┴─────┴─────┴─────┴─────┴─────┴──┐
  │   Host-Only (192.168.56.0/24)     │  ← All VMs + Host
  │   "Office LAN" simulation         │    communicate here
  └────────────────────────────────────┘