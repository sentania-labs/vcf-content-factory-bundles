# VCF Content Factory Bundles

Pre-built content bundles for **VMware Cloud Foundation (VCF) Operations** (formerly Aria Operations / vRealize Operations). Each bundle is a self-contained zip that installs dashboards, views, super metrics, custom groups, and alerts onto a VCF Ops 9.x instance — no scripting or manual configuration required.

## Available Bundles

| Bundle | Description |
|---|---|
| **Capacity Assessment** | Post-HA capacity headroom at cluster granularity, days-until-runout projections, and VM right-sizing opportunities (oversized / undersized / idle) with 95th-percentile demand justification. |
| **Environment Config Status** | VP-level environment overview — ESXi patch and version consistency, hardware vendor and BIOS firmware inventory, and capacity KPIs in a single shareable dashboard. |
| **VKS Core Consumption** | Tanzu Kubernetes (VKS) vCPU consumption broken down by workload type — supervisor control plane, worker nodes, VM service, pod VMs, vCLS — with per-vCenter rollups. |
| **VM Performance** | Per-VM performance list with CPU, memory, and readiness metrics scoped by vCenter via a resource picker. |

## Installation

Each zip contains a PowerShell install script and the content artifacts. On any machine with network access to your VCF Ops instance:

1. Download the bundle zip from the root folder in this repo (click the file, then **Download raw file**).
2. Extract and run the install script:

```powershell
Expand-Archive ".\[VCF Content Factory] Capacity Assessment.zip" -DestinationPath .\bundle
cd .\bundle
.\install.ps1
```

3. The script prompts for your VCF Ops hostname and credentials, then imports and enables all content. Each step prints `[OK]` or `[WARN]` status.

**Requirements:**
- VCF Operations 9.0 or later
- PowerShell 5.1+ (Windows) or PowerShell 7+ (cross-platform)
- An account with admin privileges on the VCF Ops instance
- Uninstall of dashboards, views, and reports requires the `admin` account specifically

## What Gets Installed

Every content object created by these bundles is prefixed with **`[VCF Content Factory]`** so you can distinguish bundle-managed content from built-in or manually created content. Dashboards are placed in the `VCF Content Factory` folder.

Each bundle zip contains individual drop-in artifacts that can also be imported manually via the VCF Ops UI (drag and drop into Administration > Content > Import):

| File | Content |
|---|---|
| `supermetric.json` | Super metric definitions |
| `Dashboard.zip` | Dashboard layout |
| `Views.zip` | List view definitions |
| `Reports.zip` | Report definitions (if included) |
| `AlertContent.xml` | Symptoms and alert definitions (if included) |
| `install.ps1` | Automated install script |
| `install.py` | Python install script (alternative) |

## Uninstall

Run the same install script with the `-Uninstall` flag:

```powershell
.\install.ps1 -Uninstall
```

This removes all content objects the bundle created. Dashboard, view, and report uninstall requires the `admin` account due to VCF Ops ownership rules.

## Compatibility

Tested on VCF Operations 9.0.2. Bundles use the standard content-zip import format and should work on any VCF Ops 9.x release. Super metric formulas use only documented DSL functions and built-in metric keys.

## Source

These bundles are built by the [VCF Content Factory](https://github.com/sentania/vcf-content-factory) framework — a YAML-driven content authoring and distribution pipeline for VCF Operations.

## License

MIT
