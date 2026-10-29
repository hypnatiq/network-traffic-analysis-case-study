# Network Connection Review Method

## 1. Define the question

Start with one practical question, such as:

What connections appear while this application launches and runs?

Do not begin with the assumption that high packet volume or an unfamiliar address is malicious.

## 2. Preserve the starting state

- Keep endpoint protection and firewall controls enabled.
- Record the date, interface, operating system, and application state.
- Save a netstat or process-aware connection snapshot.
- Record which background applications remain open.

## 3. Capture controlled windows

Use separate captures for:

1. idle baseline
2. application launch
3. active use
4. application close, when useful

Change as little as possible between captures.

## 4. Structure the evidence

Convert packet data into fields that can be searched and compared:

- time
- direction
- protocol
- source and destination
- ports
- DNS query
- HTTP host
- TLS server name
- packet length

Retain the original capture privately and use a sanitized derivative for public examples.

## 5. Filter in layers

Review the data in this order:

1. local discovery and broadcast traffic
2. DNS and service-name evidence
3. established web connections
4. repeated or high-volume flows
5. initial SYN packets and connection failures
6. inbound connection attempts
7. process ownership

Filtering in layers reduces the chance of treating ordinary background traffic as an application finding.

## 6. Attribute before acting

An address, port, or packet count is not enough by itself.

Before blocking or escalating a connection:

- identify the owning process
- confirm the timing matches the application action
- check whether the service name or certificate explains the destination
- compare repeated captures
- use current threat intelligence when it adds evidence

## 7. State the limit

Every report should answer:

- What was observed?
- What explanation is supported?
- What remains unverified?
- What would confirm or weaken the conclusion?

Avoid claims that a short capture proves an application or service is safe.

## 8. Preserve reproducibility

Keep:

- capture hashes
- exact durations and packet counts
- filters used
- conversion fields
- dataset import totals
- findings and rejected interpretations
- the next test needed

This makes the analysis explainable in an interview and repeatable later.
