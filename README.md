# Automated Outreach Workflow (n8n + Gmail + Google Sheets)

This repository documents the automated outreach workflow built with **n8n**, integrating **Google Sheets** for lead management and **Gmail** for personalized email sequences.  

The workflow handles:
- Reading leads from a Google Shee
- Sequencing outreach emails (up to 3 steps)  
- Skipping contacts who replied or opted out  
- Logging replies back into the sheet  
- Sending emails via Gmail API with RFC822 `raw` payload  

---

## Workflow Overview

1. **Google Sheets Input** → Reads leads (name, email, company, etc.).  
2. **Code Node** → Decides which step of the sequence to send and builds the Gmail RFC822 payload.  
3. **HTTP Request (Gmail API)** → Sends the email via authenticated Gmail OAuth2.  
4. **Reply Check** → Detects replies and updates the sheet.  
5. **Loop & Merge** → Handles multiple leads in a batch with wait times between sends.  

---

## Workflow Screenshots  

Below are key points of the workflow with reference images (replace links with your actual screenshots):  

1. **Google Sheets Input Node**  
   Reads lead data from the sheet.  
   ![Google Sheets Input](n1.png)

2. **Code Node (RFC822 Builder)**  
   Prepares the email subject, body, and raw payload.  
   ![Code Node](n5.png)

3. **HTTP Request Node (Send Email)**  
   Posts the `raw` payload to Gmail API.  
   ![HTTP Request Node](n3.png)

4. **Reply Detection**  
   Checks if a recipient replied and updates the sheet accordingly.  
   ![Reply Detection](n2.png)

5. **Full Workflow Canvas**  
   The complete pipeline showing all connected nodes.  
   ![Full Workflow](n4.png)
   

---

## Setup Instructions  

1. **Clone this repo** or import the workflow JSON into n8n.  
2. Set up **Google OAuth2 credentials** for Gmail and Sheets.  
3. Update your Google Sheet with columns:  
```

first\_name, last\_name, email, email1\_subject, email1\_body,
email2\_body, email3\_subject, email3\_body, sender\_email,
email1\_sent, email2\_sent, email3\_sent, replied, opted\_out

```
4. Run the workflow — emails will send automatically based on sequence logic.  

---

## Key Features  

- Automatically skips leads who replied or opted out  
- Handles up to 3 follow-up steps  
- Sends emails using Gmail’s official API (not SMTP)  
- Logs results back into Google Sheets  
- Modular and easily extendable  

---

## License  
MIT License — free to use, modify, and distribute.  

