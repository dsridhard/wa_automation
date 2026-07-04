<h1 align="center">📱 WhatsApp Automated Screenshot Bot</h1>

<p align="center">
  <a href="https://nodejs.org/"><img src="https://img.shields.io/badge/Node.js-14+-green.svg" alt="Node.js version"></a>
  <a href="https://wwebjs.dev/"><img src="https://img.shields.io/badge/whatsapp--web.js-latest-brightgreen.svg" alt="whatsapp-web.js"></a>
  <a href="https://pptr.dev/"><img src="https://img.shields.io/badge/Puppeteer-latest-blue.svg" alt="Puppeteer"></a>
  <a href="https://github.com/node-cron/node-cron"><img src="https://img.shields.io/badge/node--cron-latest-yellow.svg" alt="node-cron"></a>
</p>

A lightweight, highly reliable Node.js bot that connects to WhatsApp Web. It listens for specific trigger phrases from authorized users in a designated group, uses a headless browser to take a screenshot of a target website, and instantly replies with the image. It also features automated daily reporting using cron jobs.

## 🚀 Features
* **Real-time Triggers:** Listens for a specific phrase (e.g., "current booking status") and replies instantly with a fresh screenshot.
* **Scheduled Reporting:** Automatically captures and sends a screenshot to the group at a specific time (e.g., 10:00 AM, Monday-Friday).
* **Strict Authorization:** Only responds to messages sent by pre-approved users (using their specific WhatsApp IDs) within a strictly defined group.
* **Server-Ready:** Configured with Puppeteer stability arguments (`--no-sandbox`) to run smoothly on both Windows machines and headless Linux servers (VPS).
* **Session Persistence:** Saves the WhatsApp authentication state locally so you only have to scan the QR code once.

## 🛠️ Tech Stack
* **[Node.js](https://nodejs.org/)** - Core runtime
* **[whatsapp-web.js](https://wwebjs.dev/)** - WhatsApp API wrapper
* **[Puppeteer](https://pptr.dev/)** - Headless Chrome for capturing website screenshots
* **[node-cron](https://github.com/node-cron/node-cron)** - Task scheduling

## 📋 Prerequisites
* Node.js (v14 or higher) installed on your machine/server.
* A WhatsApp account to act as the "host" for the bot.

## ⚙️ Installation

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/yourusername/wa-automation.git](https://github.com/yourusername/wa-automation.git)
   cd wa-automation
#Install dependencies:
npm install whatsapp-web.js puppeteer node-cron qrcode-terminal
#Configure your variables:
#Open index.js and edit the Configuration section at the top of the file to match your needs:
const TARGET_URL = '[https://www.your-website.com/](https://www.your-website.com/)'; 
const TARGET_GROUP_NAME = 'Your Group Name'; 
const ALLOWED_USERS = [
    '919876543210@c.us', // Standard phone number format
    '108405075247202@lid' // Linked Device ID format
]; 
const TRIGGER_PHRASE = 'current booking status';

First Time Setup:
Run the script locally in your terminal:
node index.js

A QR code will be generated in the terminal. Open WhatsApp on your phone, go to Linked Devices, and scan the QR code. Once authenticated, the terminal will display Client is ready!.

Running in the Background (Recommended):
To keep the bot running 24/7, even if you close the terminal, use PM2:
npm install -g pm2
pm2 start index.js --name "wa-bot"

#🐛 Troubleshooting & Common Issues
The bot ignores messages from authorized users:
WhatsApp's multi-device architecture often assigns users a "Linked Device ID" (@lid) instead of their standard phone number (@c.us). Look at the [DEBUG] logs in your terminal when a user sends a message. Copy the exact Sender ID printed there and add it to your ALLOWED_USERS array.

The terminal says "Client is ready!" but nothing happens (Ghost Connection):
If your session gets corrupted, the bot thinks it is connected but isn't receiving live messages. Stop the bot, delete the hidden .wwebjs_auth folder in the project directory, and restart the bot to scan a fresh QR code.
# Windows
rmdir /s /q .wwebjs_auth

# Linux/Mac
rm -rf .wwebjs_auth
Puppeteer crashes on a Linux server:
Linux servers often lack the graphical libraries required to launch a browser. If you get a Puppeteer error on Linux, install the missing dependencies:
sudo apt-get update
sudo apt-get install -y libx11-xcb1 libxcomposite1 libxcursor1 libxdamage1 libxi-dev libxtst6 cups-libs libnss3 libxrandr2 libasound2 libpangocairo-1.0-0 libatk1.0-0 libatk-bridge2.0-0 libgtk-3-0
📄 License
This project is licensed under the MIT License.