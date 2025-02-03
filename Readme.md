# RansomWatch

RansomWatch is an automated breach notification system that monitors a trusted threat intelligence JSON feed for lottery-related security breaches. Running on a Raspberry Pi (or any Linux-based system), it securely sends email alerts using Google Apps App Passwords whenever a new incident is detected.

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

1. **Create a .env File:**

   In your home directory (or adjust the path in the script accordingly), create a .env file with the following:

```dotenv
EMAIL_SENDER=your-email@example.com
EMAIL_PASSWORD=your-google-app-password
EMAIL_RECEIVER=receiver-email@example.com
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
```

   
2. **Verify Environment Variables:**

   The script checks for these variables at startup and will exit if any required variable is misconfigured.
---
  
## Usage 
Run the breach notification tool with: 
```bash python breach_notifier.py ``` 
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
The tool maintains a `sent_breaches.json` file to track notifications. Delete or modify this file if you need to reset the notification history. --- 
## License
This project is licensed under the MIT License. See the (LICENSE) file for more details. 
   
