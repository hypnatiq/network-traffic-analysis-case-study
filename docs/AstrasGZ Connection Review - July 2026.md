# AstrasGZ Connection Review

Date: July 2026

## Starting point

I had Bitdefender running for endpoint protection, but I wanted to understand the network behavior I could observe while the AstrasGZ client was open.

The review was passive and limited to traffic captured from my own Windows PC. I did not test the remote server for vulnerabilities.

## Capture sequence

I recorded three windows on July 22, 2026:

- Initial capture - 5.282 seconds and 1,276 packets for a short baseline.
- Client-open capture - 22.489 seconds and 3,255 packets to review traffic during launch.
- Extended session - 891.931 seconds and 120,656 packets to observe sustained connection behavior.

The file originally named packet capture 10 mins.pcapng actually covers 14 minutes and 51.9 seconds. This report uses the measured duration instead of the filename.

## Data preparation

The extended capture was converted into a 16-field CSV with TShark and a Node.js conversion script.

The CSV was imported into a local Flask and SQLite log aggregator:

- imported rows: 120,656
- skipped rows: 0
- dataset storage: SQLite
- filtering: text search, field filters, sorting, pagination, details, and filtered export

## What I observed

### Launch capture

The 22.489-second launch capture contained:

- three initial outbound TCP SYN packets
- two remote destinations
- one TCP destination port, HTTPS port 443
- successful SYN and ACK responses
- no TCP resets
- no public inbound initial SYN packets to the local workstation

That pattern did not establish TCP port scanning or unsolicited inbound probing.

### High-volume UDP traffic

The largest traffic group used a small number of consistent UDP flows. The flows could be isolated by destination and port, but the capture did not identify the local process that owned those sockets.

This is why the original review classified the traffic as requiring attribution instead of blocking it based on packet count.

### Background activity

The captures also included unrelated system and application traffic such as:

- DNS
- TLS and QUIC
- multicast DNS
- LLMNR
- NetBIOS name service
- SSDP
- ARP

Those protocols are important because a full-interface capture can include activity from Windows and other applications. Not every packet recorded during the test belonged to AstrasGZ.

## Conclusion

The reviewed capture did not establish port scanning or malicious connection behavior.

It also did not prove the client or remote service was safe. The honest conclusion was narrower: the visible traffic could be organized, filtered, and investigated, but the dominant UDP flows still needed process-level attribution.

## What I would improve in a repeat test

1. Record the client process ID before launch.
2. Correlate local UDP ports with Get-NetUDPEndpoint, Resource Monitor, or equivalent process-aware evidence.
3. Capture DNS and TLS handshakes from the beginning of the session.
4. Record an idle baseline with the same background applications running.
5. Compare repeated sessions instead of relying on one extended capture.
6. Check suspicious destinations against current threat-intelligence sources only after process attribution.

## Privacy

The public case study excludes raw packet captures, private addresses, remote endpoint lists, account identifiers, registry data, and local installation paths.
