# AstrasGZ Network Traffic Analysis Case Study

## What I wanted to understand

In July 2026, I wanted to see what network activity occurred while I used the AstrasGZ game client on my own Windows PC.

Bitdefender remained active for endpoint protection. This review answered a different question: what connections and traffic patterns appeared while the client was running?

I used passive packet capture. I did not scan, probe, exploit, or modify the remote service.

## What I built

I captured three network windows, converted the longest PCAPNG capture into a structured CSV, and imported all 120,656 packet records into a local Flask and SQLite log aggregator.

The converted dataset contained 16 fields, including timestamp, packet number, packet length, protocol, IPv4 and IPv6 addresses, TCP and UDP ports, DNS names, HTTP host information, and TLS server names.

I filtered the dataset to separate high-volume UDP activity, web traffic, name resolution, and normal local discovery traffic.

## What the review supported

- The reviewed launch capture did not establish TCP port scanning or unsolicited inbound connection attempts.
- A small number of outbound HTTPS connection attempts completed normally.
- High-volume UDP flows were visible and could be isolated consistently by address and port.
- Packet volume alone was not enough to label the UDP flows malicious.
- The packet capture could not identify the owning Windows process by itself.

## What the review did not prove

This case study does not certify AstrasGZ, its client, or its infrastructure as safe.

It documents only the traffic visible during the recorded capture windows. Process attribution, payload interpretation, current threat-intelligence review, and repeated testing would be needed for stronger conclusions.

## How the workflow evolved in HypNO

The original aggregator made imported rows searchable and viewable. HypNO `0.83.9-dev` now demonstrates the same investigation task with a guided path through capture summary, filters, packet evidence, destination context, available process evidence, provider context, a plain-language explanation, missing evidence, ordered next checks, and a saved assessment.

The public screenshots use deterministic sanitized or synthetic data. The original aggregator and HypNO screenshots do not use the same dataset, and HypNO is not presented as the tool that performed the July 2026 analysis.

The selected synthetic HypNO example uses the approved label `Not flagged by responding sources`. That label records provider responses. It is not a safety guarantee.

![Original aggregator and HypNO paired comparison](images/hypno-investigation/08%20-%20Original%20Aggregator%20and%20HypNO%20Paired%20Comparison%20-%20Sanitized%20-%202026-10-28.png)

## Why this matters

The useful result was not a simple safe or unsafe label. The useful result was a repeatable method:

1. Record a baseline.
2. Capture the launch window.
3. Capture a longer session.
4. Convert packet data into structured records.
5. Filter traffic by protocol, destination, port, and time.
6. Separate expected background activity from traffic that still needs attribution.
7. State what the evidence supports and where it stops.
8. Record the next evidence needed before considering action.

This workflow became part of the early foundation that later informed HypNO, my Windows network-observation application.

## Tools

- Wireshark and TShark
- Windows netstat
- Node.js conversion script
- Python and Flask
- SQLite
- CSV filtering and export
- HypNO `0.83.9-dev` for the later sanitized workflow demonstration

## Screenshots

The two Wireshark images show protocol distribution and traffic over time without exposing endpoint addresses. The nine-image sanitized set under `images/hypno-investigation` shows the original aggregator, the current HypNO investigation path, the paired comparison, and the rendered development version.

## Repository contents

- `docs/AstrasGZ Connection Review - July 2026.md`
- `docs/Methodology.md`
- `docs/Future HypNO Reference Plan.md`
- `data/capture-summary.csv`
- `data/analysis-summary.csv`
- `data/public-safe-investigation-summary.csv`
- `images/wireshark-protocol-hierarchy.png`
- `images/wireshark-traffic-over-time.png`
- `images/hypno-investigation/`

The raw packet captures, endpoint lists, local network details, unredacted netstat output, and account-related screenshots are intentionally excluded.

## Project date

Original investigation: July 2026

Sanitized HypNO workflow comparison: October 2026

AstrasGZ reference: https://astrasgz.com/
