# Screenshot Record

## Wireshark views

1. `wireshark-protocol-hierarchy.png`
   - Shows packet and byte distribution by protocol.
   - Does not expose endpoint addresses, usernames, credentials, or local paths.
2. `wireshark-traffic-over-time.png`
   - Shows packet volume across the full capture using one-second intervals.
   - Includes Wireshark's TCP analysis line as a review aid, not a malicious-activity conclusion.

## Sanitized investigation set

The `hypno-investigation` folder contains nine images showing:

1. the original Flask and SQLite aggregator with a sanitized UDP 19299 filter
2. HypNO capture summary and limitations
3. the selected sanitized IP flow
4. individual packet evidence
5. supported synthetic process and PID correlation
6. destination and provider context
7. explanation, missing evidence, next checks, and assessment
8. the paired original-aggregator and HypNO comparison
9. the HypNO `0.83.9-dev` About view

The original and HypNO views use different sanitized datasets. The comparison demonstrates the same task, not a claim that HypNO performed the original July 2026 analysis.

## Image rules

- Use real rendered interfaces.
- Use sanitized or synthetic data.
- Exclude private addresses, endpoint lists, usernames, client keys, local paths, registry values, credentials, and unrelated applications.
- Do not use the original registry-remnant screenshot.
- Do not present a synthetic process as a real application observation.
- Do not use a provider result as a safety guarantee.
