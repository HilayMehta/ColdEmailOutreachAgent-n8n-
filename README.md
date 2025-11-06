# Job Search Email Outreach Agentic Workflow -n8n

This project is an agentic workflow built with n8n to automate personalized cold emails for job search outreach.
It reads founder or recruiter details from a Google Sheet, uses an AI model to customize a pre-defined email template for each contact, and sends the emails automatically through Gmail.
After each email is sent, the workflow updates the Google Sheet to track who has been contacted, making the entire process efficient, personalized, and fully automated.

---

## Features

- Pulls contact details (name, title, company, LinkedIn profile, etc.) directly from **Google Sheets**.  
- Based on user input, filters and selects a set number of contacts for each run.  
- Uses an **LLM (OpenAI API)** to generate personalized email messages one by one.  
- Sends emails automatically through **Gmail** with attached resume.  
- Updates the **Google Sheet** to mark each contact as “Email Sent.”  
- Fully automated, modular, and easy to extend for other outreach workflows or APIs.

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
   Loads the resume (PDF) from the local directory for email attachment.

6. **Send a Message (Gmail)**  
   Sends the personalized email to each contact with the generated message and attached resume.

7. **Update Row in Sheet**  
   Marks the corresponding contact row as “Email Sent” along with a timestamp.

---

## 🧠 Folder and File Structure

