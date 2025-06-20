# Supplier Details Automation

A UiPath Studio automation process that streamlines supplier management by processing vendor requests through email integration and web data extraction.

## Overview
This automation solution processes supplier details by:

1. Extracting emails with vendor requests from Gmail
2. Downloading Excel attachments containing vendor requirements
3. Fetching supplier data from a web portal (rpasamples.com)
4. Matching vendors with suitable suppliers based on location, industry, and employee count criteria
5. Updating Excel files with matched supplier details
6. Sending automated email responses with updated information

## Project Structure

```
SupplierDetailsAutomation/

├── Main.xaml                    # Main workflow file
├── project.json                 # Project configuration
├── Data/                        # Data storage folder
│   ├── SuppliersDetailsUpdated.xlsx
│   └── UiPath_Demo_Suppliers_Export_*.csv
├── .screenshots/                # UI element screenshots
└── README.md                    # This file
```

## Workflow Components

### 1. Email Processing
- **Activity**: GetEmailListConnections
- **Function**: Retrieves emails with subject "Supply Management" from Gmail Inbox
- **Output**: List of Gmail messages for processing

### 2. Attachment Download
- **Activity**: ForEach loop through email messages
- **Function**: Downloads Excel attachments named "GetSuppliersDetails.xlsx"
- **Storage**: Saves files to Data/ folder

### 3. Web Data Extraction
- **Target**: rpasamples.com Supplier Management System
- **Action**: Clicks "Export CSV" to download supplier database
- **Output**: CSV file with supplier information

### 4. Data Processing
- **Excel Reading**: Reads vendor requirements from "VendorRequest" sheet
- **CSV Processing**: Loads supplier data from exported CSV
- **Column Addition**: Adds "Supplier Details" column if not present

### 5. Supplier Matching Algorithm
For each vendor request, the system:

1. Extracts vendor criteria:
   - Industry type
   - Address (Street, City, State)
   - Minimum employee count
2. Filters supplier database by:
   - Exact industry match
   - Exact address components match (Street, City, State)
   - Employee count >= minimum requirement
3. Builds supplier list:
   - Collects unique "Internal Name" values
   - Prevents duplicate entries
   - Assigns "NA" if no matches found
4. Updates vendor record:
   - Populates "Supplier Details" column with comma-separated supplier names

### 6. File Management
- **Excel Update**: Writes updated data back to original Excel file
- **File Rename**: Renames to "SuppliersDetailsUpdated.xlsx"
- **Cleanup**: Removes existing updated files to prevent conflicts

### 7. Email Response
- **Activity**: ReplyToEmailConnections
- **Function**: Sends automated reply with updated Excel attachment
- **Content**: Professional message indicating supplier details completion

## Technical Requirements

### Dependencies
- UiPath.Excel.Activities: [3.1.0-preview] - Excel file operations
- UiPath.GSuite.Activities: [3.2.0-preview] - Gmail integration
- UiPath.Mail.Activities: [2.2.0-preview] - Email processing
- UiPath.System.Activities: [25.4.4] - Core system activities
- UiPath.UIAutomation.Activities: [25.10.4] - Web automation

### System Requirements
- UiPath Studio: Version 25.0.167.0 or higher
- Target Framework: Windows
- Expression Language: Visual Basic
- Gmail Account: Configured with appropriate permissions
- Internet Access: Required for web data extraction

## Configuration

### Gmail Setup
1. Configure Gmail connection in UiPath
2. Ensure access to target mailbox
3. Verify "Supply Management" subject filter

### Web Portal Access
1. Ensure access to rpasamples.com
2. Verify Supplier Management System availability
3. Test CSV export functionality

## Data Flow
Gmail Inbox → Email Extraction → Attachment Download → Web Data Fetch → Data Matching → Excel Update → Email Response

## Key Features
- Automated Email Processing: Handles multiple vendor requests simultaneously
- Intelligent Matching: Multi-criteria supplier filtering (location, industry, size)
- Data Validation: Prevents duplicate supplier assignments
- Error Handling: Graceful handling of missing matches ("NA" assignment)
- File Management: Automatic backup and versioning of Excel files
- Professional Communication: Automated response emails with attachments

## Usage
1. Prepare Email: Send vendor request with Excel attachment to monitored Gmail account
2. Run Automation: Execute Main.xaml workflow
3. Monitor Progress: Check UiPath logs for processing status
4. Receive Results: Updated Excel file delivered via email reply

## Logging and Debugging
The workflow includes comprehensive logging:
- Email extraction counts
- Data processing progress
- Supplier matching results
- File operation confirmations
- Error notifications

## Maintenance
- Regular Updates: Keep UiPath packages current
- Data Refresh: Ensure supplier database stays updated
- Connection Monitoring: Verify Gmail and web portal connectivity
- Performance Optimization: Monitor processing times for large datasets

## Project Information
- Project ID: 50df4959-da6e-444b-8fd4-b7854e7fb221
- Version: 1.0.0
- Description: Assessment 3 - Supplier Details Automation - Email - Excel
- Entry Point: Main.xaml

This automation streamlines the supplier management process, reducing manual effort and ensuring consistent, accurate vendor-supplier matching based on business criteria.