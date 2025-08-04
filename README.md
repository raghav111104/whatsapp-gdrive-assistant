## 📁 WhatsApp-Driven Google Drive Assistant (n8n Workflow)

Automate Google Drive actions via WhatsApp using n8n — list, delete, move, and summarize documents by sending simple commands like `LIST /ProjectX` or `SUMMARY /Reports`.

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

Fill in the required values:

```env
TWILIO_AUTH_TOKEN=...
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...
OPENAI_API_KEY=... (optional)
```

#### 3. Start n8n via Docker

```bash
docker-compose up -d
```

n8n will be accessible at: [http://localhost:5678](http://localhost:5678)

---

### 🔀 Supported Commands (via WhatsApp)

| Command                         | Example                              | Description                             |
| ------------------------------- | ------------------------------------ | --------------------------------------- |
| `LIST /Folder`                  | `LIST /ProjectX`                     | Lists all files in `/ProjectX`          |
| `DELETE /Folder/file.pdf`       | `DELETE /ProjectX/report.pdf`        | Sends confirmation and deletes file     |
| `MOVE /Source/file.pdf /Target` | `MOVE /ProjectX/report.pdf /Archive` | Moves a file between folders            |
| `SUMMARY /Folder`               | `SUMMARY /Reports`                   | Sends summaries of all text-based files |

---

### 🧐 Natural Language Support

You can also use phrases like:

* “Can you show what’s in /Reports?”
* “Please remove /ProjectX/oldfile.pdf”

The system maps them to the correct command automatically.

---

### 📜 Logs

Every action is logged to a Google Sheet:

* Timestamp
* Command
* WhatsApp sender
* Status

---

### 🐞 Error Handling

* Invalid commands return a friendly fallback message.
* Mass deletes require confirmation (e.g., “Yes, delete”).
* Failures are logged for debugging.

---

### 🎥 Demo Video

[Watch demo here](https://your-demo-link.com) *(Replace with actual link)*

---

### 📁 Files Included

* `workflow.json` — Import this into n8n
* `.env.sample` — Template for environment variables
* `docker-compose.yml` — Start n8n via Docker
* README — You’re reading it!

---

### 📌 Notes

* You can expand this to support uploads, renames, or reminders.
* AI summarization works only on readable text content.
