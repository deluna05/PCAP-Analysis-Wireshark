# PCAP Analysis — step-by-step

_Date: YYYY-MM-DD_  
_Analyst: Aiganym Tulebayeva_

## Goals
- Identify port scans (SYN scans)
- Verify whether observed connections completed TCP handshakes
- Detect suspicious DNS queries
- Extract suspicious flows for further analysis

## Tools used
- Wireshark (GUI)
- tshark (CLI)

---

## 1) Quick overview with tshark
Run:

tshark -r sample.pcap -q -z conv,tcp



This gives TCP conversations and bytes per direction. Look for many SYNs from one source to many destination ports.



Also:





tshark -r sample.pcap -T fields -e frame.number -e ip.src -e ip.dst -e tcp.flags.syn -e tcp.flags.ack -E separator=, > packets.csv



Open `packets.csv` to look for many `tcp.flags.syn==1` with `tcp.flags.ack==0`.



---



## 2) Detect SYN scan (Wireshark)

Filter in Wireshark:





tcp.flags.syn == 1 && tcp.flags.ack == 0



- If one IP sends many SYNs to many ports and receives few SYN/ACK — likely a SYN scan.

- Note the source IP and target ports. Example finding:

  - Source: 192.0.2.10

  - Targets: 10.0.0.5:22, 10.0.0.5:80, 10.0.0.5:443, ...



---



## 3) Verify completed handshakes

Filter:





tcp.flags.syn==1 && tcp.flags.ack==1



This shows SYN/ACK packets (responses). Then search for ACKs from client:





tcp.flags.ack==1 && tcp.len==0



Completed 3-way handshake will show SYN, SYN/ACK, ACK. If many SYNs but few complete, it's a scan.



---



## 4) DNS examination

Filter DNS:





dns



Look for unusual domains, high frequency queries, or long domain names (possible exfil). Note: check `dns.qry.name` fields in tshark:





tshark -r sample.pcap -Y dns -T fields -e frame.number -e ip.src -e dns.qry.name | sort | uniq -c | sort -nr





---



## 5) Suspicious traffic

- Look for unusual ports or high-volume traffic to unknown external IPs.

- If encrypted protocols (TLS) used on non-standard ports — investigate.



---



## 6) Extract suspicious flows

Example:





tshark -r sample.pcap -Y "ip.src==192.0.2.10 && tcp" -w artifacts/suspicious_flow.pcap



Open `suspicious_flow.pcap` in Wireshark for step-by-step packet review.



---



## Final note (example conclusion)

- Observed a SYN scan from 192.0.2.10 toward 10.0.0.5 across ports 22,80,443 — few handshakes completed → likely reconnaissance.

- Observed repeated DNS queries for `weird-subdomain.example.com` — further investigation recommended (resolve domain, check WHOIS, check passive DNS).



(вставь как есть в analysis/analysis.md)
