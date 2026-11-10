# Methodology

## Project context

- **Author:** Dangeti Bhanu Sai Teja
- **Institution:** TU Dublin
- **Programme:** MSc Applied Cybersecurity
- **Project period:** September–October 2026
- **Project:** T-Pot: Analysis of Attacks from Two Cloud Honeypots

## 1. Deployment

Two T-Pot honeynet instances were deployed in separate cloud environments:

- Server 1: Microsoft Azure, Spain Central, Ubuntu Server 24.04 LTS.
- Server 2: Oracle Cloud, Frankfurt, Ubuntu (upgraded during the project).

The deployments had different observation windows and infrastructure configurations. They were analysed as separate observations rather than as a controlled regional experiment.

## 2. Data collection

The T-Pot dashboard was used to review the overall activity landscape. Kibana Discover was used to query Elasticsearch records and narrow the analysis to individual honeypot types and relevant fields.

## 3. Service-level investigation

- **Cowrie:** reviewed SSH/Telnet sessions, simulated logins, commands, file-download events and SHA-256 values.
- **RDPHoneypot:** reviewed connection and authentication activity, including repeated login attempts.
- **Dionaea:** reviewed interactions with emulated network services, with particular attention to destination port 445 (SMB).
- **Heralding:** reviewed credential-submission activity, including PostgreSQL attempts on port 5432.

## 4. Selected observations

The analysis reported the following Server 2 counts:

| Honeypot / view | Documents or events |
|---|---:|
| Overall T-Pot dashboard | Approximately 2 million |
| Cowrie | 232,184 |
| Cowrie successful file downloads | 111 |
| Cowrie unsuccessful file downloads | 97 |
| Cowrie unique SHA-256 hashes | 17 |
| RDPHoneypot | 893,543 |
| Dionaea, destination port 445 | 135,812 |
| Heralding | 228,204 |
| Heralding, PostgreSQL filter | 696 |

These are Elasticsearch document/event counts, not unique attacker counts. A single source can generate many documents, and a session can contain multiple records.

## 5. Analysis and interpretation

Searches used honeypot type and relevant event fields to identify patterns. GeoIP values were interpreted as approximate source-IP geolocation and not proof of an operator's physical location. The findings indicated probing, authentication attempts and payload retrieval behaviour; they did not establish compromise of a production system.

## 6. Limitations

- The two deployments did not have identical observation windows or configurations.
- A high document count does not necessarily mean a high number of unique attackers.
- Honeypot events represent interactions with decoy services and do not by themselves prove compromise of a production system.
- GeoIP can reflect cloud infrastructure, VPNs, proxies or compromised devices.
- The architecture diagram is conceptual and does not imply a shared logging cluster between the two cloud servers.

## 7. Safe portfolio publication

Before publishing this repository, review all files for student identifiers, source/server IP addresses, credentials, API keys, tokens, private keys and other sensitive details. Confirm that sharing report material is permitted by TU Dublin. The included screenshots have had detailed event areas obscured. Do not upload raw logs or malware samples.
