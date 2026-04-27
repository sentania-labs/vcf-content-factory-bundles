# VCF Content Factory Bundles

Pre-built content bundles for **VMware Cloud Foundation (VCF) Operations** (formerly Aria Operations / vRealize Operations). Each bundle is a self-contained zip that installs dashboards, views, super metrics, custom groups, and alerts onto a **VCF Operations 9.x** or **Aria Operations 8.18** instance — no scripting or manual configuration required.

<!-- AUTO:START release-catalog -->

## Bundles
_No releases yet._

## Dashboards
| Name | Released | Description | Download | Install |
|---|---|---|---|---|
| demand-driven-capacity-v2 | 2026-04-27 | Demand-driven capacity planning v2. | [Download](dashboards/demand-driven-capacity-v2.zip) | `python3 install.py` |

## Views
_No releases yet._

## Super Metrics
_No releases yet._

## Custom Groups
_No releases yet._

## Reports
_No releases yet._

## Management Packs
_No releases yet._

## Retired
_No retired artifacts._
<!-- AUTO:END -->

## Installation

Each zip contains both a Python and a PowerShell install script, content artifacts, and a README with detailed instructions. On any machine with network access to your VCF Ops instance:

1. Download the bundle zip file from the root of this repo.
2. Extract the zip and run the install script for your platform — **Python** (`python3 install.py`) or **PowerShell** (`.\install.ps1`).
3. The script prompts for your VCF Ops hostname and credentials, then imports and enables all content.

See the README inside each bundle for full usage details, uninstall instructions, and manual import options.

**Requirements:**
- VCF Operations 9.x **or** Aria Operations 8.18
- Python 3.9+ **or** PowerShell 5.1+ (Windows) / PowerShell 7+ (cross-platform)
- An account with admin privileges on the VCF Ops instance
- Uninstall of dashboards, views, and reports requires the `admin` account specifically

> **Policy enablement caveat.** The install script enables imported super
> metrics on the **Default Policy** only. If your deployment uses
> non-default, non-inheriting policies, you may need to manually enable the
> imported super metrics in those policies — otherwise dashboard cells and
> view columns that depend on those metrics will appear blank for resources
> scoped under those policies. Check `Administration > Policies` after
> install to confirm enablement on every policy that needs to see the
> bundle's data.

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

## About Third-Party Content

The catalog above includes both **factory-native** content (authored in the [VCF Content Factory](https://github.com/sentania-labs/vcf-content-factory) repo) and **third-party** content (extracted from community-built dashboards and repackaged here for distribution). Third-party items live under the `ThirdPartyContent/` subtree and carry explicit **License** and **Authors** columns in the catalog.

**What the factory adds to third-party content** — the original dashboards, views, and super metrics are unchanged from their authors' designs. The factory's contribution is the install/uninstall machinery wrapped around them:

- A **scripted installer** that imports the dashboard, syncs its dependent views and super metrics, enables the SMs in the Default Policy, and turns on any required built-in (OOTB) metrics that aren't enabled by default.
- A **symmetric uninstaller** that reverses every step cleanly.
- **Dependency walking** so the bundle ships as a single self-contained zip — consumers don't need to chase or hand-import individual artifacts.
- The same Policy-enablement caveat applies as for factory-native content (see Requirements above).

Original authors retain all rights to dashboard design, queries, and view layout. License terms are per item.

## Compatibility

Targets **VCF Operations 9.x** and **Aria Operations 8.18+**. Bundles use the standard content-zip import format and rely only on documented DSL functions and built-in metric keys — both stable across the two releases. Authored and primarily verified on VCF Operations 9.0.2; Aria Operations 8.18 verification is being added per dashboard, starting with VKS Core Consumption. Per-dashboard verification status will appear in each release's notes.

## Source

These bundles are built by the [VCF Content Factory](https://github.com/sentania-labs/vcf-content-factory) framework — a YAML-driven content authoring and distribution pipeline for VCF Operations.

## License

MIT
