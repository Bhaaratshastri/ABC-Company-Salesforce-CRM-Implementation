# WI004 - ABC Customer Account Registration and Data Import

## 1. Objective & Business Value
Establish a centralized customer `Account` management solution in Salesforce for ABC Company by migrating existing customer organization records from spreadsheets into the standard Salesforce `Account` object. This eliminates spreadsheet fragmentation and provides Sales Representatives and Sales Operations with a single, reliable source of truth.

---

## 2. Salesforce Account Data Model & Schema Builder Analysis
Using **Setup → Schema Builder** (selecting `Account`, `Contact`, `Opportunity`, `Case`, and `User`), the following standard architecture was verified to ensure zero unnecessary customization:

* **Standard Object Used:** `Account`
* **Key Standard Relationships:**
  * **Account → Contact** (`1-to-Many`): Tracks individual points of contact at each customer organization.
  * **Account → Opportunity** (`1-to-Many`): Tracks sales deals and revenue pipeline associated with the account.
  * **Account → Case** (`1-to-Many`): Tracks customer service inquiries and support tickets.
  * **Account → Account (`ParentId`)** (`Self-Lookup`): Supports parent-subsidiary corporate hierarchies.
  * **User → Account (`OwnerId`)** (`1-to-Many Lookup`): Assigns Sales Representative ownership.

---

## 3. Source Data & CSV-to-Salesforce Field Mapping

* **Source File Location:** `data/abc_customer_accounts.csv` (kept separate from `force-app/` Salesforce metadata)
* **Encoding:** UTF-8

### Field Mapping Specification

| CSV Column Header | Salesforce Field Label | API Name | Data Type | Import Validation Notes |
| :--- | :--- | :--- | :--- | :--- |
| `Account Name` | Account Name | `Name` | Text (255) | **Required.** Used as the matching key (*Match Account by: Name*) to prevent duplicates. |
| `Account Number` | Account Number | `AccountNumber` | Text (40) | Legacy spreadsheet ID (`ABC-1001` to `ABC-1003`) used for export reconciliation. |
| `Type` | Type | `Type` | Picklist | Standard picklist value `Customer - Direct` is active in the org. |
| `Industry` | Industry | `Industry` | Picklist | Standard picklist value `Manufacturing` is active in the org. |
| `Phone` | Phone | `Phone` | Phone | International format (`+91-XX-XXXX-XXXX`). |
| `Billing City` | Billing City | `BillingCity` | Text (40) | Maps to the City component of the standard `BillingAddress` compound field. |

### Imported Records Summary

| Account Name | Account Number | Type | Industry | Phone | Billing City |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apex Industrial Supplies Pvt Ltd | ABC-1001 | Customer - Direct | Manufacturing | +91-79-4000-1234 | Ahmedabad |
| Northstar Manufacturing Pvt Ltd | ABC-1002 | Customer - Direct | Manufacturing | +91-261-4000-2345 | Surat |
| Western Components Ltd | ABC-1003 | Customer - Direct | Manufacturing | +91-265-4000-3456 | Vadodara |

---

## 4. Import, Error Handling & Export Reconciliation Procedure

1. **Data Import:**
   * Navigated to **Setup → Data Import Wizard → Launch Wizard**.
   * Selected **Standard Objects → Accounts and Contacts → Add new records**.
   * Configured *Match Account by* = **Name**, uploaded `data/abc_customer_accounts.csv`, verified all 6 columns mapped cleanly, and initiated the import.
2. **Error Identification & Job Monitoring:**
   * Monitored **Setup → Bulk Data Load Jobs** to confirm `Records Processed = 3` and `Records Failed = 0`.
   * Verified the **View Result** CSV log (`sf__Id`, `sf__Created`, `sf__Error`) to confirm valid 18-character Salesforce Account IDs and zero errors.
3. **Export Reconciliation:**
   * Exported the imported Account records via **Setup → Data Export** (and verified via an **Accounts** tabular report CSV export).
   * Reconciled exported rows against `data/abc_customer_accounts.csv` to confirm 100% data accuracy.

---

## 5. Peer Validation Test Steps

| Test ID | Test Scenario | Steps to Execute | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-01** | Verify Standard Object & Schema Relationships | Open **Setup → Schema Builder** and select `Account`, `Contact`, `Opportunity`, `Case`, and `User`. | Standard `Account` object displays standard fields and lookup relationships without redundant custom objects or fields. | Pass |
| **TC-02** | Validate CSV Format & Metadata Separation | Inspect repository directories (`data/` vs. `force-app/`). | `abc_customer_accounts.csv` is stored in `data/`, encoded in UTF-8, contains 3 rows, and is isolated from `force-app/`. | Pass |
| **TC-03** | Import Customer Accounts via Data Import Wizard | Launch **Setup → Data Import Wizard**, select **Accounts and Contacts → Add new records**, upload `abc_customer_accounts.csv`, and map columns. | All 6 CSV columns map cleanly to standard `Account` fields with zero unmapped columns. | Pass |
| **TC-04** | Verify Bulk Data Load Job & Error Handling | Open **Setup → Bulk Data Load Jobs** and inspect the recent job and result CSV. | Job status is `Completed`, `Records Processed: 3`, `Records Failed: 0`, and `sf__Error` is blank. | Pass |
| **TC-05** | Verify Imported Records in Salesforce UI | Navigate to the **Accounts** tab in the Sales App and inspect each of the 3 records. | All 3 customer Accounts appear with accurate Name, Account Number, Type, Industry, Phone, and Billing City. | Pass |
| **TC-06** | Export & Reconcile Customer Information | Export Account records via **Setup → Data Export** (or Accounts Report Export CSV) and compare with source CSV. | Exported CSV contains all 3 records matching Salesforce UI and `data/abc_customer_accounts.csv`. | Pass |