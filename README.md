## 📁 WhatsApp-Driven Google Drive Assistant (n8n Workflow)

Automate Google Drive actions via WhatsApp using n8n — list, delete, move, and summarize documents by sending simple commands like `LIST /ProjectX`, `DELETE /ProjectX/file.pdf`, `MOVE /ProjectX/file.pdf to /Archive`, or `SUMMARY /Reports`.

---

### 🚀 Features

* 📂 List files in a Google Drive folder
* 🗑️ Delete specific files (with confirmation)
* 📁 Move files between folders
* 🧐 Summarize documents (PDF, DOCX, TXT) using AI
* 🧾 Logs every action to a Google Sheet
* ⚠️ Handles invalid input with helpful feedback
* 🧐 Parses basic natural language commands

---

### 🔧 Prerequisites

* [Twilio WhatsApp Sandbox](https://www.twilio.com/console/sms/whatsapp/learn)
* Google Cloud project with:

  * Google Drive API enabled
  * OAuth2 client credentials
* OpenAI (optional — if using GPT)

> ⚠️ All Google Drive files or folders you want to interact with must be **owned by or shared with** the Google account used in your OAuth2 credentials.

---

### 📥 Setup Instructions

#### 1. Clone the Repo

```bash
git clone https://github.com/your-username/whatsapp-gdrive-assistant
cd whatsapp-gdrive-assistant
```

#### 2. Environment Variables

Create a `.env` file using the provided `.env.sample`:

```bash
cp .env.sample .env
```

Then fill in the required values with your own credentials:

* Twilio Account SID and Auth Token
* Google OAuth2 Client ID, Secret, Refresh Token, and Redirect URI
* (Optional) OpenAI API Key if summarization is enabled

> ⚠️ **You must have working Twilio and Google Drive credentials** for the workflow to function.

#### 3. Start n8n via Docker

```bash
docker-compose up -d
```

n8n will be accessible at: [http://localhost:5678](http://localhost:5678)

#### 4. Import the Workflow

1. Open n8n in your browser
2. Click the three-dot menu (⋮) in the top-right
3. Select **Import** and choose the `workflow.json` file from this repo

---

### 🔀 Supported Commands (via WhatsApp)

| Command                            | Example                                 | Description                             |
| ---------------------------------- | --------------------------------------- | --------------------------------------- |
| `LIST /Folder`                     | `LIST /ProjectX`                        | Lists all files in `/ProjectX`          |
| `DELETE /Folder/file.pdf`          | `DELETE /ProjectX/report.pdf`           | Sends confirmation and deletes file     |
| `MOVE /Source/file.pdf to /Target` | `MOVE /ProjectX/report.pdf to /Archive` | Moves a file between folders            |
| `SUMMARY /Folder`                  | `SUMMARY /Reports`                      | Sends summaries of all text-based files |

---

### 🧐 Natural Language Support

You can also use phrases like:

* “Can you show what’s in /Reports?”
* “Please remove /ProjectX/oldfile.pdf”
* “Move report.pdf from ProjectX to Archive”

The system maps them to the correct command automatically.

---

### 📜 Logs

Each WhatsApp command (`LIST`, `DELETE`, `MOVE`, `SUMMARY`) is logged in a connected Google Sheet with the following details:

* Timestamp
* Command issued
* File name (if applicable)
* Source and/or destination folder
* WhatsApp sender number
* Result message (e.g. success, file not found, failed)

---

### 🐞 Error Handling

* Invalid commands return a friendly fallback message.
* Mass deletes require confirmation (e.g., “Yes, delete”).
* Failures are logged for debugging.

---

### 🎥 Demo Video

https://drive.google.com/drive/folders/1axpz6TuCsnqu7-ezgxYj-h8YgkhXPfTP?usp=drive_link

---

### 📁 Files Included

* `WhatsApp-Driven Google Drive Assistants.json` — Import this into n8n
* `.env.sample` — Template for environment variables
* `docker-compose.yml` — Start n8n via Docker
* README — You’re reading it!

---

### 📌 Notes

* You can expand this to support uploads, renames, or reminders.
* AI summarization works only on readable text content.
* You must import the workflow manually from the UI using `workflow.json`
* ✅ Files/folders **must be owned by or shared with the authenticated Google account** to be accessed or modified.
