# Identify-and-Remediate-Vulnerabilities

## Objective

Covering vulnerability scanning and remediation, two core phases in the vulnerability management lifecycle. We will use **Nessus Essentials** to scan local VMs hosted on **VMware Workstation**. The lab includes running credentialed scans to discover vulnerabilities, remediating selected ones, then rescanning to verify mitigation effectiveness.

---

### Skills Learned

- Performing credentialed vulnerability scans with Nessus  
- Analyzing and interpreting vulnerability reports  
- Applying security patches and configuration changes  
- Verifying remediation through rescanning processes  
- Integrating vulnerability data into SIEM for monitoring and alerting  

---

### Tools Used

- **Nessus Essentials** for vulnerability scanning  
- **VMware Workstation** for hosting and snapshotting VMs  
- **Windows/Linux VMs** as scan targets  
- **SIEM platform** (e.g., Splunk, Wazuh) for ingesting and tracking vulnerability alerts  
- **Wireshark** for optional network traffic validation  

---

## Steps

1. **Set Up Environment & Volume Snapshot**  
   - In VMware Workstation, install two VMs: one Windows Server and one Ubuntu Server.  
   - Before scanning, take a **snapshot/checkpoint** to preserve the clean baseline state.

2. **Install Nessus Essentials**  
   - Download Nessus Essentials (free) and install it on a separate management VM.  
   - Activate it using your email-based license.

3. **Configure Credentialed Scan**  
   - Create a new scan: select “Advanced Scan” > enter target IPs (e.g., `192.168.10.50` for Windows, `192.168.10.60` for Ubuntu).  
   - Add SSH (Linux) and SMB/WMI (Windows) credentials for full access.  
   - Optional: enable compliance checks (locally mounted configs) if desired.

4. **Run the Scan**  
   - Start the credentialed scan. Expect it to run ~15–30 minutes depending on VM specs.  
   - Monitor progress in the Nessus dashboard.

5. **Analyze Results**  
   - After completion, review findings, focusing on *Critical* and *High* severity issues.  
   - Export the report (HTML or JSON format).  
   - In your SIEM, ingest Nessus alerts or parse results with built-in connectors.

6. **Remediate Vulnerabilities**  
   - For Windows VM: install pending patches via Windows Update or manually download from MS.  
   - For Ubuntu VM: run:
     ```bash
     sudo apt-get update && sudo apt-get upgrade -y
     ```
   - If high-risk misconfigurations were identified, apply the recommended hardening steps.

7. **Rescan to Verify**  
   - Revert to the snapshot taken in step 1 if desired, or simply rerun the scan on the live VMs.  
   - Confirm that critical issues are resolved and no new findings appeared.

8. **Monitor in SIEM**  
   - Check your SIEM for Nessus-based alerts or reports.  
   - Optional: set up dashboards/triggers for repeated vulnerables/rescan findings.

9. **Clean Up Environment**  
   - Optionally restore to pre-lab snapshot or delete VMs.  
   - Archive scan reports and remediation log outputs for future comparison.

---

**Volume Tips:**  
- Adjust VMware storage volume allocation: ensure at least **40 GB** per VM, plus additional snapshot volume.  
- Allocate **8 GB RAM** and **2 CPUs** per scan target VM for reliable scan performance.

---
