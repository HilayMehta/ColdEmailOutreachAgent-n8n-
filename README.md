# ColdEmailOutreachAgent-n8n-

This project automates the process of sending personalized outreach emails to multiple contacts using **n8n**, **Google Sheets**, and the **Gmail API**.  
It generates customized messages with an LLM, attaches a resume, and updates the Google Sheet to track which contacts have already been emailed.

---

## 🧩 Features

- Pulls contact data (name, title, company, LinkedIn, etc.) directly from Google Sheets.  
- Uses an LLM (OpenAI API for now) to craft tailored outreach messages.  
- Randomly selects a specified number of people each run to avoid spamming.  
- Sends emails automatically via Gmail with your attached resume.  
- Updates the Google Sheet to mark each contact as “Email Sent.”  
- Fully customizable and easily extendable to other workflows or APIs.

---

## 🏗️ Workflow Overview

The n8n workflow consists of the following nodes:

1. **Form Submission**  
   Accepts the number of emails to send (e.g., 5, 10, 15).

2. **Get Rows in Sheet**  
   Reads all contact details from a connected Google Sheet.

3. **Code in JavaScript**  
   Filters out rows where the “Email Sent” column is already marked and randomly selects N new contacts to email.

4. **Message a Model (OpenAI)**  
   Generates a short, professional outreach message for each selected contact using a predefined prompt.

5. **Read/Write Files from Disk**  
   Loads the resume (PDF) from your local directory for email attachment.

6. **Send a Message (Gmail)**  
   Sends the personalized email to each contact with the generated message and attached resume.

7. **Update Row in Sheet**  
   Marks the corresponding contact row as “Email Sent” along with a timestamp.

---

## 🧠 Folder and File Structure

