# Scan-Fix-lead-automation

# 📌 n8n Lead Automation System

## 🧾 Project Overview

This project is an automated lead management system built using **n8n**. It captures incoming customer leads, stores them in Google Sheets, and automatically sends notifications via email and SMS.

The system is designed to be simple, scalable, and easy to duplicate for multiple clients or contractors.

---

## ⚙️ What This Workflow Does

When a new lead is submitted:

1. Collects customer data from a form or webhook
2. Saves lead information into Google Sheets
3. Sends a confirmation email to the customer
4. Sends an SMS notification (if enabled via consent)
5. Sends a contractor alert with lead details
6. Sends a remider email

---

## 📊 Google Sheet Structure (Database Schema)

This system uses Google Sheets as a lightweight database.

⚠️ IMPORTANT: Column names must match exactly with the workflow mapping.

### 🧾 Contractor & Source Tracking

* `contractor_id` → Unique ID for routing leads to the correct contractor
* `contractor_name` → Name of the assigned contractor
* `directory_id` → Campaign or directory identifier
* `lead_source` → Source of the lead (website, ads, referral, etc.)
* `page_url` → Page URL where the lead was submitted

---

### 👤 Customer Information

* `full_name` → Customer full name
* `phone` → Phone number
* `email` → Email address
* `address` → Full address
* `city` → City

---

### 🛠️ Service Request Details

* `service_type` → Type of service requested
* `urgency` → Priority level (Low / Medium / High)
* `issue_summary` → Short description of the issue

---

### 📞 Communication Preferences

* `preferred_contact_method` → Email / SMS / Call
* `best_time_to_call` → Preferred calling time
* `consent_sms` → YES / NO (used for SMS compliance control)

---

### 📌 Recommended (Optional Enhancements)

* `status` → Lead status (NEW / CONTACTED / WON / LOST)
* `created_at` → Timestamp of lead creation
* `updated_at` → Last update timestamp
* `lead_score` → Priority score (1–10)

---

## 🔐 Required Setup (Credentials)

To run this workflow, you need to connect the following services inside n8n:

### 1. Google Sheets

* Enable Google Sheets API
* Create OAuth credentials in Google Cloud
* Connect credentials in n8n

### 2. Email (Gmail or SMTP)

* Connect Gmail OAuth or SMTP server
* Used for sending customer confirmation emails

### 3. Twilio (Optional for SMS)

* Create Twilio account
* Get Account SID and Auth Token
* Add verified phone number

---

## ⚙️ Workflow Logic

* Validate incoming lead data
* Normalize fields (name, email, phone, service type)
* Save lead to Google Sheets
* If `consent_sms = YES` → send SMS via Twilio
* If email exists → send confirmation email
* Always send contractor notification
* Optionally update status after follow-up

---

## ✉️ Message Templates

### Customer Email

```
Hi {{full_name}},

Thank you for contacting us.
We have received your {{service_type}} request.
Our team will contact you shortly.

Regards,
Support Team
```

---

### SMS Message

```
Hi {{full_name}}, we received your {{service_type}} request. Our team will contact you soon.
```

---

### Contractor Alert Email

```
New Lead Received:

Name: {{full_name}}
Phone: {{phone}}
Email: {{email}}
Service: {{service_type}}
Urgency: {{urgency}}
```

---

## 🚀 How to Use This Workflow

1. Import `workflow.json` into n8n
2. Connect all required credentials
3. Update Google Sheet ID inside nodes
4. Ensure column mapping matches exactly
5. Activate the workflow
6. Test with a sample lead submission

---

## 🔁 How to Duplicate for Another Client

To reuse this system for another contractor:

1. Export the workflow JSON
2. Import into n8n
3. Update:

   * Google Sheet ID
   * Contractor email(s)
   * Twilio number (if used)
   * Message templates
   * Contractor ID mapping logic
4. Activate the new workflow

---

## 📌 Important Notes

* Always use **Production Webhook URL** (not test URL)
* Ensure workflow is **Active**
* Do not change Google Sheet column names after setup
* Always test SMS/email before going live

---

## 📞 Support

If any issue occurs during setup, check:

* Credential connections
* Webhook activation status
* Google Sheet permissions
* Twilio SMS compliance settings (A2P if applicable)

---

## ✅ Summary

This system fully automates lead handling:

* Captures and stores leads
* Routes leads to correct contractors
* Sends instant notifications
* Reduces manual work
* Scales easily for multiple clients

---

**End of Document**
