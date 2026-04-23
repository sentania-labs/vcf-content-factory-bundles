# VCF Content Factory Bundles

Pre-built content bundles for **VMware Cloud Foundation (VCF) Operations** (formerly Aria Operations / vRealize Operations). Each bundle is a self-contained zip that installs dashboards, views, super metrics, custom groups, and alerts onto a VCF Ops 9.x instance — no scripting or manual configuration required.

## Available Bundles

| Bundle | Description |
|---|---|
| **Capacity Assessment** | Post-HA capacity headroom at cluster granularity, days-until-runout projections, and VM right-sizing opportunities (oversized / undersized / idle) with 95th-percentile demand justification. |
| **Environment Config Status** | VP-level environment overview — ESXi patch and version consistency, hardware vendor and BIOS firmware inventory, and capacity KPIs in a single shareable dashboard. |
| **VKS Core Consumption** | Tanzu Kubernetes (VKS) vCPU consumption broken down by workload type — supervisor control plane, worker nodes, VM service, pod VMs, vCLS — with per-vCenter rollups. |
| **VM Performance** | Cluster-level VM performance indicators — average VM CPU usage, worst-case CPU ready, worst-case memory contention, powered-on VM count, and allocated vCPU rollup — plus a snapshot health metric flagging VMs whose snapshots exceed provisioned disk size. Includes a per-vCenter list view and performance dashboard. |

## Installation

Each zip contains both a Python and a PowerShell install script, content artifacts, and a README with detailed instructions. On any machine with network access to your VCF Ops instance:

1. Download the bundle zip file from the root of this repo.
2. Extract the zip and run the install script for your platform — **Python** (`python3 install.py`) or **PowerShell** (`.\install.ps1`).
3. The script prompts for your VCF Ops hostname and credentials, then imports and enables all content.

See the README inside each bundle for full usage details, uninstall instructions, and manual import options.

**Requirements:**
- VCF Operations 9.0 or later
- Python 3.9+ **or** PowerShell 5.1+ (Windows) / PowerShell 7+ (cross-platform)
- An account with admin privileges on the VCF Ops instance
- Uninstall of dashboards, views, and reports requires the `admin` account specifically

## What Gets Installed

Every content object created by these bundles is prefixed with **`[VCF Content Factory]`** so you can distinguish bundle-managed content from built-in or manually created content. Dashboards are placed in the `VCF Content Factory` folder.

Each bundle zip contains drop-in artifacts for manual import and automated install scripts:

**Drop-in artifacts** (can be imported manually via the VCF Ops UI — navigate to the matching UI location and drag the file in):

| File | VCF Ops UI location |
|---|---|
| `supermetric.json` | Administration > Super Metrics > Import |
| `Views.zip` | Manage > Views > Import |
| `Dashboard.zip` | Manage > Dashboards > Import |
| `AlertContent.xml` | Alerts > Alert Definitions > Import |
| `Reports.zip` | Administration > Content > Reports > Import (if included) |

**Install scripts:**

| File | Purpose |
|---|---|
| `install.py` | Automated install (Python 3.9+) |
| `install.ps1` | Automated install (PowerShell 5.1+ / 7+) |

## Uninstall

Run the install script with the uninstall flag: `python3 install.py --uninstall` or `.\install.ps1 -Uninstall`. This removes all content objects the bundle created. Dashboard, view, and report uninstall requires the `admin` account due to VCF Ops ownership rules.

## Compatibility

Tested on VCF Operations 9.0.2. Bundles use the standard content-zip import format and should work on any VCF Ops 9.x release. Super metric formulas use only documented DSL functions and built-in metric keys.

## Source

These bundles are built by the [VCF Content Factory](https://github.com/sentania-labs/vcf-content-factory) framework — a YAML-driven content authoring and distribution pipeline for VCF Operations.

## License

MIT
