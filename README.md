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

## Workflow Overview

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

## Folder and File Structure

project/
├── JobSearchColdEmailOutreachAgenticSystem.json   # Exported n8n workflow
├── README.md                                      # Project documentation
└── .env.example                                   # Example environment variables

## ⚙️ Setup Instructions

### 1. Prerequisites
- **Docker** installed on your system  
  Follow the n8n Community Edition setup guide: [Install using Docker](https://docs.n8n.io/hosting/installation/docker/)
- **Google Sheets** and **Gmail API** access via Google Cloud Console  
- **OpenAI API Key** for generating personalized messages  
- Import the provided `workflow.json` file into your n8n instance  

### 2. Clone the Repository
```bash
git clone https://github.com/<yourusername>/automated-outreach-n8n.git
cd automated-outreach-n8n
```

### 3. Run n8n with Persistent Storage

```bash
docker run -it \
  -v n8n_data:/home/node/.n8n \
  -v /Users/<yourname>/Documents:/files \
  -p 5678:5678 \
  -e N8N_BRANDING_N8N_POWERED=false \
  -e GENERIC_TIMEZONE="America/Los_Angeles" \
  n8nio/n8n
```

### 4. Import the Workflow

1. Open n8n in your browser: [http://localhost:5678](http://localhost:5678)  
2. Navigate to **Workflows → Import from File**  
3. Select the file **`n8n_workflow_export.json`** from this repository  
4. Once imported, you’ll see the full workflow displayed inside n8n  

---

### 5. Connect Your Credentials

Before running the workflow, connect the necessary credentials:  
- **Google Sheets:** Select or connect your Google account to allow the workflow to read and update the sheet  
- **Gmail:** Authorize access so n8n can send emails from your Gmail account  
- **OpenAI:** Add your API key in the **“Message a model”** node to enable personalized message generation  

---

### 6. Update File Paths

In the **“Read/Write Files from Disk”** node, make sure the resume file path matches your local setup.  
By default, it looks like this:  

```bash
/files/ {Resune.pdf}
```

If your resume is stored in a different folder, update the path accordingly.  
This file will be attached to every email sent by the workflow.  

A sample `data.csv` file is already included in the repository.  
You can use it to test and understand how contact data moves from the sheet to the email automation. 


## Future Improvements

- Integrate open-source LLMs such as **Ollama**, **Mistral**, or **Phi-3** for local generation  
- Add web search context for deeper personalization  
- Build a dashboard for analytics and engagement tracking  
- Schedule automatic runs (daily or weekly)  
- Add fallback handling for failed sends  
