# RecruitAI — AI-Powered Recruitment & Hiring Platform

**n8n Capstone Project | Summer School'26**

RecruitAI is a modular recruitment automation platform built with **n8n**, **Google Sheets**, **Google Drive**, **Gmail**, and **Google Gemini**. It automates candidate registration, resume collection, AI-based resume analysis, HR communication, and interview scheduling.

## Problem Statement

Growing technology companies receive large numbers of applications through different sources. Manual resume screening and recruitment coordination can cause delays, inconsistent evaluations, duplicate work, and poor candidate communication.

RecruitAI addresses this by connecting recruitment steps into modular n8n workflows and maintaining a centralized candidate record in Google Sheets.

## Objectives

- Automate candidate registration and resume collection.
- Analyze resumes using AI.
- Store structured candidate information in a centralized recruitment sheet.
- Support HR shortlisting/approval communication.
- Automate interview-related notifications.
- Reduce repetitive manual recruitment work.

## System Architecture

```text
Candidate / Google Form
        |
        v
Google Sheets — Candidates
        |
        +----------------------------+
        |                            |
        v                            v
WF-01 Candidate Registration   WF-02 Resume AI Analysis
        |                            |
        |                            +--> Google Drive
        |                            +--> Extract PDF/Text
        |                            +--> Google Gemini AI
        |                            +--> Update candidate record
        |
        v
WF-03 HR Approval & Email Notification
        |
        v
HR decision / candidate communication
        |
        v
WF-04 Interview Scheduling
        |
        v
Interview notification via Gmail
```

## Workflows

### 1. Candidate Registration & Resume Collection

**File:** `workflows/WF-01 Candidate Registration.json`

**5 nodes**

1. Google Sheets Trigger
2. Edit Fields
3. Code in JavaScript
4. Update row in sheet
5. Gmail — Send a message

**Purpose:** Detect a new candidate record, prepare candidate data, generate/update candidate information, and send an automated email.

### 2. Resume Parsing & AI Evaluation

**File:** `workflows/Workflow_2_Resume_AI_Analysis.json`

**8 nodes**

1. Google Sheets Trigger
2. Download file — Google Drive
3. Edit Fields
4. Extract from File
5. Edit Fields1
6. AI Agent
7. Google Gemini Chat Model
8. Update row in sheet

**Purpose:** Retrieve the candidate resume from Google Drive, extract its contents, send the resume information to Gemini through the n8n AI Agent, and write the resulting structured analysis back to the Candidates sheet.

### 3. HR Approval & Email Notification

**File:** `workflows/Workflow 3 – HR Approval & Email Notification.json`

**4 nodes**

1. Google Sheets Trigger
2. If
3. Gmail — Send a message
4. Gmail — Send a message

**Purpose:** Monitor the candidate sheet for the relevant HR decision/status and route the candidate to the appropriate email notification branch.

### 4. Interview Scheduling

**File:** `workflows/Workflow 4 - Interview Scheduling.json`

**3 nodes**

1. Google Sheets Trigger
2. If
3. Gmail — Send a message

**Purpose:** Detect the configured interview condition in the candidate record and send the corresponding interview notification.

## Implementation Summary

| Workflow | Nodes |
|---|---:|
| Candidate Registration | 5 |
| Resume AI Analysis | 8 |
| HR Approval & Email Notification | 4 |
| Interview Scheduling | 3 |
| **Total** | **20** |

The project contains **4 independent n8n workflows and 20 nodes in total**, satisfying the stated implementation minimum of 4–6 workflows and 20–25 nodes.

## Technologies & Integrations

- **n8n** — workflow orchestration
- **Google Sheets** — centralized candidate database and workflow trigger
- **Google Drive** — resume file retrieval
- **Google Gemini** — AI-powered resume analysis
- **Gmail** — automated candidate/HR communication
- **JavaScript** — data transformation and candidate ID/data processing

## AI Component

The resume-analysis workflow uses an **n8n AI Agent connected to Google Gemini Chat Model**. The extracted resume content is passed to the AI model, which returns structured candidate information such as personal details, education, experience, skills, and an AI match score where configured.

The structured result is then mapped back into the Google Sheets candidate record.

## Data Flow

1. A candidate submits application information.
2. The candidate record appears in Google Sheets.
3. Candidate registration workflow processes the new record.
4. The resume-analysis workflow retrieves the uploaded resume.
5. Resume text is extracted.
6. Gemini analyzes the extracted resume.
7. The analysis is written back to the candidate record.
8. HR-related workflow conditions determine the appropriate notification.
9. Interview-related conditions trigger interview communication.

## Repository Structure

```text
RecruitAI/
│
├── README.md
│
├── workflows/
│   ├── WF-01 Candidate Registration.json
│   ├── Workflow_2_Resume_AI_Analysis.json
│   ├── Workflow 3 – HR Approval & Email Notification.json
│   └── Workflow 4 - Interview Scheduling.json
│
├── docs/
│   └── (project documentation / architecture diagram)
│
└── screenshots/
    └── (optional workflow and output screenshots)
```

## How to Import the Workflows

1. Open your n8n instance.
2. Open the target workspace.
3. Use **Import from File**.
4. Select the required `.json` workflow.
5. Reconnect credentials if required.
6. Verify Google Sheets, Google Drive, Gmail, and Gemini credentials.
7. Check spreadsheet/document IDs and field mappings before execution.
8. Execute the workflow with test data.

> Credentials are not intentionally included in this repository. Configure your own credentials in n8n after importing.

## Project Outcome

RecruitAI demonstrates how n8n can be used to build a modular AI-assisted recruitment automation platform. The system reduces repetitive recruitment operations by connecting candidate intake, resume processing, AI analysis, HR communication, and interview notification into a centralized workflow ecosystem.

## Demo

A 5–10 minute demo video will demonstrate:

- Candidate registration
- Resume retrieval and extraction
- AI resume analysis
- Google Sheets update
- HR notification flow
- Interview notification flow

## Capstone Deliverables

- Problem Analysis
- Workflow Architecture
- Four exported n8n workflow JSON files
- Project documentation
- Architecture diagram
- Demo video
- GitHub repository and README
- 10–12 slide presentation
