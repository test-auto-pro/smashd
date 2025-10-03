# Social Media Automation System - Setup Guide

## TL;DR - Quick Setup Overview

**Prerequisites:** Google Drive (free), Google Sheets (free), n8n (free or paid options), Blotato (paid), OpenAI API (paid)

**Setup Steps:**
1. **Google Tools:** Create MyContent folder structure → Import Google Sheet → Run Apps Script to scan files
2. **Blotato:** Register account → Connect social platforms → Copy API key
3. **n8n:** Import workflow JSON → Configure 4 credentials (Google OAuth, OpenAI, Blotato) → Activate/deactivate platform nodes → Test run

**First run:** Mark one row "Ready To Post" in Google Sheets → Execute n8n workflow → Verify post scheduled in Blotato → Check Google Sheet updated with timestamps

---

## Introduction

This system posts your original content to up to 9 social platforms, helping solo creators save time and resources on social media distribution without hiring a big team.

Instead of manually logging into each platform and posting the same content repeatedly, you upload once to organized folders. The system generates platform-optimized captions and hashtags, then distributes your content automatically.

**How it works:**

User uploads media files to organized cloud folders by business category. Automated system discovers new files and populates the tracking sheet with file details and default metadata. AI Agent generates platform-optimized titles, captions and hashtags based on content category. n8n workflow sends content to Blotato, which posts to all 9 platforms simultaneously. The system tracks what posted where and when for future repurposing.

**⚠️ IMPORTANT: Test with provided files first**

This package includes 20 test video files (10 in "Process" folder, 10 in "Motivation" folder). You MUST set up and test the system with these provided files and naming conventions first. Once everything works correctly, then customize for your own content and categories.

---

## Prerequisites

Before starting setup, you need active accounts for:

1. **Google Drive** (free)
2. **Google Sheets** (free)
3. **OpenAI API** (paid)
   - Register at platform.openai.com
   - Set up billing and add credit
   - Generate an API key from the API Keys section
4. **n8n** (free or paid - see Glossary for options)
5. **Blotato** (paid - includes free trial)

---

## Chapter 1: Google Tools Setup

### Step 1: Create MyContent Folder Structure

**What you're doing:** Setting up organized cloud storage for your content files.

1. Open your Google Drive
2. Create a new folder named `MyContent`
3. Inside `MyContent`, create two subfolders:
   - `Process`
   - `Motivation`
4. Copy the 20 test video files from your download package:
   - 10 files into the `Process` folder
   - 10 files into the `Motivation` folder

**Your folder structure should look like:**
```
Google Drive
└── MyContent
    ├── Process (10 video files)
    └── Motivation (10 video files)
```

`[SCREENSHOT: Google Drive folder structure showing MyContent with Process and Motivation subfolders]`

5. Open the Google Sheet template from your download package
6. In Google Drive, move this spreadsheet file INTO the `MyContent` folder
7. Your final structure:
```
Google Drive
└── MyContent
    ├── Social_Media_Publisher_PRO_V2.4 (Google Sheet)
    ├── Process (10 video files)
    └── Motivation (10 video files)
```

**Why this matters:** The Apps Script scans from the spreadsheet's location. Both the sheet and content folders must be inside `MyContent`.

---

### Step 2: Import and Understand Google Sheet Structure

**What you're doing:** Understanding your control center for the automation system.

1. Open the Google Sheet you just placed in `MyContent` folder
2. You'll see 3 tabs at the bottom: Settings, ContentData, Metadata

**Settings Tab:**
- Open this tab first
- Read the note about accepted file formats (standard video: .mp4, .mov, .avi; images: .png, .jpg, .jpeg, .gif)
- See the "Run Now" button - you'll use this later
- See the "Enable Autotrigger" dropdown - leave as "No" for now
- No action needed yet

`[SCREENSHOT: Settings tab showing note, Run Now button, and autotrigger controls]`

**ContentData Tab:**
- Open this tab
- Review the column headers:
  - Filename
  - Media URL
  - Content Category
  - Title
  - Caption
  - Status
  - Platform columns (instagram, facebook, tiktok, pinterest, youtube, threads, twitter, linkedin, bluesky)
- This tab is currently empty - it will fill automatically when you run the Apps Script
- No action needed yet

`[SCREENSHOT: ContentData tab showing column headers with empty rows]`

**Metadata Tab:**
- Open this tab
- See 2 pre-populated rows corresponding to your 2 test folders (Process, Motivation)
- Column structure:
  - **Category Folder Name:** Must match Google Drive subfolder name exactly
  - **Business Context:** Full description of audience and positioning
  - **Default Title:** Template used for new content
  - **Default Caption:** Template used for new content

`[SCREENSHOT: Metadata tab showing 2 pre-populated example rows]`

**Pre-populated examples:**

**Process folder context:**
- Audience: Solopreneurs, Side Hustlers and Small Business Owners creating social media content with the purpose of content marketing. Creators who already produce videos or images but get stuck on posting to multiple social platforms. People frustrated by device switching, app juggling, and rewriting titles, captions and CTAs.
- Positioning: AI powered smart automation that removes posting friction. Upload once to Google Drive, system optimizes and posts to 9 platforms. Focus is on eliminating tedious multi-platform, device, app repetition.
- Voice: casual and relatable, like a friend sharing a hack. Emphasizes the ease and relief of having posting handled automatically.

**Motivation folder context:**
- Audience: people interested in manifestation, spiritual growth, and conscious living. Followers of Bashar, Abraham Hicks, and Law of Attraction teachings who scroll for daily reminders of their power and alignment.
- Positioning: stay aligned with your vision through faceless motivational videos that inspire trust, belief, and manifestation without showing a face.
- Voice: calm, clear, outcome-focused. Affirming and uplifting.

**Why this matters:** The AI Agent uses Business Context to generate platform-optimized captions and hashtags that match your brand voice and audience.

---

### Step 3: Run Apps Script to Load Data

**What you're doing:** Automatically discovering your 20 test files and populating the tracking sheet.

1. Go back to the **Settings** tab
2. Click the **"Run Now"** button

**First-time authorization required:**

3. Google will show a permissions dialog
4. Click "Review Permissions"

`[SCREENSHOT: Google Apps Script authorization dialog]`

5. Select your Google account
6. You'll see a warning "Google hasn't verified this app"
7. Click "Advanced" at the bottom
8. Click "Go to [script name] (unsafe)" - this is YOUR script, it's safe

`[SCREENSHOT: Advanced authorization screen]`

9. Click "Allow" to grant permissions:
   - See and download all your Google Drive files
   - View and manage spreadsheets

**After authorization:**

10. The script will run (may take 30-60 seconds for 20 files)
11. Watch cell B3 in Settings tab for status message
12. When complete, you'll see a summary: "Loaded 20 new files"

`[SCREENSHOT: Settings tab showing completion message in B3]`

**Verify the results:**

13. Switch to **ContentData** tab
14. You should see 20 rows of data:
   - 10 rows with Content Category = "Process"
   - 10 rows with Content Category = "Motivation"
   - Each row has Filename, Media URL, default Title and Caption from Metadata tab
   - All rows show Status = "In Progress"

`[SCREENSHOT: ContentData tab with 20 populated rows]`

**Prepare for posting:**

15. Pick ONE row to test with (any file from either folder)
16. Click the Status cell for that row
17. Select "Ready To Post" from the dropdown

`[SCREENSHOT: Status dropdown showing options: In Progress, Ready To Post, Posted]`

18. Leave all other rows as "In Progress" for now

**Why this matters:** Only rows marked "Ready To Post" will be processed by the n8n workflow. This gives you control over what posts and when.

---

## Chapter 2: Blotato Setup

### Step 1: Register for Blotato Account

**What you're doing:** Setting up your multi-platform posting service.

1. Go to Blotato registration page using the affiliate link provided (or blotato.com)
2. Create your account
3. Free trial available

**Why this matters:** Blotato handles the actual posting to all 9 social platforms through one API.

---

### Step 2: Connect Your Social Media Accounts

**What you're doing:** Authorizing Blotato to post on your behalf.

1. Log into your Blotato account
2. Navigate to the "Connect Accounts" or "Social Accounts" section
3. Connect as many of these platforms as you want to use:
   - Instagram
   - Facebook
   - TikTok
   - Pinterest
   - YouTube
   - Threads
   - Twitter
   - LinkedIn
   - Bluesky

**You don't need all 9.** Connect only the platforms you actually use.

4. For each platform, click "Connect" and follow the OAuth authorization flow
5. Grant Blotato posting permissions

`[SCREENSHOT: Blotato dashboard showing connected social accounts]`

**Important note:** Later in the n8n workflow, you'll need to activate/deactivate nodes based on which platforms you connected here. More on this in Chapter 3.

---

### Step 3: Get Your Blotato API Key

**What you're doing:** Getting your authentication credential for n8n to communicate with Blotato.

1. In your Blotato dashboard, go to **Account Settings**
2. Find the **API** or **API Keys** section
3. Click "Generate API Key" or copy your existing key
4. Save this key somewhere safe - you'll need it for n8n setup

`[SCREENSHOT: Blotato settings page showing API key location]`

**For detailed instructions:** See [Blotato API documentation link - to be provided]

**Why this matters:** This API key allows n8n to send your content to Blotato for posting.

---

## Chapter 3: n8n Setup

### Step 1: Import Workflow and Review Instructions

**What you're doing:** Loading the pre-built automation workflow into n8n.

1. Log into your n8n instance (cloud or self-hosted)
2. Click **"Add Workflow"** → **"Import from File"**
3. Select the `workflow.json` file from your download package
4. The workflow will load with all nodes pre-configured

`[SCREENSHOT: n8n import dialog]`

5. You'll see the workflow canvas with multiple connected nodes:
   - Google Drive trigger
   - Google Sheets nodes
   - AI Agent node with OpenAI
   - Multiple Blotato posting nodes (one per platform)

`[SCREENSHOT: n8n workflow overview showing all nodes]`

**Review the workflow structure:**
- **Trigger:** Checks Google Sheets for rows with Status = "Ready To Post"
- **AI Agent:** Generates platform-specific titles, captions, hashtags
- **Blotato nodes:** Post to each platform (9 separate nodes)
- **Update Sheet:** Marks Status as "Posted" and records timestamps

**Why this matters:** Understanding the flow helps you troubleshoot issues and customize later.

---

### Step 2: Configure Credentials and Connections

**What you're doing:** Connecting n8n to your Google Drive, Google Sheets, OpenAI, and Blotato accounts.

This is the most technical step. Take your time.

**Google Drive and Google Sheets (OAuth):**

1. Click on any Google Drive or Google Sheets node
2. Click "Create New Credential"
3. Follow n8n's official documentation for Google OAuth setup: [n8n Google OAuth documentation link]
   - This covers creating a Google Cloud Console project
   - Enabling required APIs
   - Setting up OAuth credentials
   - Configuring redirect URIs

**This is the most technical step.** n8n's documentation provides current, detailed instructions that account for any Google Cloud Console interface changes.

4. After completing OAuth setup following n8n's guide, authorize n8n to access your Google account
5. Select your Google Drive folder (MyContent) for the Google Drive node
6. Select your Google Sheet (Social_Media_Publisher_PRO_V2.4) for the Google Sheets nodes

**OpenAI API:**

1. Click on the AI Agent node
2. Click "Create New Credential" for OpenAI
3. Enter your OpenAI API key (from Prerequisites step)
4. Select model: gpt-4 or gpt-3.5-turbo (depending on your preference)

`[SCREENSHOT: n8n OpenAI credential setup]`

**Blotato API:**

1. Click on any Blotato node
2. Click "Create New Credential"
3. Enter your Blotato API key from Chapter 2, Step 3

`[SCREENSHOT: n8n Blotato credential setup]`

**Activate/Deactivate Platform Nodes:**

4. Look at the 9 Blotato posting nodes (Instagram, Facebook, TikTok, etc.)
5. If you did NOT connect a platform in Blotato, you need to deactivate that node:
   - Right-click the node
   - Select "Deactivate"
   - Deactivated nodes are grayed out

`[SCREENSHOT: n8n showing how to deactivate a node]`

6. Only keep active the platforms you connected in Chapter 2

**Why this matters:** Credentials allow n8n to access your services. Deactivating unused platforms prevents errors.

---

### Step 3: Show Time - First Test Run

**What you're doing:** Running the workflow manually to verify everything works.

**Pre-flight check:** ✈️
- ✓ Google Sheet has 20 rows in ContentData
- ✓ At least ONE row has Status = "Ready To Post"
- ✓ All credentials configured in n8n
- ✓ Only connected platforms are active in workflow

**Execute the workflow:**

1. In n8n workflow canvas, click **"Execute Workflow"** button at the bottom
2. Watch the nodes light up as they process
3. Execution should take 30-60 seconds

`[SCREENSHOT: n8n workflow executing with nodes lighting up]`

**Success indicators:**

**In n8n:**
- All active nodes show green checkmarks
- No red error indicators
- Output data visible in each node

**In Blotato:**
4. Log into your Blotato dashboard
5. Go to "Scheduled Posts" or "Queue"
6. You should see your test post scheduled for 7 days from now
7. **This is intentional** - posts are scheduled in the future so you can test safely and delete if needed

`[SCREENSHOT: Blotato dashboard showing scheduled post]`

**In Google Sheets:**
8. Open your ContentData tab
9. Find the row you marked "Ready To Post"
10. Verify these updates:
    - Status changed from "Ready To Post" to "Posted"
    - Each connected platform column shows:
      - Date/time stamp
      - Platform-specific title (for YouTube)
      - Platform-specific caption
      - Platform-specific hashtags

`[SCREENSHOT: ContentData tab showing updated row with timestamps and captions]`

**If you see all these success indicators: Congratulations! Your system is working.**

**What to do with the scheduled test post:**

11. Go back to Blotato dashboard
12. Find the scheduled post
13. Either:
    - Delete it if you don't want it published, OR
    - Let it publish in 7 days to verify actual posting works, OR
    - Edit the schedule to post sooner

**Test with more content:**

14. Go back to Google Sheets ContentData tab
15. Change another row's Status to "Ready To Post"
16. Run the n8n workflow again
17. Repeat until you're confident the system works

**Why this matters:** Manual testing verifies all components work together before you rely on automation.

---

## Chapter 4: Troubleshooting

### Common Issue 1: Apps Script Permission Errors

**Symptom:** When clicking "Run Now", you see "Authorization required" repeatedly, or script fails to run.

**Solutions:**
1. Clear your browser cache and cookies
2. Try a different browser
3. Make sure you clicked "Advanced" → "Go to [script name]" in the authorization dialog
4. If script is embedded and won't authorize, use the standalone `.gs` file from your package:
   - In Google Sheets, go to Extensions → Apps Script
   - Delete existing code
   - Paste code from the `.gs` file
   - Save and try again

---

### Common Issue 2: n8n Credential Connection Failures

**Symptom:** Red error indicators on nodes saying "Credentials are not valid" or "Authentication failed"

**Solutions:**

**For Google OAuth:**
1. Verify you enabled both Google Drive API AND Google Sheets API in Google Cloud Console
2. Check that your OAuth redirect URI in Google Cloud Console exactly matches what n8n provides
3. Try disconnecting and reconnecting the credential
4. Generate a new OAuth token

**For OpenAI:**
1. Verify your API key is still valid at platform.openai.com
2. Check you have available credit/billing set up
3. Make sure there are no extra spaces when pasting the API key

**For Blotato:**
1. Verify the API key is copied exactly (no spaces)
2. Check your Blotato account is active (not expired trial)
3. Try regenerating the API key in Blotato settings

---

### Common Issue 3: Wrong File Formats

**Symptom:** Apps Script loads files but they don't appear in ContentData, or n8n fails to process certain files.

**Solution:**
1. Check Settings tab note for accepted formats:
   - Videos: .mp4, .mov, .avi
   - Images: .png, .jpg, .jpeg, .gif
2. Convert unsupported formats before uploading
3. Check file names don't have special characters that might break the system

---

### Common Issue 4: Folder Sharing and Permissions

**Symptom:** Apps Script can't find files, or n8n can't access Google Drive folder.

**Solutions:**
1. Verify the Google Sheet is INSIDE the MyContent folder, not outside it
2. Make sure you're using the same Google account for:
   - Google Drive/Sheets
   - n8n OAuth authorization
3. Check folder permissions if using a shared drive or team account
4. Try moving everything to your personal Google Drive for testing

---

### Common Issue 5: n8n Workflow Doesn't Trigger

**Symptom:** You mark rows "Ready To Post" but nothing happens when you execute workflow.

**Solutions:**
1. Verify the Google Sheets node is pointing to the correct sheet
2. Check the sheet name is exactly: `Social_Media_Publisher_PRO_V2.4`
3. Check the tab names are exactly: `ContentData`, `Settings`, `Metadata`
4. Verify the Status column has exactly "Ready To Post" (not "ready to post" or "Ready to Post")
5. Make sure there are no hidden rows or filters applied in the sheet

---

## Chapter 5: Customizations

### Customizing Content Categories (Folders)

**Adding new content categories:**

1. In Google Drive, create a new subfolder inside `MyContent`
   - Example: `MyContent/Product-Launch`
2. In Google Sheets **Metadata** tab, add a new row:
   - Category Folder Name: `Product-Launch` (must match folder name EXACTLY)
   - Business Context: [Your full audience and positioning description]
   - Default Title: [Your template]
   - Default Caption: [Your template]
3. Upload content to the new folder
4. Run Apps Script "Run Now"
5. No changes needed in n8n - Apps Script automatically detects new folders

**Renaming existing categories:**

If you rename a Google Drive subfolder:
1. Update the **Category Folder Name** in Metadata tab to match new name exactly
2. If you renamed the `MyContent` parent folder:
   - In n8n, reconnect the Google Drive node and point to the new folder path
3. If you renamed the Google Sheet file:
   - In n8n, reconnect the Google Sheets nodes and select the new file name

**Dependencies:**
- Google Drive folder name ↔ Metadata tab Category Folder Name (must match exactly)
- MyContent folder location ↔ n8n Google Drive node configuration
- Google Sheet file name ↔ n8n Google Sheets node configuration

---

### Customizing Default Captions and Titles

**Location:** Google Sheets → Metadata tab

**What you can customize:**
1. **Business Context:** Change audience description, positioning, voice
   - The AI Agent uses this to understand your brand and generate appropriate content
   - Be specific about audience pain points, desires, and language style
2. **Default Title:** Change the template used when new files are discovered
   - Keep it short and descriptive
   - AI Agent will optimize this per platform
3. **Default Caption:** Change the template used when new files are discovered
   - This is your starting point caption
   - AI Agent will adapt it for each platform's style and character limits

**How it works:**
- When Apps Script discovers a new file, it copies the Default Title and Caption into ContentData
- Then AI Agent reads the Business Context and generates platform-specific versions
- You can edit these in ContentData tab before marking "Ready To Post"

---

### Customizing AI Agent Behavior

**Location:** n8n workflow → AI Agent node

**What you can customize:**

1. **System Prompt:** Click the AI Agent node → Options → System Message
   - This tells the AI Agent how to behave
   - Default prompt instructs it to create platform-optimized content
   - You can modify tone, style, rules

2. **Input Data:** The AI Agent receives:
   - Content Category (folder name)
   - Business Context (from Metadata tab)
   - Default Title and Caption
   - You can modify which fields it reads by editing node parameters

3. **Model Selection:** In the AI Agent credential settings
   - Default: gpt-4 (better quality, higher cost)
   - Alternative: gpt-3.5-turbo (faster, cheaper, good quality)

**Warning:** If you change the AI Agent's output structure, you may need to update the nodes that process its output. Only modify the prompt text unless you understand the workflow structure.

---

### Customizing Which Platforms to Use

**Location:** n8n workflow → Blotato posting nodes

**To use fewer than 9 platforms:**

1. In n8n workflow, find the Blotato posting nodes
2. Right-click any platform node you DON'T want to use
3. Select "Deactivate"
4. Deactivated nodes are grayed out and won't execute
5. Save the workflow

**To add a platform back:**
1. First connect that platform in Blotato dashboard
2. In n8n workflow, right-click the deactivated node
3. Select "Activate"
4. Make sure the Blotato credential is set
5. Save the workflow

**Why this matters:** You only pay for Blotato based on your plan, not per platform. But you should only activate platforms you've connected in Blotato to avoid errors.

---

### Adjusting Post Scheduling

**Location:** n8n workflow → Blotato posting nodes

**Default behavior:** Posts are scheduled 7 days in the future for safe testing.

**To change scheduling:**
1. Click any Blotato posting node
2. Scroll down to the bottom to "Scheduled Time" option
3. Options:
   - Post immediately: leave blank
   - Post at specific time: Set date/time value
   - Keep as scheduled: Leave at +7 days
4. Repeat for all active Blotato nodes
5. Save the workflow

`[SCREENSHOT: Blotato node showing Scheduled Time field at bottom]`

**Advanced:** You can add logic to schedule posts based on content category or other factors by adding decision nodes before Blotato nodes.

---

## Congratulations!

You've successfully set up your Social Media Automation System.

**Your workflow:**
1. Create content (videos or images)
2. Upload to appropriate Google Drive category folder
3. Apps Script automatically discovers and populates sheet (runs every X minutes if autotrigger enabled)
4. Review and edit titles/captions in Google Sheets if desired
5. Mark Status as "Ready To Post"
6. n8n workflow automatically processes and posts to all platforms
7. Track what posted where in ContentData tab

**Next steps:**
- Test with your own content (not just the sample files)
- Customize Business Context for your actual brand
- Add more content categories as you grow
- Enable autotrigger in Settings tab for fully automated file discovery
- Set up n8n workflow on a schedule for regular automation

**Support:**
- Review this guide when you encounter issues
- Check the Troubleshooting section
- Refer to Customizations section as you grow

You now have a professional-grade content distribution system.

---

## Glossary of Terms

### n8n Hosting Options

**Cloud n8n (Paid)**
- Hosted by n8n on their servers
- Pros: No maintenance, always updated, accessible from anywhere, reliable uptime
- Cons: Monthly subscription cost, limited control over infrastructure
- Best for: Users who want simplicity and don't mind paying for convenience

**Self-Hosted n8n (Cloud, Paid)**
- You deploy n8n on cloud servers (AWS, DigitalOcean, etc.)
- Pros: More control than managed cloud, no per-execution fees, can customize
- Cons: Requires technical setup, you manage updates and maintenance, server hosting costs
- Best for: Technical users who want control but need internet accessibility

**Local n8n (Free)**
- n8n runs on your own computer
- Pros: No monthly fees, full control, no data leaves your machine
- Cons: Only works when your computer is on, requires local maintenance and updates, not accessible remotely
- Best for: Cost-conscious technical users willing to maintain their own installation
- **Learn more:** [Link to Local n8n Installation Guide - to be provided]

**Which should you choose?**
- Want simplicity? → Cloud n8n (paid)
- Have technical skills and want to save money? → Local n8n (free)
- Need remote access but want control? → Self-hosted cloud (paid)

### Key Terms

**OAuth**
- Authentication method that lets n8n access your Google account without storing your password
- You authorize once through Google's secure login
- Used for Google Drive and Google Sheets connections

**API Key**
- Secret credential that identifies your account to a service
- Like a password, but for applications instead of humans
- Used for Blotato and OpenAI connections

**Apps Script**
- Google's JavaScript platform for automating Google Workspace
- Embedded in your Google Sheet to scan Drive folders
- Runs automatically or manually via "Run Now" button

**Workflow**
- Series of connected automation steps in n8n
- Each step (node) performs one action
- Data flows from one node to the next

**Node**
- Individual step in an n8n workflow
- Examples: Google Sheets node, AI Agent node, Blotato posting node
- Can be activated (runs) or deactivated (skipped)

**Credential**
- Stored authentication information in n8n
- One credential can be reused across multiple nodes
- Keeps your API keys and OAuth tokens secure

**Business Context**
- Description in Metadata tab that tells AI Agent about your audience and brand voice
- Used to generate platform-appropriate captions
- More detailed context = better AI-generated content

**Content Category**
- Google Drive subfolder name that organizes your content
- Must match exactly between Drive folder and Metadata tab
- Used to apply correct Business Context to each piece of content