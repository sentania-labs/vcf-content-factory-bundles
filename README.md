# VCF Content Factory Bundles

Pre-built content bundles for **VMware Cloud Foundation (VCF) Operations** (formerly Aria Operations / vRealize Operations). Each bundle is a self-contained zip that installs dashboards, views, super metrics, custom groups, and alerts onto a VCF Ops 9.x instance — no scripting or manual configuration required.

## Factory-Generated Bundles

These bundles are authored and distributed by the VCF Content Factory. All content objects carry the `[VCF Content Factory]` prefix to distinguish them from built-in or manually created content.

| Bundle | Description |
|---|---|
| **Capacity Assessment** | Post-HA capacity headroom at cluster granularity, days-until-runout projections, and VM right-sizing opportunities (oversized / undersized / idle) with 95th-percentile demand justification. |
| **Environment Config Status** | VP-level environment overview — ESXi patch and version consistency, hardware vendor and BIOS firmware inventory, and capacity KPIs in a single shareable dashboard. |
| **VKS Core Consumption** | Tanzu Kubernetes (VKS) vCPU consumption broken down by workload type — supervisor control plane, worker nodes, VM service, pod VMs, vCLS — with per-vCenter rollups. |

## Community Bundles

These bundles are not authored by the VCF Content Factory. They are sourced from the community and distributed here as a convenience — the Factory's packaging tooling wraps them in compatible install/uninstall scripts, but authorship and content ownership remain with the original authors.

### IDPS Planner 3.2

**Author:** Geoff Shukin  
**Source:** [Broadcom Community](https://community.broadcom.com/applications-networking-security/viewdocument/operations-dashboard-version-3-2?CommunityKey=a802a279-130e-43e5-a23d-f522bc290b5c&tab=librarydocuments)  
**Original upload:** March 18, 2026

A capacity planning tool for sizing hosts and clusters that will run vDefend ATP Intrusion Detection and Prevention System (IDPS) workloads. Visualizes host- and cluster-level network metrics from a VM workload perspective.

**Contents:**
- 1 dashboard — IDPS Planner
- 5 list views — IDPS Planner Host Metrics, IDPS Planner VM Metrics, and three selection widgets (Datacenter, Cluster, vCenter)
- 6 super metrics — host-level network rollups (peak usage, peak packets/sec, transmit, receive, total packets/sec)

**Packaging note:** Original upstream artifacts are preserved verbatim in the zip under `bundles/idps-planner-3.2/ORIGINAL/`, including the PDF installation guide. Two technical changes were made for cross-instance portability: the dashboard's embedded `userId` is substituted at install time, and one super metric name was corrected (double-space to single-space) with the author's permission.

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
