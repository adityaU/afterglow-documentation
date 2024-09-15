# Setting Up Reports & Configurations in Afterglow

In Afterglow, when you download or schedule a report, the system converts the result into a .csv file and uploads it to your AWS S3 bucket (currently, only AWS is supported). After uploading, Afterglow uses your configured email server to send the report to the user's email address. Setting up these configurations ensures seamless report generation and delivery.This involves setting up both an AWS S3 bucket for storing report files and an email server for sending reports to users. Additionally, you can configure download limits and enable experimental GenAI features for query assistance.

## Setting Up Email Server and AWS S3 Bucket

To set up the necessary configurations, follow the steps below.

### Accessing Reports Configuration

#### Navigate to Settings

1. Click on your name on sidebar of the Afterglow interface.
2. Select "Settings" from the dropdown menu.

#### Open Reports Configuration Tab

1. In the Settings page, click on the "Reports Configuration" tab.

### Configuring the Email Server

In the Reports Configuration tab, locate the Email Configuration section. All fields are mandatory.

#### Email Server

- **Hostname or IP Address:** Enter the hostname or IP address of your email server (e.g., `smtp.example.com`).
- **Port:** Specify the port used by your email server (common ports are 25, 465, or 587).
- **Username:** Provide the username for authenticating with your email server.
- **Password:** Enter the password associated with the email server username.
- **Sender ID:** Specify the email address that will appear as the sender of the reports (e.g., `reports@example.com`).
- **Hostname (if different):** Enter the hostname for the email server if different from the Email Server field.

> **Note:** Ensure that your email server permits sending emails from the specified sender ID and that the authentication details are accurate. If using AWS SES in sandbox mode, both the sender and receiver email addresses must be verified. Sandbox mode is intended for testing purposes only. For general use, SES should be moved out of sandbox mode to avoid the need for repeated verification of receiver email addresses.

### Configuring AWS S3 Bucket

Next, configure your AWS settings in the AWS Configuration section.

#### AWS Credentials

- **Access Key ID:** Enter your AWS Access Key ID with permissions to upload files to the S3 bucket.
- **Secret Access Key:** Provide the corresponding AWS Secret Access Key.
- **Region:** Specify the AWS region where your S3 bucket is located (e.g., `us-west-2`).

#### S3 Bucket Settings

- **Bucket Name:** Enter the name of the S3 bucket where reports will be stored.
- **Private Bucket:** Toggle this option ON if you want the S3 bucket to be private.

```admonish note
  If enabled, you must update your S3 bucket policy to allow Afterglow to access it.
```

- **Signed S3 URL Timeout (in sec):** Set the duration (in seconds) for which the download link to the report will remain valid. Example: Setting it to 3600 makes the link valid for one hour.

```admonish important
Ensure that the AWS credentials provided have the necessary permissions to upload files to the S3 bucket and that the bucket policies are correctly configured, especially if using a private bucket.
```

---

## Managing Download Limits for Reports

Afterglow allows you to control the download capabilities and data limits for reports.

- **Can Download Reports:** Found in the Reports Configuration tab. Toggle this option to ON or OFF to enable or disable report downloads for this Afterglow installation.
  > **Note:** This setting can be overridden at the Organization and User levels.
- **Maximum Number of Rows in Exports/Reports:** Also in the Reports Configuration tab. Set a limit on the number of rows that can be included in a report. Leave this field empty for no limit.
  > **Note:** This setting can also be overridden at the Organization and User levels.
- **Maximum Number of Rows on Frontend:** Navigate to the Frontend Configuration tab. Set the maximum number of rows that can be displayed on the frontend.
  > **Note:** The system does not allow more than 2,000 rows to optimize performance.

---

## Enabling GenAI Configuration (Experimental)

Afterglow offers an experimental GenAI feature to assist with query writing using natural language processing.

```admonish caution
This feature sends your schema details to the GenAI provider. Use it as a template to generate base queries and modify them as needed.
```

- **Select GenAI Provider:** Choose from the supported providers:

  - **OpenAI**
  - **Claude**
  - **Local models via Ollama**

- **Provider API Key:** Enter the API key for the selected GenAI provider.

- **Provider Model Name:** Specify the model name you wish to use (e.g., `gpt-4o` for OpenAI).
- **API URL**: Enter the API endpoint URL for the GenAI provider. Leave default if using the standard endpoint.
- **Users can override GenAI Settings:** Toggle this option ON if you want users to be able to override the OpenAI key at the query level.
  > **Note:** Users can override the GenAI Settings Toggle can be enabled at the Organization level.
