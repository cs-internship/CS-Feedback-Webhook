# CS Feedback Bot

A feedback collection and management system designed for the CS Internship Program. This bot automates the process of collecting, validating, and distributing feedback about teaching assistants and instructors.

## Overview

CS Feedback Bot is a webhook-based application that:

- Receives feedback submissions from Tally forms
- Validates and encrypts sensitive data
- Stores feedback in a Notion database
- Sends automated Telegram notifications to both feedback senders and receivers

## Features

- **Automated Webhook Processing**: Handles form submissions via Tally webhook integration
- **Secure Data Handling**: Uses encryption/decryption for usernames and sensitive information
- **Notion Database Integration**: Stores all feedback in a structured Notion database
- **Telegram Notifications**: Sends personalized messages to stakeholders
- **Error Handling & Logging**: Admin notifications for system errors and failures
- **Data Validation**: Validates form completeness and data integrity

## Tech Stack

- **Node.js** - JavaScript runtime
- **Express.js** - Web server framework
- **Notion API** - Database storage
- **Telegram Bot API** - Notification delivery
- **Tally** - Form collection platform

## Prerequisites

Before running this project, ensure you have:

- Node.js (v14 or higher)
- npm (Node Package Manager)
- Git
- A Notion account with API access
- A Telegram Bot token
- A Tally account with form setup

## Installation

1. Clone the repository:

```bash
git clone https://github.com/cs-internship/CS-Feedback-Bot.git
cd CS-Feedback-Bot
```

2. Install dependencies:

```bash
cd project
npm install
```

3. Configure environment variables:
   Create a `.env` file in the `project` directory with the following variables:

```
PORT=3000
NOTION_API_KEY_ANS=your_notion_api_key
NOTION_DATABASE_ID_ANS=your_notion_database_id
TELEGRAM_BOT_TOKEN=your_telegram_bot_token
TELEGRAM_ADMIN_ID=your_telegram_admin_id
ENCRYPTION_KEY=your_encryption_key
```

## Usage

1. Start the server:

```bash
npm start
```

The server will run on the specified PORT and expose:

- `GET /` - Health check endpoint
- `POST /webhook/tally` - Webhook endpoint for Tally form submissions

2. Configure Tally webhook:
    - Set your Tally form webhook to point to: `YOUR_SERVER_URL/webhook/tally`
    - You can use [ngrok](https://ngrok.com/) for local development: `ngrok http 3000`

3. Submit feedback through Tally form and watch notifications appear on Telegram!

## Project Structure

```
project/
├── server.js                          # Express server configuration
├── notionService.js                   # Notion database operations
├── utils/
│   ├── telegramService.js            # Telegram bot integration
│   ├── decryptAndValidate.js         # Encryption/decryption utilities
│   ├── parseFormFields.js            # Form data parsing
│   ├── getTelegramIdByUsername.js    # Username to Telegram ID mapping
│   ├── errorReporter.js              # Error notification system
│   ├── questions.js                  # Survey questions configuration
│   └── telegramMessageTemplate/      # Message template builders
│       ├── buildSenderSuccessMessage.js
│       ├── buildSenderErrorMessage.js
│       ├── buildReceiverMessage.js
│       └── buildAdminLogMessage.js
└── package.json                       # Project dependencies
```

## How It Works

1. **Form Submission**: User submits feedback via Tally form
2. **Webhook Reception**: Server receives webhook payload from Tally
3. **Data Processing**: Form fields are parsed and validated
4. **Encryption Check**: Sensitive data is decrypted and validated
5. **Notion Storage**: Feedback is stored in Notion database with structured properties
6. **Notifications**: Telegram messages are sent to sender, receiver, and admin
7. **Error Handling**: Any errors are logged and reported to admin

## Environment Variables

| Variable                 | Description                               |
| ------------------------ | ----------------------------------------- |
| `PORT`                   | Server port number (default: 3000)        |
| `NOTION_API_KEY_ANS`     | Notion API authentication key             |
| `NOTION_DATABASE_ID_ANS` | Notion database ID for feedback storage   |
| `TELEGRAM_BOT_TOKEN`     | Telegram bot token from BotFather         |
| `TELEGRAM_ADMIN_ID`      | Telegram user ID for admin notifications  |
| `ENCRYPTION_KEY`         | Secret key for data encryption/decryption |

## License

This project is licensed under the [MIT License](./LICENSE).

## Contact / Author Info

- **Author:** [Ali Sadeghi](https://github.com/Ali-Sdg90)
- **Developed for:** [CS Internship Program](https://github.com/cs-internship)
