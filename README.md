# PCAP-Analysis-Wireshark

Author: Aiganym Tulebayeva  

## Summary
This repo contains a small PCAP file and a detailed analysis demonstrating basic network forensics tasks commonly used by SOC analysts: identifying SYN scans, analyzing TCP handshakes, finding suspicious DNS lookups and extracting relevant flows with `tshark`.

## Files
- `analysis/sample.pcap` — sample capture (add your pcap here).
- `analysis/analysis.md` — step-by-step analysis and findings.
- `artifacts/tshark_summary.txt` — exported summaries (example).
- `artifacts/notable_packets.png` — screenshot of important Wireshark view.

## How to reproduce locally
1. Open the `sample.pcap` in Wireshark and follow the analysis in `analysis/analysis.md`.
2. Use the included `tshark` commands to extract summaries.


