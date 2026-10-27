# Troubleshooting Log

During the build and configuration of this home lab, several technical issues were encountered. This document details the symptoms, attempted solutions, and final resolutions.

\---

### Issue 1: Python Environment Variable Conflict

* **Symptom:** VirtualBox failed to recognize installed Python dependencies required for the environment.
* **Root Cause:** A duplicate, older version of Python was installed on the host OS. The system PATH environment variable was pointing to the old version rather than the active installation.
* **Resolution:** Edited the Windows System Environment Variables to remove the old path. Reordered the PATH to prioritize the correct Python installation.

\---

### Issue 2: VirtualBox Periodic Crashes

* **Symptom:** The VirtualBox application experienced intermittent crashes on the host machine, making the VMs unstable.
* **Root Cause:** Windows Hypervisor (Hyper-V) and Virtualization-Based Security (VBS) were conflicting with VirtualBox's ability to access the hardware virtualization features.
* **Resolution:**

  * Disabled the Windows Hypervisor (Hyper-V) to prevent conflicts with VirtualBox's Type-2 hypervisor engine.
  * Disabled Virtualization-Based Security (VBS) / Core Isolation in Windows.
  * These changes resolved the crashes and stabilized the VM environment.

\---

### Issue 3: VM Sluggishness \& Low Mouse Refresh Rate

* **Symptom:** The Windows 10/11 Client VM felt extremely sluggish, and the mouse cursor had a very low refresh rate, making it difficult to navigate.
* **Resolution:** Mounted the VirtualBox Guest Additions CD image (`.iso`) to the VM and installed the drivers. This enabled seamless mouse integration, shared clipboard, and significantly improved display performance.

\---

### Issue 4: Internal NIC Reverting to APIPA

* **Symptom:** When attempting to assign a static IP address to the internal network adapter on the Domain Controller, the setting would not save. The adapter would revert to an Automatic Private IP Addressing (APIPA) address (169.254.x.x).
* **Resolution:** Executed a specific sequence to force the network stack to accept the configuration:

  1. Disabled the internal network adapter in Windows.
  2. Applied the static IP, Subnet Mask, and DNS settings.
  3. Re-enabled the network adapter.

\---

### Issue 5: DHCP Server Failure \& Scope Authorization

* **Symptom:** Following the network adapter fix (Issue 4), the DHCP server stopped functioning. The client machine was unable to lease an IP address from the scope, even when logged in as an administrative user.
* **Attempted Solutions:**

  * Logged in as the built-in Domain Administrator and restarted the DHCP Server service.
  * Created a dedicated security group for DHCP Administrators and added the domain admin user to it.
  * Right-clicked the Domain Controller within the DHCP management console and selected **"Authorize."**
* **Resolution:** The DHCP service began working. In an Active Directory environment, DHCP servers must be explicitly authorized in AD DS to prevent rogue servers from handing out bad IP addresses. It is highly likely that the **"Authorize"** action, combined with the active security group permissions, resolved the issue.

