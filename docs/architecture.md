# Project Architecture

The Telegram Downloader Bot is organized into separate components, with each component responsible for a specific part of the application.

## General Flow

```text
Telegram User  
      ↓  
Telegram Handlers  
      ↓  
Request / Business Logic  
      ↓  
┌──────────────┬──────────────┬──────────────┐
│ Video        │ Image        │ Audio        │
│ Downloader   │ Downloader   │ Processing   │
└──────────────┴──────────────┴──────────────┘
      ↓  
Media Processing  
      ↓  
Telegram
```

## Main Components

### Handlers

Receive Telegram updates and handle user commands, messages, buttons, and payments.

### Downloaders

Responsible for downloading supported media from platforms such as YouTube, Instagram,TikTok and other platform or websites.

### Services

Contains application-level logic such as request management, progress tracking, rate limiting, and cleanup.

### Processors

Handles media operations such as audio extraction and video processing.

### Recognition

Provides music and voice recognition functionality.

### Database

Stores users, downloads, payments, Premium information, and application statistics using SQLite.

### Keyboard

Contains Telegram inline keyboards used for quality selection, Premium plans, administration, and other interactions.

## Premium System

The Premium system provides additional functionality and higher limits.

Premium subscriptions are processed through Telegram Stars.

```text
User
 ↓
Premium Plan
 ↓
Telegram Stars Payment
 ↓
Payment Handler
 ↓
Database
 ↓
Premium Activated
```

## Request Processing

Each download request is handled independently and assigned a unique request identifier.

This allows the bot to safely process multiple requests and keep temporary files and request data separated.

## Concurrency and Rate Limiting

The bot uses concurrency controls and per-user rate limiting to prevent excessive simultaneous downloads and reduce resource usage.

## Error Handling

Errors during downloading, processing, or Telegram operations are caught and handled so that users receive an appropriate status instead of the application crashing.

## Technology Stack

* Python
* python-telegram-bot
* yt-dlp
* FFmpeg
* Telethon
* SQLite
* OpenAI Whisper
* httpx
