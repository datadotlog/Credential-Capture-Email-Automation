## Secure Screenshot Capture and Email Sender

Automates the process of capturing screenshots from the Windows Credential Manager and sending them via email using DuckyScript and PowerShell.

## Overview

This project provides an automated solution for capturing screenshots from the Windows Credential Manager and securely sending them via email. It combines DuckyScript 3.0 for automation of user actions and PowerShell for handling screenshot captures and email sending. This tool is designed for use in offensive security assessments to demonstrate vulnerabilities in physical access and credential management.

## Key Features

- **Automated Screenshot Capture**: Uses DuckyScript to open the Windows Credential Manager and execute a PowerShell script.
- **Multiple Screenshots**: Captures multiple screenshots of the Credential Manager for thorough documentation.
- **Secure Storage**: Stores screenshots in a zip file encrypted with a specified password.
- **Email Delivery**: Automatically sends the encrypted zip file to a specified email address.
- **Cleanup**: Deletes all temporary files after the email is sent to avoid detection.

## Detailed Workflow

1. **DuckyScript Execution**:
   - Opens the Windows Credential Manager.
   - Executes a PowerShell script to handle the rest of the process.

2. **PowerShell Script Execution**:
   - Creates a directory to store screenshots.
   - Captures multiple screenshots at defined intervals.
   - Compresses and encrypts the screenshots into a zip file.
   - Sends the encrypted zip file via email to a pre-configured address.
   - Cleans up all temporary files and directories to leave no trace.

## Requirements

- A USB Rubber Ducky with DuckyScript 3.0 or a Flipper Zero configured as a BadUSB.
- PowerShell configured on the target Windows machine.
- Valid SMTP server credentials for sending emails.

## Security Considerations

- **Permission**: Ensure you have authorization to perform security assessments on the target machine.
- **Confidentiality**: Handle captured data securely and responsibly.
- **Legality**: Use this tool only for ethical hacking and authorized security testing.
