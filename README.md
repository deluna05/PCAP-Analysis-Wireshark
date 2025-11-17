# PCAP-Analysis-Wireshark

Author: Aiganym Tulebayeva

## Summary

This repository contains a PCAP file and detailed analysis demonstrating network forensics techniques commonly used by SOC analysts. The analysis covers identification of SYN scans, TCP handshake verification, suspicious DNS query detection, and flow extraction using `tshark`.

## Repository Structure

```
PCAP-Analysis-Wireshark/
├── README.md
├── analysis/
│   ├── sample.pcap
│   └── analysis.md
└── artifacts/
    ├── tshark_summary.txt
    └── notable_packets.png
```

## Files

- `analysis/sample.pcap` — Sample network capture file for analysis
- `analysis/analysis.md` — Step-by-step analysis and findings
- `artifacts/tshark_summary.txt` — Exported tshark summaries
- `artifacts/notable_packets.png` — Screenshot of important Wireshark view

## How to Reproduce Locally

1. Open `analysis/sample.pcap` in Wireshark
2. Follow the step-by-step analysis in `analysis/analysis.md`
3. Run the included `tshark` commands to extract summaries and verify findings
