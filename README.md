Splunk SSH Brute-Force Detection Project
Project Overview
This project demonstrates a basic SOC analyst investigation using Splunk Search Processing Language (SPL). I analyzed sample SSH authentication logs to identify repeated failed login attempts, investigate targeted usernames, and check for evidence of successful password authentication from a suspicious source.

Tools Used
Splunk Search & Reporting
Splunk Search Processing Language (SPL)
SSH authentication logs
GitHub for project documentation
Investigation Findings
Log source: tutorialdata.zip:./www1/secure.log
Source IP investigated: 87.194.216.51
Failed authentication events: 948
Observed dates: October 15–22, 2026
Peak daily count: 223 failures on October 19, 2026
Observed usernames: Included root, administrator, daemon, and guest
Successful authentication check: No matching Accepted password events were returned for this IP in the searched data.

Detection Query
The following SPL query extracts usernames and source IP addresses, then summarizes the failed authentication events associated with the investigated IP.
index=* sourcetype=secure-2 "Failed password"
| rex field=_raw "Failed password for (?:invalid user )?(?<username>\S+) from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| search src_ip="87.194.216.51"
| stats count AS failed_attempts dc(username) AS unique_usernames values(username) AS usernames by src_ip
View the complete SPL query

Analysis
The repeated failed SSH authentication attempts and use of multiple usernames are consistent with possible automated password guessing or account discovery.

The available search results did not establish that an account was compromised. The absence of matching successful password events does not rule out other authentication methods or events missing from the dataset.

Recommended Response
Review related authentication events and timestamps.
Investigate any successful logins associated with the source.
Validate the source and activity before recommending a block.
Consider appropriate SSH protections, such as disabling remote root login where operationally appropriate, enforcing key-based authentication, and applying rate limits.
Investigation Evidence
1. Failed SSH Login Summary
2. Daily Failed Login Activity
3. Raw SSH Log Evidence
Incident Report
Read the full investigation report

Environment and Limitations
This is a learning project using Splunk’s supplied tutorial dataset, not a live security incident. Findings are limited to the events and searches examined.

Skills Demonstrated
Log analysis
SPL searching and filtering
Authentication failure investigation
Event aggregation and time-based analysis
Preliminary incident assessment
Security documentation
Disclaimer
This project uses Splunk tutorial/sample data for educational purposes. It does not represent a confirmed real-world security incident.




