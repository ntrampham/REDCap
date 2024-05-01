# CVE-2023-38825: SQL Injection in REDCap Versions <13.8.0

## Issue Summary
An SQL Injection vulnerability was found on `/<redcap_version>/MyCapMobileApp/update.php` API. Because of lacking of verifying untrusted data `$_POST['index_modal_update']` results in malicious payload being passed to the SQL query via the `$page_id` variable.

![](./attachments/2023-05-23%2016_21_42-Clipboard.png)

After sending the malicious payload, the response time exceeds 5 seconds.

## Issue Impact
An attacker can employ a SQL Injection attack to dump all data from the database.

Besides that, the REDCap password reset mechanism requires a `password_reset_key` provided in the URL delivered to the user. An attacker can quickly obtain this key using the SQL Injection bug already found and change the passwords of any REDCap users by forging their password reset requests. Then he can access whatever account he wants, especially the admin account.

![](./attachments/2023-07-11%2017_40_19-Clipboard.png)

Change the admin password successfully

## Disclosure Timeline for CVE-2023-38825
- 05/20/23: Vulnerability discovered
- 07/01/23: Vulnerability reported to REDCap
- 07/07/23: Patch provided by REDCap
- 07/11/23: Writeup published and CVE Requested
- 08/03/23: CVE-2023-38825 assigned

## References
[REDCap Changelog](./attachments/REDCap-changelog.md)

> Major security fix: An SQL Injection vulnerability was found on a MyCap-related page, in which a malicious user could potentially exploit it and execute arbitrary SQL commands on the database by manipulating an HTTP request in a specially-crafted way. In order to exploit this, the user must be logged in as a REDCap user and must also have one or more instruments enabled as MyCap tasks.
