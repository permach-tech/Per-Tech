---
title: "Azure Automation Best Practices"
date: 2025-09-02T19:00:00-05:00
draft: false
tags: ["Azure", "Automation", "IAM", "DevOps"]
categories: ["Cloud Architecture"]
summary: "Lessons learned building automation with Azure Automation Runbooks, Logic Apps, and Microsoft Graph."
---

As a Cloud & IAM Architect, I rely on automation to scale enterprise identity, compliance, and governance.

Here are some of my go-to practices:

## 1. Use PowerShell 7.2 in Runbooks
Older PowerShell versions can cause compatibility issues. I standardize all my Automation Runbooks on **PowerShell 7.2** for long-term support.

## 2. Prefer Managed Identities Over Secrets
Hardcoding secrets is a big risk. Use **System-Assigned Managed Identities** wherever possible. For multi-app scenarios, consider **User-Assigned Managed Identities**.

## 3. Monitor with Log Analytics + KQL
Every runbook logs to Log Analytics. I format errors with timestamps (EST) and store them in KQL-friendly fields for quick troubleshooting.

```kql
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.AUTOMATION"
| where StreamType_s == "Error"
