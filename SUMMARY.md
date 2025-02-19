# Table of contents

## Welcome wanderer

* [Intro](README.md)
* [The Hacker Manifesto](welcome-wanderer/the-hacker-manifesto.md)
* [Useful Links](welcome-wanderer/useful-links.md)
* [Certificates](welcome-wanderer/certificates.md)

## PENTESTING

* [Methodology](pentesting/methodology.md)
* [Protocols](pentesting/protocols/README.md)
  * [FTP](pentesting/protocols/ftp.md)
  * [SMB](pentesting/protocols/smb.md)
  * [NFS](pentesting/protocols/nfs.md)
  * [SSH](pentesting/protocols/ssh.md)
  * [RDP](pentesting/protocols/rdp.md)
  * [SMTP](pentesting/protocols/smtp.md)
  * [IMAP / POP3](pentesting/protocols/imap-pop3.md)
  * [RSYNC](pentesting/protocols/rsync.md)
  * [SNMP](pentesting/protocols/snmp.md)
  * [IPMI](pentesting/protocols/ipmi.md)
  * [R-Services](pentesting/protocols/r-services.md)
  * [WinRM](pentesting/protocols/winrm.md)
  * [WMI](pentesting/protocols/wmi.md)
  * [LDAP](pentesting/protocols/ldap.md)
* [Databases](pentesting/databases/README.md)
  * [MySQL](pentesting/databases/mysql.md)
  * [MSSQL](pentesting/databases/mssql.md)
  * [Oracle TNS](pentesting/databases/oracle-tns.md)
  * [PostgreSQL](pentesting/databases/postgresql.md)
* [File Transfers](pentesting/file-transfers/README.md)
  * [Windows](pentesting/file-transfers/windows.md)
  * [Linux](pentesting/file-transfers/linux.md)
  * [Code](pentesting/file-transfers/code.md)
  * [Misc](pentesting/file-transfers/misc.md)
* [Password Attacks](pentesting/password-attacks/README.md)
  * [John The Ripper](pentesting/password-attacks/john-the-ripper.md)
  * [Hashcat](pentesting/password-attacks/hashcat.md)
* [Docker](pentesting/docker.md)
* [Pass-The-Hash(FOR LIN\&WIN)](pentesting/pass-the-hash-for-lin-and-win.md)
* [Detection And Evasion (FOR RT LATER)](pentesting/detection-and-evasion-for-rt-later.md)

## TOOLS

* [Nmap](tools/nmap.md)
* [Responder](tools/responder.md)
* [Metasploit](tools/metasploit.md)
* [Other](tools/other.md)
* [Hydra](tools/hydra.md)
* [Sliver](tools/sliver.md)
* [BloodHound](tools/bloodhound.md)
* [Mimikatz](tools/mimikatz.md)
* [NetExec](tools/netexec.md)

## WEB

* [Web Recon](web/web-recon/README.md)
  * [Fuzzing](web/web-recon/fuzzing.md)
* [Attacks](web/attacks.md)
* [DNS](web/dns.md)

## Linux

* [Theory](linux/theory.md)
* [Commands and Utilities](linux/commands-and-utilities.md)
* [Bash Scripting](linux/bash-scripting.md)
* [Post-Exploitation](linux/post-exploitation/README.md)
  * [Tools](linux/post-exploitation/tools.md)
  * [Cred Hunting](linux/post-exploitation/cred-hunting.md)
  * [Pivoting](linux/post-exploitation/pivoting.md)
* [Privilege Escalation](linux/privilege-escalation.md)
* [Useful Commands](linux/useful-commands.md)

## WINDOWS

* [Theory](windows/theory/README.md)
  * [Security](windows/theory/security.md)
* [Commands and Utilities](windows/commands-and-utilities.md)
* [PowerShell](windows/powershell.md)
* [Post-Exploitation](windows/post-exploitation/README.md)
  * [Tools](windows/post-exploitation/tools.md)
  * [Enumeration](windows/post-exploitation/enumeration.md)
  * [Pivoting](windows/post-exploitation/pivoting.md)
  * [Cred Hunting](windows/post-exploitation/cred-hunting.md)
* [Privilege Escalation](windows/privilege-escalation/README.md)
  * [Privileges](windows/privilege-escalation/privileges.md)
  * [Built-In Groups](windows/privilege-escalation/built-in-groups/README.md)
    * [Backup Operators](windows/privilege-escalation/built-in-groups/backup-operators.md)
    * [Server Operators](windows/privilege-escalation/built-in-groups/server-operators.md)
    * [Print Operators](windows/privilege-escalation/built-in-groups/print-operators.md)
    * [DnsAdmins](windows/privilege-escalation/built-in-groups/dnsadmins.md)
    * [Event Log Readers](windows/privilege-escalation/built-in-groups/event-log-readers.md)
  * [Privilege Abuse](windows/privilege-escalation/privilege-abuse/README.md)
    * [Potatoes](windows/privilege-escalation/privilege-abuse/potatoes.md)
    * [SeDebugPrivilege](windows/privilege-escalation/privilege-abuse/sedebugprivilege.md)
    * [SeTakeOwnershipPrivilege](windows/privilege-escalation/privilege-abuse/setakeownershipprivilege.md)
  * [MISC](windows/privilege-escalation/misc/README.md)
    * [DLL Hijacking](windows/privilege-escalation/misc/dll-hijacking.md)
    * [UAC Bypass](windows/privilege-escalation/misc/uac-bypass.md)
    * [User-Interaction Attacks](windows/privilege-escalation/misc/user-interaction-attacks.md)
    * [Weak Permissions](windows/privilege-escalation/misc/weak-permissions.md)

## ACTIVE DIRECTORY

* [Theory](active-directory/theory.md)
* [Recon](active-directory/recon.md)
* [Movement](active-directory/movement/README.md)
  * [ADCS](active-directory/movement/adcs.md)
  * [Credentials](active-directory/movement/credentials/README.md)
    * [Ticket/Hash Attacks](active-directory/movement/credentials/ticket-hash-attacks.md)
  * [Powershell Remoting](active-directory/movement/powershell-remoting.md)
* [Persistence](active-directory/persistence.md)
* [Linux](active-directory/linux/README.md)
  * [Linux Post-Exploitation](active-directory/linux/linux-post-exploitation.md)

## Networking

* [Theory](networking/theory/README.md)
  * [Types / Topologies](networking/theory/types-topologies.md)
  * [OSI & TCP/IP Models](networking/theory/osi-and-tcp-ip-models.md)
  * [TCP / UDP](networking/theory/tcp-udp.md)
  * [MAC Addresses](networking/theory/mac-addresses.md)
  * [IP / Subnetting](networking/theory/ip-subnetting.md)
  * [Proxies](networking/theory/proxies.md)
  * [ARP](networking/theory/arp.md)
* [Pivoting](networking/pivoting/README.md)
  * [Port-Forwarding](networking/pivoting/port-forwarding.md)
* [Commands and Utilities](networking/commands-and-utilities.md)
* [Techniques](networking/techniques.md)

## CLOUD

* [Google GKE/GCP](cloud/google-gke-gcp/README.md)
  * [Theory](cloud/google-gke-gcp/theory.md)

## programming

* [Page 1](programming/page-1.md)
