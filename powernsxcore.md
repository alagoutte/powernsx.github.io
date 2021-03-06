---
permalink: /powernsxcore/
---

# PowerNSX Core

Experimental support for PowerShell Core is now available in the master branch of PowerNSX.  The master branch is where all development occurs, and *is not guaranteed to be stable*.

If you are interested in PowerNSX running on PowerShell core, then please try it out and let us know of the good, the bad and the ugly, but be mindful that limited testing has occured, and issues are likely!

## Installing PowerNSX on PowerShell Core

The PowerNSX installation script now supports all PowerShell Core platforms.  See [Install](/install/) for detailed instructions for your platform.

## Usage

Usage should mirror that of PowerNSX on Windows.  Any differences or errors should be reported via the project issues page at [Issues](https://github.com/vmware/powernsx/issues).

Start powershell, and the module will be automatically loaded when any PowerNSX command is invoked.  In addition, it will also automatically load the PowerCLI.ViCore and PowerCLI.Vds modules.

*If either the PowerCLI.ViCore or PowerCLI.Vds modules do not load, the PowerNSX module will fail to load also.*

## Troubleshooting

If you need to troubleshoot module load issues, try manually loading PowerCLI.ViCore and PowerCLI.Vds first and resolve any issues here before attempting to load PowerNSX.

## Known Issues

There are several known isuses that affect PowerNSX Core usage.  See the issues page [Issues](https://github.com/vmware/powernsx/issues) for up to date information.

* PowerNSX cmdlets typically emit progress dialogs.  On PowerShell Core, these have a nasty habbit of overwriting output.  As a result, progress reporting is disabled by default on PowerNSX Core.  If you want to revert this, set the $PowerNsxConfiguration.ProgressReporting = $true.  Currently this is not persistent between PowerShell sessions.  This will be improved upon in future commits.  To disable progress reporting globally, set $ProgressPreference = "SilentlyContinue"
* Significant differences in the dotNet classes backing invoke-restmethod and invoke-webrequest (the cmdlets used internally by PowerNSX to interact with the NSX API) mean that there are some rough edges and limitations that exist on the PowerShell Core versions of these cmdlets.  Over time, it is expected that these will be resolved, but in order to support PowerNSX Core at this point, the internal functions used by PowerNSX to interact with NSX have been refactored / rewritten significantly to support PowerShell Core.  As a result, you may encounter differences in the way errors are returned and in some cases, some commands may fail unexpectedly.  Again - please report these occurences along with steps to reproduce via the issues page at [Issues](https://github.com/vmware/powernsx/issues).
