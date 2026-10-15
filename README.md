# Nexus Freight: Windows Server 2019 Infrastructure Design (ITCOA)

Windows Server infrastructure design and lab implementation for **Nexus Freight**, a fictional freight company with a head office in Gqeberha and branches in Bloemfontein and Polokwane. Completed as an individual assessment for the ITCOA module at Eduvos.

> **Full write-up:** [itcoa-nexus-freight-assessment.pdf](itcoa-nexus-freight-assessment.pdf)

## Scenario in brief
Nexus Freight (~305 staff, 3 sites) is replacing a single legacy server that failed and caused a week-long outage. The business also had ransomware near-misses and must protect POPIA-regulated Finance data, all on a tight budget with a 3-person IT team.

## What the design covers

| Area | Highlights |
|---|---|
| **Licensing** | Windows Server 2019 Datacenter on the Hyper-V hosts, per-user CALs |
| **Active Directory** | 2 writable DCs at HQ, RODC at Polokwane, 3 AD sites mirroring the subnets, hub-and-spoke site links |
| **DNS** | AD-integrated internal zone, separate public zone, CAA record, split-brain DNS evaluated |
| **DHCP** | Bloemfontein scope with reservations, Hot Standby failover via relay |
| **Group Policy** | Baseline, Finance, Workstation and Branch GPOs; Policy vs Preference decisions |
| **PKI and remote access** | Two-tier AD CS, public CA for the portal, Always On VPN |
| **Security hardening** | Defender and Controlled Folder Access, firewall rules, BitLocker, fine-grained password policy |
| **Server Core and automation** | Server Core for utility servers, PowerShell share provisioning, DSC |
| **High availability** | NLB for the web tier, failover clustering for file services, S2D and Storage Replica |
| **Containers** | Hyper-V container isolation for a third-party vendor image |
| **Virtualisation** | Virtual switches, Shielded VMs, Linux appliance VM, backup strategy |
| **Troubleshooting, risks, migration** | Task Manager to PerfMon workflow, risk register, phased migration with rollback |

## Lab implementation (Question 5)
Built in Oracle VirtualBox on a Windows Server 2019 VM named `NXS-DC-01`, domain `nexusfreight.local`.

### 5.1 Installation
| | |
|---|---|
| ![Windows Server 2019 setup](screenshots/5.1-01-windows-server-2019-setup.png) | ![Server Manager](screenshots/5.1-02-server-manager-local-server.png) |

### 5.2 Roles, OUs and groups
| | |
|---|---|
| ![AD DS role installed](screenshots/5.2-01-adds-role-installed.png) | ![DHCP role installed](screenshots/5.2-02-dhcp-role-installed.png) |
| ![OU structure](screenshots/5.2-03-ou-structure-nexus.png) | ![Finance-Users group](screenshots/5.2-04-finance-users-group.png) |

![DHCP console](screenshots/5.2-05-dhcp-console.png)

### 5.3 DHCP: Bloemfontein scope (172.18.20.0/24)
| | |
|---|---|
| ![Scope](screenshots/5.3-01-bloemfontein-scope.png) | ![Address pool](screenshots/5.3-02-address-pool.png) |

![Reservation](screenshots/5.3-03-reservation.png)

### 5.4 Group Policy
| | |
|---|---|
| ![GPOs linked to Workstation OU](screenshots/5.4-01-gpo-linked-workstation-ou.png) | ![GPO details](screenshots/5.4-02-gpo-details.png) |

## Repository contents
```
.
├── README.md
├── itcoa-nexus-freight-assessment.pdf
└── screenshots/
```

## Notes
This repository is a personal portfolio record of my own coursework. Please don't reuse it for your own submissions.
