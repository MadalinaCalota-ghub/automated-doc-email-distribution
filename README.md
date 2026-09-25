# 📧 Automated Document Parsing & Bulk Email Distribution Pipeline

An automated ETL and email dispatch workflow built in **Make.com** that extracts recipient lists from unparsed Google Docs files, dynamically splits and iterates through email addresses, attaches presentation assets from Google Drive, and dispatches targeted emails via Gmail API.

---

## 🎯 Project Overview & Business Value
In marketing and client outreach operations, contact lists often arrive in unstructured text formats (e.g., comma-separated strings inside documents or raw notes). 

This automation solves the manual effort of copy-pasting contacts by:
1. **Extracting raw text data** automatically from central Google Docs repository files.
2. **Parsing and array iteration** of comma-separated email addresses into individual queue items.
3. **Retrieving dynamic attachments** (e.g., PowerPoint presentations, sales decks) stored in Google Drive.
4. **Automating direct email delivery** via Gmail integration with custom attachments.

---

## 🏗️ Workflow Architecture & Data Flow
[ Google Docs ] ➔ [ Google Drive ] ➔ [ Iterator (Split & Map) ] ➔ [ Gmail API ]
   (Fetch Text)      (Download Deck)     (Parse & Loop Emails)     (Dispatch Emails)
   
### Process Breakdown:
1. **Google Docs (Get Content of a Document):** Fetches the raw text content from the source file containing batch email entries.
2. **Google Drive (Download a File):** Downloads the target file asset (e.g., presentation slides, campaign media) to be attached.
3. **Flow Control - Iterator:** Uses string manipulation `split(Text Content; ,)` to transform raw comma-separated email strings into structured array elements for individual processing.
4. **Gmail (Send an Email):** Loops through each parsed email address, attaching the downloaded presentation file and sending personalized content.

---

## 📸 Technical Implementation

### Make.com Automation Blueprint
![Make Workflow](Screenshot%202026-09-25%20fluxMake_Integration%20Google%20Docs.png)

### Data Parsing & Array Iteration Logic
The `Iterator` module handles the transformation from a single comma-separated text block into discrete email recipients:
```text
Input:  "calota.ancamadalina@gmail.com, razvan.calota@gmail.com, gabriel.calota13@gmail.com"
Logic:  split(2.Text Content; ,)
Output: 3 distinct execution bundles sent sequentially to Gmail.
