# FastAPI OTP Authentication via Email

## Project Description

This project is a secure OTP (One-Time Password) Authentication System built using FastAPI, SQLAlchemy, MySQL, and Gmail SMTP.

Users can request a 6-digit OTP using their email address, verify the OTP, resend a new OTP, and gain access to the system. OTPs expire automatically after 5 minutes for enhanced security.

---

# Features

* Generate 6-digit OTP
* Send OTP to real email address
* Verify OTP
* OTP Expiry (5 Minutes)
* Resend OTP
* OTP Status Check
* MySQL Database Integration
* SQLAlchemy ORM
* Gmail SMTP Integration
* Swagger API Documentation
* Postman Collection Testing

### Bonus Features

* OTP History API
* OTP Rate Limiting (3 requests per 10 minutes)

---

# Technology Stack

* Python 3.x
* FastAPI
* SQLAlchemy
* MySQL
* PyMySQL
* Pydantic
* Uvicorn
* python-dotenv
* aiosmtplib

---

# Project Structure

```text
otp_auth_project/
│
├── main.py
├── models.py
├── schemas.py
├── database.py
├── email_service.py
├── requirements.txt
├── README.md
├── .env
├── .env.example
├── otp_auth_db.sql
└── postman_collection.json
```

---

# Database Setup

## Create Database

```sql
CREATE DATABASE otp_auth_db;
USE otp_auth_db;
```

## Users Table

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(255) UNIQUE NOT NULL,
    is_verified BOOLEAN DEFAULT FALSE
);
```

## OTP Verification Table

```sql
CREATE TABLE otp_verifications (
    id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(100) NOT NULL,
    otp_code VARCHAR(6) NOT NULL,
    is_used BOOLEAN DEFAULT FALSE,
    created_at DATETIME,
    expires_at DATETIME
);
```

---

# Installation

## Create Virtual Environment

```bash
python -m venv venv
```

## Activate Environment

Windows:

```bash
venv\Scripts\activate
```

Linux/Mac:

```bash
source venv/bin/activate
```

## Install Dependencies

```bash
pip install fastapi uvicorn sqlalchemy pymysql python-dotenv aiosmtplib email-validator
```

---

# Environment Variables

Create a `.env` file:

```env
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_ADDRESS=your_email@gmail.com
EMAIL_PASSWORD=your_app_password

DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=otp_auth_db
```

---

# Run Project

```bash
uvicorn main:app --reload
```

Server URL:

```text
http://127.0.0.1:8000
```

Swagger Documentation:

```text
http://127.0.0.1:8000/docs
```

---

# API Endpoints

## Send OTP

**POST**

```http
/send-otp
```

Request:

```json
{
  "email": "user@gmail.com"
}
```

Response:

```json
{
  "message": "OTP sent successfully",
  "email": "user@gmail.com",
  "expires_in": "5 minutes"
}
```

---

## Verify OTP

**POST**

```http
/verify-otp
```

Request:

```json
{
  "email": "user@gmail.com",
  "otp": "123456"
}
```

Response:

```json
{
  "message": "OTP verified successfully"
}
```

---

## Resend OTP

**POST**

```http
/resend-otp
```

Request:

```json
{
  "email": "user@gmail.com"
}
```

Response:

```json
{
  "message": "OTP resent successfully",
  "email": "user@gmail.com"
}
```

---

## OTP Status

**GET**

```http
/otp-status/{email}
```

Example:

```http
/otp-status/user@gmail.com
```

Response:

```json
{
  "email": "user@gmail.com",
  "status": "active",
  "remaining_seconds": 240
}
```

---

# OTP Expiry Logic

* OTP is valid for 5 minutes.
* Expired OTPs cannot be verified.
* Used OTPs cannot be reused.
* Resending OTP invalidates previous OTPs.

---

# Email Integration

Email integration is implemented using Gmail SMTP and aiosmtplib.

When a user requests an OTP:

1. A 6-digit OTP is generated.
2. OTP is stored in MySQL.
3. OTP is sent to the user's registered email address.
4. OTP expires automatically after 5 minutes.

Example Email:

```text
Subject: OTP Verification

Your OTP is: 123456

This OTP is valid for 5 minutes.
```

---

# Postman Testing

All APIs were tested successfully using Postman.

Tested APIs:

* POST /send-otp
* POST /verify-otp
* POST /resend-otp
* GET /otp-status/{email}

Postman Collection is included in the project submission.

---

# GitHub Repository

Project Source Code is uploaded to GitHub.

Repository contains:

* Source Code
* SQL Script
* README File
* Postman Collection
* Requirements File

---

# Submission Requirements Completed

* Database Created
* Users Table Created
* OTP Verification Table Created
* OTP APIs Working
* Email Integration Completed
* OTP Expiry Logic Implemented
* Postman Testing Done
* Code Uploaded to GitHub

---

# Future Improvements

* JWT Authentication after OTP Verification
* Redis-based OTP Storage
* OTP Rate Limiting
* OTP History API
* User Registration & Login
* Admin Dashboard

---

# Author

FastAPI OTP Authentication Project
Developed using FastAPI, SQLAlchemy, MySQL, and Gmail SMTP.
