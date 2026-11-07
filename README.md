# Crowdtangle Email ETL | Pentaho Data Integration

## About the Project

This project automates the extraction and loading of data files received through Crowdtangle email notifications.

Using **Pentaho Data Integration (PDI)**, the workflow reads emails from a dedicated IMAP folder, identifies the relevant message, extracts the download URL from the email body, downloads the Excel file and loads its data into a database.

The main goal is to reduce manual tasks and demonstrate an automated ETL process using email integration, file downloading and database loading.

## Project Features

- **Email Integration:** Reads incoming emails using the IMAP protocol.
- **Email Filtering:** Filters messages based on their sending date.
- **Content Extraction:** Processes the email body to extract the Excel file download URL.
- **Automated Download:** Uses an HTTP job entry to download the file.
- **Database Loading:** Executes a Pentaho transformation to load the downloaded data into a DBMS.
- **Execution Notifications:** Sends email notifications for successful or failed executions.

## Technologies

| Technology | Purpose |
|---|---|
| Pentaho Data Integration (PDI) | ETL development and orchestration |
| Pentaho Job (.kjb) | Workflow execution and process control |
| Pentaho Transformation (.ktr) | Data extraction, processing and loading |
| IMAP | Email retrieval |
| HTTP | File downloading |
| SQL / DBMS | Data persistence |
| Excel | Source data format |

## ETL Architecture

The solution is organized into an orchestration job and dedicated transformations.

```text
             Crowdtangle Email
                     |
                     v
              IMAP Connection
                     |
                     v
             Read Email Messages
                     |
                     v
              Filter Messages
                     |
                     v
          Extract Excel Download URL
                     |
                     v
              HTTP File Download
                     |
                     v
             Excel Data Extraction
                     |
                     v
               Database Loading
                     |
                     v
             Execution Notification
```

## Workflow Description

### 1. Email Extraction

The `ler_email.ktr` transformation connects to an email server using IMAP and reads messages from a dedicated folder.

The process retrieves relevant email information, including:

- Email subject.
- Sender.
- Message body.
- Sent date.

### 2. Email Filtering and URL Extraction

The workflow filters messages according to the sending date and processes the email body to identify the Excel download link.

The extracted URL is passed to the next step of the process.

### 3. File Download

The main Pentaho job uses an HTTP entry to download the Excel file using the extracted URL.

### 4. Database Loading

The `input_database.ktr` transformation is responsible for processing the downloaded file and persisting its data into the target database.

### 5. Execution Notifications

The job includes notification steps for successful and failed executions, helping monitor the ETL process.

## Project Structure

```text
ETL_PDI_crowdtangle/
│
├── JOB.kjb
├── ler_email.ktr
├── input_database.ktr
└── README.md
```

| File | Description |
|---|---|
| `JOB.kjb` | Main job responsible for orchestrating the ETL workflow. |
| `ler_email.ktr` | Reads and processes Crowdtangle email messages and extracts the download URL. |
| `input_database.ktr` | Processes the downloaded file and loads data into the database. |

## Configuration Requirements

Before executing the workflow, configure the connections and variables required by the Pentaho transformations and job.

The environment requires:

- A valid IMAP server and email account.
- Access to the email folder used for Crowdtangle notifications.
- A valid HTTP download URL.
- A configured database connection.
- A valid SMTP server for execution notifications.

Connection details, credentials, server addresses and other environment-specific settings should be configured locally rather than stored in public repository files.

## How to Run the Project

1. Install and configure Pentaho Data Integration (Spoon).
2. Clone or download this repository.
3. Open `JOB.kjb` in Pentaho Spoon.
4. Review and configure the email, HTTP, database and SMTP connections.
5. Open the referenced transformations and validate their configuration.
6. Execute the main job.

> The original workflow contains environment-specific configuration. It requires connection updates before it can run in another environment.

## Key Concepts Demonstrated

- ETL process automation.
- Pentaho job orchestration.
- Pentaho transformations.
- IMAP email integration.
- Email content processing.
- HTTP file downloading.
- Excel data extraction.
- Database loading.
- Execution notifications.

## Project Objective

This project demonstrates how Pentaho Data Integration can be used to automate an end-to-end data ingestion process, integrating email services, file downloads and database persistence.

It highlights practical experience with ETL development, workflow orchestration and data integration.

---

**Author:** [Deyvid Linoba](https://github.com/dlinoba)
