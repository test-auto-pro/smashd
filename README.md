# 🔁 Social Media Automation System Help Documentation

This repository contains a **S**ocial **M**edia **A**utomation **S**ystem for posting visual content to **9 social media platforms** via [Blotato API](https://blotato.com/?ref=aiacntnt) and [n8n](https://n8n.io).

- **n8n** is an open-source workflow automation tool that lets you build automated processes with no/low coding skills.
- **Blotato** is an AI-powered content creation and distribution platform designed to streamline the process of producing high-quality, consistent content across multiple social media platforms

---
## 🚀 Description 

This system automates the process of publishing visual content across multiple social media platforms.

It performs the following:

- Detects new content (videos, images) added to a specific Google Drive folder
- Logs the content details into a Google Sheet, on demand or scheduled 
- Uses the n8n automation platform to distribute the content to up to 9 platforms via the Blotato API
- Tracks which platforms each piece of content was published to and when it was published in the same sheet

---

## ⚙️ Prerequisites

| Tool               | Type                | Notes                                                  |
|--------------------|---------------------|---------------------------------------------------------|
| **Google Drive**   | Free                | Stores videos and drives the content pipeline          |
| **Google Sheets**  | Free                | Used to manage post data and status tracking           |
| **Apps Script**    | Free                | Embedded in the Google Sheet to automate new content detection     |
| **Blotato**        | **Paid**            | Social media API abstraction layer                     |
| **n8n**            | Free Trial / Free   | 14-day Cloud trial or [FREE Local n8n Installation](local_n8n.md)              |
| **Canva** *(optional)* | Free/Paid     | Used to create faceless videos               |

> 📌 Note: n8n Cloud offers 14-day free trial. Self-hosted version is free — see local setup guide.

---

## 📥 Setup Instructions

### 1. **Download the Project Files**

- Download the zip file from this repo
- Extract the contents to your Google Drive, **'Video'** folder. 

 Sample structure:

```
/My Drive/Video/
├── CanvaVideo01.mp4
├── CanvaVideo02.mp4
├── publish_9_social_platforms_n8n_byTAP.json
└── Publish to 9 Social Platforms (Google Sheet)

```

---

### 2. **Share the Video Folder**
```
IMPORTANT! Do not skip this step
```
- Open your `/Video` folder in Google Drive in the browser
- Right-click and choose **“Share”**
- Set sharing to:
  - “Anyone with the link”
  - Viewer access is sufficient
- This allows Apps Script to generate **valid public File URLs**

---

### 3. **Open the Google Sheet**

- File: `Publish to 9 Social Platforms`
- Tabs/Sheets:
  - `Settings` — contains Description and functionality to populate the sheet on demand via a "Run Now" button or schedule the auto population.
  - `ContentData` sheet — where the script will populate file data
  - `ContentData` sheet can be populated manually.
        - Before running the n8n workflow make sure at least one row in ContentData sheet is set to 'Ready to Post' in the Status column
  -  `Metadata`sheet  — populate manually for titles and captions to be randomly selected, see ContentData first row example, Title and Caption columns contain formula to get random values from Metadata sheet

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

- The First run: Open Apps Script  Window> Extension Apps Script > Run Button

 - Accept the security warning during the Script execution.

---

### 5. **Set Up Blotato and Get API Keys**

- Create an account at [blotato.com](https://blotato.com/?ref=aiacntnt) (Paid)
- Connect your social media accounts
- Copy your API key and each platform’s Account ID
- These are entered once in the **Settings node** inside n8n

---

### 6. **Import the n8n Workflow**

* Register an account with n8n and get a 14-day free trial
  *(later you can set up your own free local instance if preferred)*
* Open your n8n instance (cloud or local)
* Import `publish_9_social_platforms_n8n_byTAP.json`
* Configure:

  * **Google Sheets connection 1 - Google Sheets NODE**: Connect to the 'Publish to 9 Social Platforms' Google Sheet

    * This is the first node — it reads data where the **Status** column equals **Ready to Post**
  * **Setup Social Accounts NODE**: Add your Blotato API key and account IDs
  * **Google Sheets connection 2 - Update Network Status NODE**: Connect to the same sheet

    * This is the final node — it updates the sheet by setting the **Status** and **Date Posted** for rows matching the **Video URL*


---
### 7. **Test the Set Up**
- Test each node first 
- Each time the workflow is executed 
---
### 8. **Distribute Content**

- Run the workflow manually or via a schedule
- Each run:
  - Pulls the next `"Ready to Post"` row from `ContentData`
  - Posts to all enabled social networks (Corresponding n8n node is active)
  - Updates Google sheet for each network's column with `"Posted on [timestamp]"`
  - Marks the `Status` column as `"Posted"`

---

## 📌 Notes

- Built to maximize efficiency and minimize cost. 
- Supports one post at a time (one file/data row per run)
- Supports scheduling via n8n, i.e. post every 8 hours (3 times a day)
- Each platform is independently optional — if a node is disabled, it's skipped

---

## 🛠 Roadmap

- Add OpenAI integration to generate titles, captions, hashtags for specified niche
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
- **Canva** – to generate faceless, video content

---

Created by [TestAutomationPro](https://www.instagram.com/test.automation.pro/) — automating the automation, so creators can focus on what matters.
👉 Don't do it a̶g̶a̶i̶n̶. Automate! 🚀
