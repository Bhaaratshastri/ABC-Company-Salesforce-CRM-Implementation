# WI001 - Salesforce CRM Foundations and Environment Setup

## Overview
This document records the completion of the individual Salesforce development
environment setup and foundational CRM knowledge required before participating
in ABC Company's CRM implementation project.

## 1. Trailhead Playground
- Org Type: Trailhead Playground
- Org ID: 00DNS0000166ffd
- Edition: Developer Edition
- Access confirmed via: Salesforce Lightning Experience
- Credential storage: Stored securely in [password manager name, e.g., 1Password/Bitwarden],
  not committed to source control or shared in plaintext.

## 2. Navigation & App Access
- Confirmed access to the **Sales** application via the App Launcher (grid icon).
- Reviewed primary Sales app tabs: Home, Accounts, Contacts, Opportunities, Leads.
- Located **Setup** (gear icon, top right) and navigated to **Object Manager**.

## 3. Standard Objects Reviewed
| Object   | Type     | Notes                                      |
|----------|----------|---------------------------------------------|
| Account  | Standard | Represents companies/organizations          |
| Contact  | Standard | Represents individuals linked to an Account |

## 4. Core Concepts
- **Object**: A data structure representing a type of record (e.g., Account) — similar to a database table.
- **Field**: An individual attribute on an object (e.g., Account Name, Phone) — similar to a column.
- **Record**: A single instance/entry of an object (e.g., one specific company's Account).

## 5. Package/App Installation in Playground
- Reviewed **Setup → Installed Packages** to understand how managed packages are installed via
  install URLs (typically provided through Trailhead modules).
- Confirmed understanding that installed packages/apps are scoped to the individual Playground org.

## 6. GitHub Access
- Confirmed access to assigned repository: ABC-Company-Salesforce-CRM-Implementation
- Permanent learner branch confirmed: `learner/bhaarat`
- Work item branch created: `work/bhaarat/WI001`

## 7. Trailhead Badges Completed
- [ ] [[Trailhead Playground Management](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management)]
- [ ] [[Salesforce CRM](https://trailhead.salesforce.com/content/learn/modules/lex_implementation_basics)]

## 8. Trailblazer Profile
- Public profile URL: [https://www.salesforce.com/trailblazer/nsck03joht7pbqdg0x]

## 9. Test Steps (for Peer Validation)
1. Log in to the Trailhead Playground and confirm the UI loads in Lightning Experience.
2. Open the App Launcher and confirm the **Sales** app is listed and opens successfully.
3. Navigate to **Setup → Object Manager** and confirm **Account** and **Contact** objects are visible.
4. Open the **Account** object and confirm standard fields are listed under Fields & Relationships.
5. Open an existing or sample Account record and confirm record-level data displays correctly.
6. Confirm the Trailblazer profile URL above is publicly accessible (open in incognito/private window).
7. Confirm all listed Trailhead badges show as completed on the Trailblazer profile.
8. Confirm the `work/[name]/WI001` branch exists in GitHub and targets `learner/[name]`.

## Trello Reference
- Work Item ID: WI001
- Trello Card URL: [https://trello.com/c/P4iP6E1k/1-wi001-salesforce-crm-foundations-and-environment-setup-learner-1]