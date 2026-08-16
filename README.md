
# HITS Attendance Alert System

> Automated attendance monitoring and SMS alert system for Hindustan Institute of Technology and Science (HITS).

## 📌 Overview

The **HITS Attendance Alert System** monitors student attendance on a subject-wise basis and automatically identifies students whose attendance falls **below 75%**.

When a student is identified as being at risk, the system generates an automated **SMS notification**.

The current prototype uses a **simulated ERP dataset**. The architecture is designed to support HITS ERP integration in a future phase.

---

## 🚨 Notification Channel: WhatsApp → SMS

The project initially planned to use WhatsApp for automated notifications. After evaluating **cost, integration complexity, accessibility, and project constraints**, the team decided to use **SMS**.

### Why SMS?

* Lower and more predictable cost
* No internet connection or WhatsApp account required
* Simple REST API integration
* Suitable for one-way attendance notifications
* Easier to test and maintain
* Better suited for a college project with limited funding

> **Security Note:** SMS is not inherently more secure than WhatsApp. Application-level security will be implemented using HTTPS, API authentication, environment-based secrets, access control, and secure logging.

---

## 🏗️ System Workflow

```text
ERP / Simulated Dataset
          │
          ▼
     MongoDB Atlas
          │
          ▼
 Attendance Calculation
          │
          ▼
   Risk Detection (<75%)
          │
          ▼
   Notification Service
          │
          ▼
      SMS Gateway
          │
          ▼
   Student Mobile
          │
          ▼
     Alert History


---

🛠️ Technology Stack

Component	Technology

Backend	FastAPI
Database	MongoDB Atlas
Database Driver	Motor
Frontend	React + TypeScript + Vite
Scheduler	APScheduler
Authentication	bcrypt
Notification	SMS REST API
API Testing	Postman
Version Control	Git + GitHub



---

📊 Attendance Calculation

Attendance Percentage

Attendance % = (Classes Attended / Classes Conducted) × 100

Alert Condition

if attendance_percentage < 75:
    send_sms()

Important:

75% → No alert

<75% → Alert required


Attendance is calculated independently for each subject.

Classes Required to Reach 75%

X = ceil((0.75 × Classes Conducted - Classes Attended) / 0.25)

This determines the minimum number of consecutive classes a student must attend to reach the 75% threshold.


---

📱 SMS API Research

The following providers were considered:

Provider	India Support	API	Cost Level	Evaluation

MSG91	Strong	REST	Low	Primary Candidate
Fast2SMS	Strong	REST	Low	Alternative
Textlocal	Strong	REST	Low/Medium	Alternative
Twilio	Global	REST	Higher	Reference


Selection Criteria

Cost

API reliability

India support

DLT compliance

Documentation

Delivery reports

Developer experience


> The final provider will be selected after successful end-to-end API testing.




---

🧪 Initial SMS Test

Before connecting attendance logic, the Automation team will verify the SMS mechanism independently.

Python Script
      │
      ▼
   SMS REST API
      │
      ▼
  SMS Gateway
      │
      ▼
  Test Number

Test Message

Hello from HITS Attendance System

Success Criteria

API authentication succeeds

SMS request is triggered programmatically

SMS reaches the test number

Provider response is captured

Message/delivery status can be tracked



---

💰 Cost Optimization

The project follows a free-first development strategy because there is no dedicated project funding.

Free / Open Source

Git

GitHub

FastAPI

React

TypeScript

Vite

MongoDB Atlas Free Tier

APScheduler

Motor

Postman

Mock SMS Provider


Paid

Real SMS credits will be used only for controlled end-to-end testing.

During normal development, a MockSMSProvider should be used to avoid unnecessary SMS costs.


---

🔐 Security

Sensitive credentials must never be committed to GitHub.

MONGODB_URI
JWT_SECRET
SMS_API_KEY
SMS_AUTH_TOKEN
SMS_SENDER_ID

Store credentials using environment variables:

MONGODB_URI=
JWT_SECRET=
SMS_API_KEY=
SMS_SENDER_ID=

Add .env to .gitignore.

Security Measures

HTTPS communication

API authentication

Password hashing

Input validation

Environment-based secrets

Access control

Secure logging

Data minimization


Production SMS deployment must also comply with applicable Indian DLT/SMS regulations.


---

🗂️ Project Structure

HITS-Attendance-Alert-System/
│
├── Backend/
│   └── FastAPI REST API
│
├── Frontend/
│   └── React + TypeScript UI
│
├── Database/
│   └── Dataset and seed data
│
└── Research/
    └── RESEARCH.md


---

👥 Team Responsibilities

Branch	Responsibility

Backend	API, database, attendance calculation
Frontend	React UI, dashboard and UX
Database	Schema and dataset generation
Research	Technical research and feasibility
Automation-Logic	Scheduler and SMS pipeline



---

🚀 Development Roadmap

1. Fake Attendance Dataset
          ↓
2. MongoDB Integration
          ↓
3. Attendance Calculation
          ↓
4. <75% Risk Detection
          ↓
5. SMS API Proof of Concept
          ↓
6. Notification Service Integration
          ↓
7. APScheduler Automation
          ↓
8. End-to-End Testing


---

📌 Current Status

Component	Status

Attendance Logic	✅ Completed
WhatsApp → SMS Decision	✅ Completed
SMS Provider Research	✅ Completed
Dataset Design	✅ Completed
SMS API Testing	⏳ Pending
Final SMS Provider	⏳ Pending
ERP Integration	⏳ Future Phase
Full Automation	🔄 In Progress



---

🎯 Objective

Build a secure, modular, cost-efficient and automated attendance monitoring system that:

Calculate
   ↓
Detect <75%
   ↓
Generate Alert
   ↓
Send SMS
   ↓
Track Delivery

The notification layer will remain provider-independent, allowing the SMS provider to be changed without modifying the core attendance calculation logic.

This is the version I would actually use for the **main project `README.md`**. Keep your larger research document separately as `Research/RESEARCH.md` so the repository stays clean.          
