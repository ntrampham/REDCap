## Version 13.8.1 (released on 2023-07-07)
### CHANGES IN THIS VERSION:

- Bug fix: On certain occasions, the Control Center and/or Configuration Check page might mistakenly display the warning that "Some non-versioned files are outdated", which might be incorrect and a false positive.
- Bug fix: A fatal PHP error might occur when using Duo for two-factor authentication.
- Bug fix: A fatal PHP error might occur when attempting to send emails via the Email Users page, thus preventing the emails from being sent.
- Bug fix: A fatal PHP error might occur related to CDIS when performing the EHR launch of the REDCap window inside the EHR user interface.

## Version 13.8.0 (released on 2023-07-07)
### CHANGES IN THIS VERSION:

- **New feature: Background Data Import**
    - In the Data Import Tool, users may now alternatively import data using an asynchronous background process (as opposed to the existing real-time process). The background process is better for large data files. The background process will email the user after the data file has been fully imported, and the email will note any errors that may have occurred during the import process.
    - During the background data import process, which is performed by several simultaneous cron jobs, each record will be imported one at a time. If there is any error with a record being imported, none of that individual record’s data will be imported, after which the user will be able to view all the errors with the option to re-download the records/data that failed to import, thus allowing the user to fix the data and attempt to import it again.
    - Note: The background data import works with the “Reason for Change” project-level feature, which requires a reason for any changes made to an existing record.
    - The feature is currently only available in the user interface (not in the API), but it may be available for the API in the future.
    - If the background data import has begun, the user who initiated the import (or an administrator) can cancel the import process at any time. However, any data that was imported by the import process prior to it being canceled will not be undone after it is canceled. All changes made by the process up until cancellation are permanent.
- **Critical security fix**: A Blind SQL Injection vulnerability was found on data entry forms and survey pages, in which a malicious user could potentially exploit it and execute arbitrary SQL commands on the database by manipulating an HTTP request in a specially-crafted way. This bug affects all known REDCap versions.
- **Critical security fix**: A PHP Deserialization Remote Code Execution vulnerability was found in which a malicious user who is logged in could potentially exploit it by manipulating an HTTP request to a specific CDIS-related page while manipulating a certain CDIS-related cookie in a specific way. If successfully exploited, this could allow the attacker to remotely execute arbitrary code on the REDCap server. This vulnerability exists in REDCap 13.0.1 and higher.
- **Critical security fix**: A Blind SQL Injection vulnerability was found when calling certain API methods, in which a malicious user could potentially exploit it and execute arbitrary SQL commands on the database by entering specially-crafted data into a Text field, changing the field to a File Upload field, and then calling the Delete File or Import File API method. This bug affects all known REDCap versions.
- **Major security fix**: An SQL Injection vulnerability was found on a MyCap-related page, in which a malicious user could potentially exploit it and execute arbitrary SQL commands on the database by manipulating an HTTP request in a specially-crafted way. In order to exploit this, the user must be logged in as a REDCap user and must also have one or more instruments enabled as MyCap tasks.
- **Major security fix**: A Cross-site Scripting (XSS) vulnerability was discovered in which a malicious user could potentially exploit it by inserting HTML tags and/or JavaScript in a very specific way on many pages that output user-defined text onto a REDCap webpage. This bug affects all versions of REDCap.
- Bug fix: After unsuspending a user on the Browse Users page on the "View User List By Criteria" tab, the "Display only X users" drop-down would mistakenly get reset. (Ticket #208937)
- Bug fix: A new Clinical Data Mart background process would not be scheduled if the current one was taking too long to complete.
- Bug fix: PHP 8 related fix for the Data Import Tool. (Ticket #208086)
- Bug fix: When using Multi-Language Management with the e-Consent Framework, some text on the e-Consent confirmation screen at the end of the survey was mistakenly not translatable.
- Bug fix: When using Multi-Language Management, the language switcher and globe menu would not work on survey return pages when the survey is set up to show a logo and the option to "Hide survey title on survey page when display logo" is turned on. (Ticket #208961)
- Bug fix: When using Multi-Language Management on a survey where Google reCAPTCHA is enabled, the Google reCAPTCHA text would mistakenly not be translatable. (Ticket #208797)
- Bug fix: PHP 8 related issue on certain MyCap pages in project. (Ticket #208688)
- Various fixes and changes for the External Module Framework, including 1) Documented sanitizeFieldName() method, and 2) Miscellaneous security scan & documentation improvements.
- Bug fix: In some situations, the survey page might mistakenly throw a fatal PHP error for PHP 8. (Ticket #208147)