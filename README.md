# Parse-Pull-Pass

[Next Page (Top level logic)](/AutoReportFwd/readme.md)

##  Navigating this project

There are readme files in most directories that describe the contents.

Table of contents

1. [Top level logic](/AutoReportFwd/readme.md)
    * [Detailed breakdown](/AutoReportFwd/Flow/readme.md)

# General summary

## What is this? 

This is a mechanism I built in PowerAutomate that will parse an email, pull specific information, then pass that into the subject and send off a reply. This is useful if perhaps the email being sent requires specific information in the subject to trigger a rule for the recipient. This flow automates that process.

### The problem to solve

An external report generation system automatically creates monthly performance reports for a wide range of clients and sends them via email to ``user``. These reports contain essential metrics such as account numbers, client names, and performance summaries in the email body. The 8 digit ``Acct#`` (account number) is crucial for linking each report to the right customer account in the internal CRM or reporting system.

However, the external system is not able to modify the subject line to match internal requirements for proper account tracking, nor can it directly send the reports to the internal system due to security, privacy, or formatting limitations. As a result, ``user`` must manually review the email, extract the ``Acct#``, and add it to the subject line before forwarding it to the internal system for further processing.

The rest of this explanation will be in the context of solving this problem.

[Next Page (Top level logic)](/AutoReportFwd/readme.md)