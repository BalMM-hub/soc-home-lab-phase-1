# Troubleshooting: Sysmon Forwarding Issue

[← Back to project overview](README.md)

This stage surfaced a real issue, and it is documented here in full rather than smoothed over, since diagnosing problems like this is a core part of SOC and log-pipeline work. General Windows Security and System logs were confirmed to be forwarding correctly and were fully searchable in Splunk. Sysmon-specific events, however, were not appearing in any Splunk search, despite Event Viewer clearly showing them being generated locally on the VM.

## Confirming the Gap

To confirm this rather than assume it, the `EventCode` field for the Windows VM host was inspected directly in Splunk. The top values returned were all standard Windows Security event codes (4907, 5379, 4624, 4672, 4799, and others) — with no Sysmon-related event codes present anywhere in the results. This confirmed the gap was specific to Sysmon data, not a general forwarding failure.

![EventCode breakdown](images/figure24_eventcode_breakdown.png)
*EventCode field breakdown showing only standard Windows Security event codes, confirming Sysmon events were not yet present in Splunk*

## Root Cause Investigation

Reviewing the `inputs.conf` file line by line against the working stanzas turned up a typo in an unrelated stanza (`WinEventLogs://System` instead of `WinEventLog://System`), which was corrected. The Sysmon stanza itself was re-checked and appeared syntactically correct. The Universal Forwarder was restarted after the fix and reconfirmed as actively connected to Splunk Enterprise using the forward-server status check.

![inputs.conf fixed](images/figure25_inputs_fixed.png)
*Corrected inputs.conf file with the typo fixed*

![Forwarder restarted after fix](images/figure26_forwarder_restart_fixed.png)
*Universal Forwarder restarted successfully following the configuration fix*

## Current Status

As of this writing, Sysmon events are still not appearing in Splunk search results even after this fix, and the issue is being actively investigated. Working hypotheses include the forwarder's internal checkpoint/service state not fully resetting on restart, an indexing or index-routing configuration issue on the Splunk Enterprise side, or a remaining problem with the Sysmon input stanza itself that has not yet been identified.

**This page will be updated with the resolution once the root cause is confirmed.**

---

[← Back to project overview](README.md)
