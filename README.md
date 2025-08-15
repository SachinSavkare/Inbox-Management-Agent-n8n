# 📬 Inbox Management Agent

Automate your email management with an **Inbox Management Agent** built on **n8n**. This agent categorizes emails, drafts responses, summarizes content, and notifies you via Telegram — making your inbox smarter, faster, and more organized.

---

## 🚀 Project Overview

- **Purpose**: Automatically classify emails, summarize content, draft replies, and send notifications.  
- **Main Tools**: n8n (workflow automation), Gmail, Telegram, AI agents (OpenAI GPT-4o).  
- **Outcome**:  
  - ⚡ High-priority emails get immediate attention.  
  - 💬 Customer support emails are replied to automatically.  
  - 🎁 Promotional emails are summarized with recommendations.  
  - 💰 Finance/Billing emails are forwarded and summarized.  

- **Beginners Guide**: [Click here to access the step-by-step guide](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Beginners%20Guide%20_Inbox%20Management%20Agent.pdf)

---

## 📂 Categories & Sample Emails

### ⚡ 1) High Priority Emails
**Description**: Emails requiring immediate attention. Drafts are created automatically for quick action.

> **Sample Email**  
> **Subject**: Urgent Approval Needed: Q3 Marketing Plan  
> **Body**:  
> Hi Team,  
> Please review and approve the Q3 marketing plan immediately. The client is awaiting confirmation by 3 PM today.  
> Best regards,  
> Alice - Marketing Lead  

**Workflow Steps**:

![High Priority Emails](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/High%20Priority.JPG)

1. 📧 **Gmail Node: Add Label** – Label emails as "High Priority".  
2. 🤖 **AI Agent Node: Creating Draft**  
   - **Prompt**:  
     ```
     You are an executive assistant. Respond to incoming high priority emails accurately.
     Email: {{ $('Gmail Trigger').item.json.text }}
     
     Output:
     - Subject
     - Message
     - From (extract signer)
     - Telegram text: HIGH PRIORITY EMAIL from {{ From }}. Draft created with subject {{ Subject }}
     ```
3. 📧 **Gmail Node: Create Draft** – Uses AI-generated subject and message.

![Create Draft](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Mail%20high%20Priority.JPG)

4. 💬 **Telegram Node: Notification** – Sends: `HIGH PRIORITY EMAIL from {{ From }}. Draft created with subject {{ Subject }}`

![Telegram Output](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Telegram%20High%20Priority.JPG)

---

### 🛠️ 2) Customer Support Emails
**Description**: Customer queries that need prompt responses. AI drafts replies or forwards to support team if unable to handle.

> **Sample Email**  
> **Subject**: Login Issue with Dashboard  
> **Body**:  
> Hello Support Team,  
> I cannot log into my account. Resetting password didn’t work. Please assist me as soon as possible.  
> Regards,  
> Bob - Client  

**Workflow Steps**:

![Customer Support Emails](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Customer%20Support.JPG)

1. 📧 **Gmail Node: Add Label** – Label emails as "Customer Support".  
2. 🤖 **AI Agent Node: Creating Email**  
   - **Prompt**:  
     ```
     You are a customer service representative. Respond to incoming customer support emails accurately.
     If unable to handle, refer to customersupport@abccorp.com.
     
     Email: {{ $('Gmail Trigger').item.json.text }}
     Sign off as: Codebasics Support Team
     
     Output:
     - Subject
     - Message
     - From
     - Telegram text: Responded to customer support inquiry from {{ From }}
     ```
3. 📧 **Gmail Node: Auto Reply** – Sends AI-generated response.

![Auto Reply](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Mail%20Customer%20Support.JPG)
  
4. 💬 **Telegram Node: Confirmation** – Sends: `Responded to customer support inquiry from {{ From }}`  

![Telegram Output](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Telegram%20Customer%20Support.JPG)

---

### 🎁 3) Promotional Emails
**Description**: Marketing or promotional emails. AI provides summaries and recommendations for stakeholders.

> **Sample Email**  
> **Subject**: Exclusive AI Automation Offer  
> **Body**:  
> Hi there,  
> Enjoy a 20% discount on our AI automation services this month! Boost your productivity with our latest tools.  
> Cheers,  
> Clara - AI Solutions Team  

**Workflow Steps**:

![Promotion](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Promotion.JPG)

1. 📧 **Gmail Node: Add Label** – Label emails as "Promotions".  
2. 🤖 **AI Agent Node: Summary and Recommendation**  
   - **Prompt**:  
     ```
     You are in charge of promotions. Evaluate incoming promotional emails.
     
     Email: {{ $('Gmail Trigger').item.json.text }}
     
     Output:
     - Summary
     - Recommendation
     - From
     - Telegram text: Promotion from {{ From }} summarized. Recommendation: {{ Recommendation }}
     ```
3. 💬 **Telegram Node** – Sends: `Promotion from {{ From }} summarized. Recommendation: {{ Recommendation }}`  

![Telegram Output](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Telegram%20Promotion.JPG)

---

### 💰 4) Finance/Billing Emails
**Description**: Finance or billing related emails. AI summarizes content and forwards to finance department.

> **Sample Email**  
> **Subject**: Invoice #56789 Due Reminder  
> **Body**:  
> Hello,  
> This is a reminder that your invoice #56789 for INR 4500 is due by September 5th. Please process payment to avoid late fees.  
> Thanks,  
> Emma - Accounts Department  

**Workflow Steps**:

![Telegram Output](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Finance_Billing.JPG)

1. 📧 **Gmail Node: Add Label** – Label emails as "Finance/Billing".  
2. 🤖 **AI Agent Node: Summary from Finance Dept.**  
   - **Prompt**:  
     ```
     You are a finance/billing assistant. Summarize incoming emails concisely.
     
     Email: {{ $('Gmail Trigger').item.json.text }}
     
     Output:
     - Subject
     - Message
     - From
     - Telegram text: Finance/Billing inquiry from {{ From }}. Notified finance department.
     ```
3. 📧 **Gmail Node: Forward Email** – Forwards to finance team.

![Forward Email](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Mail%20Finace.jpg)
   
4. 💬 **Telegram Node: Notification** – Sends: `Finance/Billing inquiry from {{ From }}. Notified finance department.`  

> **Workflow Image Placeholder**  
> *(Upload workflow diagram here)*  

---

## 🏷️ Gmail Label Image
**Description**: Example of how incoming emails are labeled in Gmail for categorization.  

![Gmail Label Image](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Gmail%20Inbox.png)

---

## 🔧 Workflow Description
The agent uses **n8n workflows** to process incoming emails: triggers Gmail, classifies messages, calls AI agents for drafting, summaries, or auto replies, and finally sends Telegram notifications. Each category workflow is designed for **modular improvements** and can integrate with CRM or other tools in the future.  

![Workflow](https://github.com/SachinSavkare/Inbox-Management-Agent-n8n/blob/main/Workflow.png)

---


