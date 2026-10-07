# Power Automate – Finance Email Attachment Auto-Saver

## Project Overview

This project demonstrates an automated cloud flow built with Microsoft Power Automate to automatically save qualifying email attachments into a controlled OneDrive for Business or SharePoint location.

The project is based on a Finance / Order-to-Cash (O2C) business scenario where operational reports and supporting documents are received through email.

## Business Problem

The manual process of monitoring emails, downloading attachments, renaming files, and saving them to a team folder can result in:

- Missed attachments
- Duplicate downloads
- Inconsistent file naming
- Accidental saving of signature or logo images
- Limited processing traceability

## Objective

Build an automated cloud flow that identifies qualifying emails, evaluates each attachment against business rules, and saves valid attachments using a collision-resistant file name.

The flow also provides visible failure handling through run history and a dedicated error path.

## Tools & Technologies

- Microsoft Power Automate
- Office 365 Outlook
- OneDrive for Business
- SharePoint

## Flow Type

*Automated Cloud Flow*

The process starts automatically when a qualifying email arrives in the configured mailbox folder.

## Flow Architecture

Outlook Mailbox  
↓  
Email Trigger  
↓  
Attachments Array  
↓  
Apply to each  
↓  
Allowed Extension Condition  
↓  
Create File  
↓  
Run History / Error Handling

## Trigger

*Office 365 Outlook – When a new email arrives (V3)*

Trigger filtering includes:

- Configured mailbox folder
- Emails with attachments
- Subject containing FIN-DAILY
- Optional approved sender

## Processing Logic

1. A qualifying email arrives.
2. The trigger evaluates the configured email criteria.
3. The attachment collection is passed to an *Apply to each* loop.
4. Each attachment is evaluated individually.
5. The file extension is checked against the allowed file types.
6. Valid attachments are saved to the destination.
7. Unsupported attachments are skipped and logged.
8. Failures are handled through a dedicated error path.

## Allowed File Types

The first build allows:

- .xlsx
- .csv
- .pdf

The following file types are excluded:

- .png
- .jpg
- .jpeg
- .gif

## File Naming

The saved file name uses a timestamp together with the original attachment name to reduce the risk of file-name collisions.

Example:

20261007_153045123_AR_Daily_Report.xlsx

## Key Power Automate Concepts Demonstrated

- Automated Cloud Flow
- Outlook Connector
- OneDrive / SharePoint Connector
- Dynamic Content
- Arrays
- Apply to each
- Conditions
- Expressions
- Scope
- Compose
- Create file
- Configure run after
- Try / Catch / Finally
- Run History

## Allowed Extension Expression

```text
or(
  endsWith(toLower(item()?['name']), '.xlsx'),
  endsWith(toLower(item()?['name']), '.csv'),
  endsWith(toLower(item()?['name']), '.pdf')
)
