# Setting Up reports & Configurations

You will need to setup reports configuration so that you are able to download reports and receive them on your email

## Reports Configuration

Whenever you try to download or schedule a report, Afterglow first converts the result into a .csv file and upload to your AWS S3 bucket (Only AWS supported for now). After that, Afterglow uses your email server to send the report to the user’s email. We will setup both AWS S3 bucket & Email server in order for you to download reports seamlessly.

### Setting up Email Server & S3 bucket

Go to Settings (“Your Name” on Top Right -> Settings) page and click on Reports Configuration tab

### Add your Email Configuration (All Mandatory fields)

- Email Server
- Email Server Port
- Email Server Username
- Email Server Password
- Email Sender ID: This is the email which will appear as sender
- Email Server Hostname

#### Add your AWS Configuration

- AWS ACCESS KEY ID
- AWS SECRET ACCESS KEY
- AWS REGION
- S3 Bucket
- Use Private Bucket: Enable this if you want to keep the S3 bucket private. You’ll have to update your s3 bucket policy yourself
- Signed S3 Url Timeout (in sec): This is the duration for which your file is available to download

### Download Limits for Reports

You can also set the following details regarding data limit for reports:

- **Can download reports:** This is found in `Reports Configuration Tab`. You can turn this off to disable downloads for this Afterglow installation. This can however, be overridden on Organization and User level
- **Maximum number of Rows in Exports/Reports:** This is found in `Reports Configuration Tab`. Leave it empty for no limit. This can however, be overridden on Organization and User level.
- **Maximum Number of Rows on frontend:** Go to `Frontend Configuration Tab`. It can be less than 2000 as system doesn’t allow for anything more than 2000 internally to optimise performance

### GenAI Configuration (Experimental)

You can also supercharge your query writing by using Gen AI. We send your schema details to GenAI in order to create a query using natural language. Since, queries depend a lot on internal context and your schema design, this is recommended more as a template to get a base query and then modify it accordingly.

- Add the following configuration for GenAI:
  - Select GenAI Provider. Currently Afterglow Supports OpenAI, Claude & local models via Ollama
  - Provider API Key
  - Provider Model Name
