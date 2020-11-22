# Mitre ATT&CK® Mappings for Amazon GuardDuty

GuardDuty operates on three data sources: CloudTrail, VPC flow logs (netflow), and Route 53 DNS logs. Thus it doesn't have a lot of visibility, which makes sense when we consider the Shared Responsibility model. Additionally, many GuardDuty Findings are anomaly detections rather than categorical detections. Modeling some of these GuardDuty Findings into Mitre ATT&CK can be a bit of a square peg in a round hole so it's not a perfect science by any means. I clearly diverged with AWS on some of their own mappings as you'll see Persistence Findings mapped to Discovery and so forth.

As of November 22, 2020, there are 71 unique GuardDuty Findings.

There's a dotted inclusion of Command and Control since this Tactic is not yet included in Enterprise Cloud.

## Mapping Insights
- The Pentest:S3 Findings were thrown under Discovery, particularly since these are not a result of using valid AWS access keys. These are likely going to be unauthenticated S3 API calls.
- Policy:S3 were categorized into Defensive Evasion though these Findings are more indicative of risky configuration changes in S3 rather than an attacker modification. These, realistically, do not map to ATT&CK.
- Backdoor:EC2/Spambot are categorized as Resource Hijacking versus Phishing (T1566) since the abuse of SMTP appears to be the intent of the detection.
- Impact:S3/PermissionsModification.Unusual are categorized as collection as this seems to look for object permission modification.
- UnauthorizedAccess:S3 were placed into Collection as this is S3 API access.
- PenTest:IAMUser and Policy:IAMUser/RootCredentialUsage Findings could represent many life cycles of the attack but were modeled as Initial Access for similicity. The first alert for this rule would likely indicate the initial access from those valid AWS access keys.
- Recon:IAMUser Findings have all been modeling into Discovery since these is authenticated API access.
- Stealth:IAMUser/PasswordPolicyChange should probably be a Policy Finding and doesn't map well.
- UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration detects instance credentials in use, but modeling into Credential Access given the uniqueness of the technique and this detection. Realistically, monitoring for an SSRF vulnerability to subsequently access the IMDS would probably fall within the Enterprise Linux Matrix.
