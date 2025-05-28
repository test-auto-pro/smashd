# 🔁 Social Media Automation System Help Documentation

This repository contains a **S**ocial **M**edia **A**utomation **S**ystem for posting visual content to **9 social media platforms** via [Blotato API](https://blotato.com/?ref=aiacntnt) and [n8n](https://n8n.io).

- **n8n** is an open-source workflow automation tool that lets you build automated processes with no/low coding skills.
- **Blotato** is an AI-powered content creation and distribution platform designed to streamline the process of producing high-quality, consistent content across multiple social media platforms

---

## 🚀 Purpose

This system automates the process of publishing visual content across multiple social media platforms.

It performs the following:

- Detects new content (videos, images) added to a specific Google Drive folder
- Logs the content details into a Google Sheet
- Uses the n8n automation platform to post that content to up to 9 platforms via the Blotato API
- Tracks which platforms each piece of content was published to in the same sheet
---

## 📦 What's Included

This repo (or downloadable zip folder) contains:

- `Video/` folder:
  - 10 sample videos for testing
  - A Google Sheet: `Publish to 9 Social Platforms`  
    - Contains:
      - `Settings` tab — for running Apps Script manually
      - `ContentData` tab — where file data is populated and tracked
- `apps_script.gs` — Apps Script for pulling file metadata into the sheet
- `publish_9_social_platforms_n8n_byTAP.json` — the complete, production-ready n8n workflow template

---

## ⚙️ Prerequisites

| Tool               | Type                | Notes                                                  |
|--------------------|---------------------|---------------------------------------------------------|
| **Google Drive**   | Free                | Stores videos and drives the content pipeline          |
| **Google Sheets**  | Free                | Used to manage post data and status tracking           |
| **Apps Script**    | Free                | Embedded in the Google Sheet to automate detection     |
| **Blotato**        | **Paid**            | Social media API abstraction layer                     |
| **n8n**            | Free Trial / Free   | 14-day Cloud trial or Local Installation (free)               |
| **Canva** *(optional)* | Free/Paid     | Used to create faceless video templates                |

> 📌 Note: n8n Cloud offers 14-day free trial. Self-hosted version is free — setup guide coming soon.

---

## 📥 Setup Instructions

### 1. **Download the Project Files**

- Download the zip file from this repo
- Extract the contents to your Google Drive under the following structure:

```
/My Drive/Video/
├── CanvaVideo01.mp4
├── CanvaVideo022.mp4
├── ...
└── Publish to 9 Social Platforms (Google Sheet)
```

---

### 2. **Share the Video Folder**

- Open your `/Video` folder in Google Drive
- Right-click and choose **“Share”**
- Set sharing to:
  - “Anyone with the link”
  - Viewer access is sufficient
- This allows Apps Script to generate valid public File URLs

---

### 3. **Open the Google Sheet**

- File: `Publish to 9 Social Platforms`
- Tabs:
  - `Settings` — contains a "Run Now" button
  - `ContentData` — where the automation will populate file data

---

### 4. **Run the Apps Script**

- Open the **Settings** tab
- Click the `Run Now` button to trigger the Apps Script
  - This will:
    - Scan the `/Video` folder
    - Detect all new files of these types: `.mp4`, `.mov`, `.avi`, `.png`, `.jpg`, `.jpeg`, `.gif`
    - Populate the `ContentData` sheet with:
      - Filename
      - File URL
      - Default caption
      - Status = "In Progress"
- Captions, titles, and hashtags can be edited manually before publishing

---

### 5. **Set Up Blotato and Get API Keys**

- Create an account at [blotato.com](https://blotato.com) (Paid)
- Connect your social media accounts
- Copy your API key and each platform’s Account ID
- These are entered once in the **Settings node** inside n8n

---

### 6. **Import the n8n Workflow**

- Open your n8n instance (cloud or self-hosted)
- Import `publish_9_social_platforms_n8n_byTAP.json`
- Configure:
  - Google Sheets credentials
  - Blotato API Key and account IDs
  - OpenAI key (optional, for title generation)

---

### 7. **Distribute Content**

- Run the workflow manually or via a schedule
- Each run:
  - Pulls the next `"Ready to Post"` row from `ContentData`
  - Posts to all enabled social networks
  - Updates each network's column with `"Posted on [timestamp]"`
  - Marks the `Status` column as `"Posted"`

---

## 📌 Notes

- Currently supports one post at a time (one file per run)
- Each platform is independently optional — if a node is disabled, it's skipped
- The workflow was designed to be duplicated and sold as a **packaged automation system**

---

## 🛠 Roadmap

- Add OpenAI integration to generate titles from captions
- Add auto-caption generation based on video/audio analysis
- Add retry logic and error logging
- Build out template versions for:
  - Faceless niche creators
  - ADHD / neurodivergent workflows
  - AI avatar video publishing

---

## 🧠 Built With

- **n8n** – low-code automation platform
- **Blotato** – unified social media posting API
- **Google Drive / Sheets** – file system + structured content source
- **Canva** – to generate faceless, scroll-stopping video content

---

Created by [TestAutomationPro](https://www.instagram.com/test.automation.pro/) — automating the automation, so creators can focus on what matters.
