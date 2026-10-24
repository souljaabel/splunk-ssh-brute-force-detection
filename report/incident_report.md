Incident Investigation Report: SSH Authentication Failures
1. Executive Summary
I investigated repeated SSH authentication failures in Splunk’s supplied tutorial dataset. The investigation focused on source IP 87.194.216.51 and activity targeting the root account and other usernames.

The observed pattern is consistent with possible automated password guessing or account discovery. The available searches did not establish a successful compromise.

2. Environment
SIEM: Splunk Search & Reporting
Dataset: Splunk tutorial data
Log source: tutorialdata.zip:./www1/secure.log
Log type: SSH authentication events
3. Findings
Finding

Result

Source IP investigated

87.194.216.51

Failed authentication events

948

Observation period

October 15–22, 2026

Highest daily count

223 on October 19, 2026

Usernames observed

root, administrator, daemon, guest

Matching successful password events

None returned by the search

4. Investigation Method
Searched the secure-2 sourcetype for SSH authentication failures.
Extracted source IP addresses and usernames from raw log messages using SPL.
Aggregated failures by source IP.
Examined the daily distribution of failures.
Searched for successful SSH password authentication events from the same source.
5. Assessment
Repeated failures from one source, combined with attempts involving multiple usernames, are consistent with potential SSH password guessing or account discovery.

This is a preliminary assessment. The source IP’s ownership and intent have not been established. No matching successful password authentication events were returned, but this does not rule out other successful authentication methods or missing events.

6. Recommended Next Steps
Review surrounding authentication events and investigate any successful logins.
Validate the source IP and event details against the available environment.
Consider appropriate SSH hardening and rate limiting.
Escalate according to the organization’s incident response procedures if corroborating evidence is found.
7. Limitations
This investigation uses a supplied tutorial dataset rather than live production logs. The results represent the events returned by the searches performed and should not be interpreted as proof of a real-world attack or compromise.

8. Skills Demonstrated
SIEM log investigation
SPL field extraction and aggregation
SSH authentication analysis
Time-based event analysis
Preliminary incident assessment
Security report writing
