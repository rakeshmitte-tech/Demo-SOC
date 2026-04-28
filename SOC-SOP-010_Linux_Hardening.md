📄 SOC-SOP-010: Linux Server Hardening (Ubuntu 24.04)
Document Information
Document ID: SOC-SOP-010
Owner: Harshit Sengar (CISO)
Document Type: Standard Operating Procedure
Version: V2.0
Role	Name	Function	Date
Created	Rahul Rao M	Junior Cybersecurity Engineer	15-Apr-2026
Updated	Rakesh Mitte	Associate Software Engineer	(Current Date)
Approved	Harshit Sengar	CISO	(Pending)

1. Objective

Define the mandatory security configurations required to harden Ubuntu 24.04 LTS servers in alignment with CIS Benchmark Level 1 and ISO/IEC 27001 requirements.

2. Scope

This SOP applies to all Ubuntu 24.04 Linux instances deployed within the Simplify3X environment, including:

Amazon Web Services (AWS)
DigitalOcean
On-Premise infrastructure

3. Phase 1 – Baseline Hardening (CIS Level 1)

3.1 SSH Lockdown (CIS 5.2)

Disable Root Login:
PermitRootLogin no

Disable Password Authentication:
PasswordAuthentication no

Set Max Auth Tries:
MaxAuthTries 4

Restart SSH Service:
systemctl restart sshd

3.2 Password Aging and Account Policies (CIS 5.5)

PASS_MAX_DAYS 90
PASS_MIN_DAYS 7
PASS_WARN_AGE 14
useradd -D -f 30

3.3 Auditd Configuration & Log Forwarding (CIS 4.1)

apt-get install auditd audispd-plugins
Configure /etc/audit/rules.d/audit.rules

Monitor:
/etc/sudoers
/etc/shadow
Failed logins

Ensure Wazuh integration:
Log source: /var/log/audit/audit.log

4. Phase 2 – Advanced Hardening (CIS Level 2)

Disable unused kernel modules (e.g., USB storage)

Apply filesystem restrictions:
/tmp, /var/tmp → nodev, nosuid, noexec

Enable AppArmor enforcement

Disable unnecessary services:
FTP, Telnet, NFS, LDAP (if unused)

5. Phase 3 – Assessment & Gap Analysis (ISO: PLAN)

Compare system configuration with CIS benchmark

Identify:
Missing controls
Misconfigurations

Maintain:
Gap analysis report
Compliance checklist

6. Phase 4 – Implementation (ISO: DO)

Apply configurations using:
Shell scripts
Ansible automation

Follow:
Test → Validate → Deploy

Maintain:
Change logs
Implementation records

7. Phase 5 – Validation & Testing (ISO: CHECK)

SSH Validation:
sshd -T | grep permitrootlogin

Password Policy:
chage -l <username>

Audit Rules:
auditctl -l

Perform:
Functional testing
Security validation

8. Phase 6 – Monitoring & Logging (ISO: CHECK)

Ensure logs forwarded to SIEM:
Wazuh

Monitor:
Failed logins
Privilege escalation
File changes

Configure alerts for suspicious activity

9. Phase 7 – Continuous Compliance (ISO: ACT)

Perform periodic audits:
Monthly / Quarterly

Detect configuration drift

Re-apply CIS baseline if deviations found

10. Phase 8 – Exception Management

All exceptions must:
Be documented
Be risk-assessed
Be approved

Store in:
SOC-REG-001

11. Phase 9 – Audit & Reporting

Maintain:
Configuration evidence
Audit logs
Compliance reports

Support:
ISO 27001 audits
Internal reviews
