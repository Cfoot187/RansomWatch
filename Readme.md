# RansomWatch

RansomWatch is an automated breach notification system that monitors a trusted threat intelligence JSON feed for security breaches. While the below configuration is setup to monitor breaches related to lottery, the script can be tailored to anything. Running on a Raspberry Pi (or any Linux-based system), it securely sends email alerts using Google Apps App Passwords whenever a new incident is detected.

This project not only helps in proactive monitoring but also served as a valuable learning experience in secure email practices, Python scripting, and automation.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Scheduling](#scheduling)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

RansomWatch continuously polls a public JSON feed (sourced from [RansomWatch on GitHub](https://github.com/joshhighet/ransomwatch)) for new posts related to lottery breaches. By filtering the feed using keywords like "lotto" and "lottery", the tool ensures that only relevant security incidents trigger an email alert.

Key aspects include:
- **Continuous Monitoring:** The script performs an initial check upon startup and then continues to run, checking for new breaches at scheduled intervals.
- **Duplicate Prevention:** A local record (`sent_breaches.json`) is maintained to prevent redundant notifications.

---

## Features

- **Automated Monitoring:** Periodically checks a remote JSON feed for security breaches.
- **Keyword Filtering:** Uses specified lottery-related keywords to identify relevant incidents.
- **Secure Email Notifications:** Sends alerts securely via SMTP using Google Apps App Passwords.
- **Environment-Based Configuration:** Manages sensitive credentials through a `.env` file.
- **Duplicate Notification Prevention:** Keeps track of already notified breaches to avoid repeated emails.

---

## Requirements

- **Python 3.6+**
- **Hardware:** Raspberry Pi (or any Linux-based system)
- **Python Libraries:**
  - `requests`
  - `schedule`
  - `python-dotenv`
  - Standard libraries: `os`, `time`, `json`, `smtplib`, `email`

---

## Installation

1. **Clone the Repository:**

   git clone https://github.com/Cfoot187/RansomWatch.git
   cd RansomWatch


---

2. **Set Up a Virtual Environment (Optional but Recommended):**

    python3 -m venv venv
    source venv/bin/activate

---

## Configuration

**Google Apps App Password Setup**

To securely send email notifications via your Google account, you must generate an App Password. **Important:** Your Google account must have 2-Step Verification enabled to generate an App Password.

*Steps to Enable 2-Step Verification and Generate an App Password:*

1. **Enable 2-Step Verification:**
   - Sign in to your Google Account.
   - Navigate to **Security**.
   - Under "Signing in to Google," locate **2-Step Verification** and click on it.
   - Follow the on-screen instructions to enable 2-Step Verification if it isn’t already enabled.

2. **Generate an App Password:**
   - Once 2-Step Verification is enabled, go back to the **Security** section.
   - Click on **App passwords** (this option will appear only after enabling 2-Step Verification).
   - You may be prompted to sign in again.
   - In the App Passwords section, select the app and device for which you want to generate the password. For             example, choose "Mail" as the app and "Other (Custom name)" as the device (you might name it "RansomWatch").
   - Click **Generate**.
   - Copy the 16-character password that is displayed.

3. **Configure Your Application:**
   - Update your `.env` file with the generated App Password. For example:
     ```dotenv
     EMAIL_SENDER=your-email@example.com
     EMAIL_PASSWORD=your-generated-app-password
     EMAIL_RECEIVER=receiver-email@example.com
     SMTP_SERVER=smtp.gmail.com
     SMTP_PORT=587
     ```

By following these steps, you'll ensure that your application can securely send email notifications using your Google account credentials.

---
  
## Usage 
Run the breach notification tool with: 
```python breach_notifier.py ``` 
On startup, the script immediately checks for breaches and then continues to run, checking for new incidents every hour. --- 
## Scheduling 
The tool leverages the `schedule` library to check for breaches on an hourly basis:
```python schedule.every().hour.do(check_and_notify) ``` 
The script then enters an infinite loop, running pending scheduled jobs every minute. Adjust the schedule as needed for your environment. --- 
## Troubleshooting 
### Missing Environment Variables 
Ensure that your `.env` file exists in the expected location and includes all the necessary variables. 
### SMTP Connection Issues 
Confirm that your SMTP settings are correct and that your Google account has App Passwords enabled. Check your credentials if you encounter errors. 
### JSON Feed Errors
Verify that the JSON feed URL (`https://raw.githubusercontent.com/joshhighet/ransomwatch/main/posts.json`) is accessible and that your network connection is stable. 
### Duplicate Notifications
The tool maintains a `sent_breaches.json` file to track notifications. Delete or modify this file if you need to reset the notification history.
## License
This project is licensed under the MIT License. See the (LICENSE) file for more details. 
   
