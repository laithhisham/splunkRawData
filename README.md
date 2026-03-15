# splunkRawData

This repository contains Splunk out-of-the-box (OOB) macros used across various data sources and integrations.

## Microsoft Teams Access

Yes — this repository has access to Microsoft Teams (M365 Teams) data through the following macros defined in `macros.csv`:

| Macro | Description |
|---|---|
| `m365_teams_indexes` | Defines the Splunk indexes that contain Microsoft Teams data (default: `index=main OR index=*`). |
| `m365_teams_caller` | Parses raw Microsoft Teams call records — expands sessions, segments, and media streams to extract caller device, caller network, and per-media QoS fields. |
| `m365_teams_qos` | Parses Microsoft Teams QoS (Quality of Service) call data — expands sessions, segments, and media streams to extract jitter, round-trip time, and other stream-level metrics. |

### Usage

To query Microsoft Teams call data in Splunk, reference these macros in your searches:

```spl
index=`m365_teams_indexes` sourcetype=o365:management:activity Workload=MicrosoftTeams
| `m365_teams_caller`
```

```spl
index=`m365_teams_indexes` sourcetype=o365:management:activity Workload=MicrosoftTeams
| `m365_teams_qos`
```