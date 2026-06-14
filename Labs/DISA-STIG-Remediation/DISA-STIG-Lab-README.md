# DISA STIG Vulnerability Remediation Lab

**Category:** Vulnerability Management / Compliance  
**Tools Used:** Microsoft Azure · Windows 11 VM · Tenable Nessus · PowerShell · DISA STIGs  
**Date Completed:** 06/13/2026
**Status:** ✅ Complete

\---

## Overview

A Windows 11 virtual machine was deployed in Microsoft Azure, intentionally misconfigured via PowerShell to introduce STIG-relevant vulnerabilities, scanned with Tenable Nessus using a DISA STIG audit template, and then manually remediated. A follow-up rescan was conducted to validate findings.

\---

## Tools \& Technologies

|Tool|Purpose|
|-|-|
|Microsoft Azure|Cloud hosting for the Windows 11 VM|
|Windows 11|Target system being scanned and hardened|
|PowerShell|Used to introduce vulnerabilities onto the VM|
|Tenable Nessus|Vulnerability scanner running DISA STIG audit policy|
|DISA STIGs|Security benchmarks used to evaluate compliance|

\---

## Lab Steps

1. Spun up a Windows 11 VM in Microsoft Azure
2. Prompted Claude (AI) to generate a PowerShell script that introduces STIG-relevant vulnerabilities
3. Executed the PowerShell script on the Windows 11 VM via RDP
4. Created a DISA STIG scan template in Tenable Nessus
5. Ran a credentialed scan against the Windows 11 VM
6. Analyzed scan findings and manually remediated 12 identified STIG controls

\---

## Remediated STIG Findings

|STIG ID|Finding|Remediation|
|-|-|-|
|WN11-00-000090|Accounts must be configured to require password expiration|Unchecked "Password never expires" for all active accounts via Computer Management > Local Users and Groups > Users|
|WN11-AC-000005|Account lockout duration must be 15 minutes or greater|Set Account lockout duration to 20 minutes via Computer Configuration > Windows Settings > Security Settings > Account Lockout Policy|
|WN11-AC-000010|Bad logon attempts must be configured to three or less|Set Account lockout threshold to 3 invalid logon attempts via Computer Configuration > Account Lockout Policy|
|WN11-AU-000582|Windows 11 must audit file system successes|Enabled Audit File System Success via Computer Configuration > Advanced Audit Policy Configuration > Object Access|
|WN11-CC-000040|Insecure logons to an SMB server must be disabled|Set "Enable insecure guest logons" to Disabled via Computer Configuration > Administrative Templates > Network > Lanman Workstation|
|WN11-CC-000090|Group Policy objects must be reprocessed even if unchanged|Enabled "Configure registry policy processing" with "Process even if GPO has not changed" via Computer Configuration > Administrative Templates > System > Group Policy|
|WN11-CC-000110|Printing over HTTP must be prevented|Set "Turn off printing over HTTP" to Enabled via Computer Configuration > Administrative Templates > System > Internet Communication Management|
|WN11-CC-000206|Windows Update must not obtain updates from other PCs on the internet|Set Delivery Optimization Download Mode to HTTP only (0) via Computer Configuration > Administrative Templates > Windows Components > Delivery Optimization|
|WN11-CC-000280|RDS must always prompt a client for passwords upon connection|Set "Always prompt for password upon connection" to Enabled via Computer Configuration > Administrative Templates > Remote Desktop Services > Security|
|WN11-CC-000315|Windows Installer must not always install with elevated privileges|Set "Always install with elevated privileges" to Disabled via Computer Configuration > Administrative Templates > Windows Components > Windows Installer|
|WN11-SO-000010|The built-in guest account must be disabled|Disabled the Guest account via Computer Management > Local Users and Groups > Users > Guest Properties|
|WN11-SO-000270|UAC must run all administrators in Admin Approval Mode|Set "User Account Control: Run all administrators in Admin Approval Mode" to Enabled via Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options|

\---

## Scan Results Comparison

|Metric|Initial Scan|Rescan|
|-|-|-|
|Failed Audits|163|161|
|STIGs Targeted \& Remediated|—|12 ✅|

> All 12 targeted STIG controls were confirmed as failing in the initial scan and confirmed as passing on rescan. The net reduction of only 2 is due to 10 additional audit failures detected during the rescan that were not caught initially. This reflects a real-world scenario where vulnerability remediation is a continuous process — resolving known findings can uncover previously undetected issues requiring further investigation.

\---

