
# 💌 Build Your Own AI Email Manager with n8n, OpenAI & Slack

*(Simple Guide to Automating Emails, Writing Replies & Sending Slack Alerts)*

---

### ✨ **Introduction**

Are you tired of sorting, replying, and checking every single email manually? Imagine if an AI agent could handle all your emails — label them, write responses, and even send alerts to your Slack — while you relax or focus on real work.

In this guide, you’ll learn how to build such an AI-powered system using:

* **n8n (Open-source automation tool)**
* **OpenAI (to generate responses)**

And the best part? You don’t need to write a single line of code!

---

## 🛠️ **Tools You'll Use**

1. **n8n** – To build the no-code automation flow
2. **OpenAI (Chat Model)** – To classify emails & generate replies
3. **Gmail** – As the mail platform

---

## 🚀 **Step-by-Step Guide**

---

## **1. Setup n8n (Cloud or Self-Hosted)**

* You can run n8n via their **official cloud** or install it **self-hosted** (cheaper option).
* The creator hosted it for \$7/month on **railway.app** instead of \$20 on n8n Cloud.

👉 Once inside n8n Dashboard, create a **New Workflow**.

---

## **2. Add the Gmail Trigger**

* Add a **Gmail node** and choose "**On Message Received**."
* If this is your first time, you’ll need to set up Gmail credentials (n8n docs can guide you).
* Set **polling time** to “Every Minute” to check your inbox for new emails.
* **Test this node** — you’ll see n8n can now detect new emails.

---

## **3. Classify Email Content using OpenAI**

* Add the **Text Classifier node**.

* Set it to use the **email body (snippet)** from Gmail.

* Define your own **email categories/labels**. Example:

  * Consultation Request
  * Billing
  * Customer Support

* You can also add a simple **System Prompt** (for LLM guidance).

* Set up OpenAI API credentials in n8n (you can use OpenAI's API key platform).

* Use **gpt-4o-mini model** (or better, use GPT-4o in production).

👉 **Test this node** — your email should now get classified into one of your 3 labels.

---

## **4. Apply Labels to Gmail Emails**

* After classifying the email, add a **Gmail node** to **“Add Label to Message.”**

* Pass the **Email ID** from the earlier node.

* Select the **correct label** depending on the classification:

  * Consultation Request
  * Billing
  * Customer Support

* You can **duplicate this step** for each label and connect the correct paths.

👉 **Test this node** — emails will be labeled in Gmail properly.

---

## **5. Auto-Draft Replies for “Consultation Requests”**

* If the email is classified as **Consultation**, let AI write a draft reply.

* Add an **OpenAI Chat Model node**:

  * Use the same API key & model (gpt-4o-mini or gpt-4o).
  * Prompt it to write a reply based on the email body.

* Next, add a **Gmail node** to **“Create Draft”**:

  * Pull the AI-generated reply.
  * Add **Thread ID** and **Subject** to make sure the reply matches the right email.

👉 **Test this node** — a draft reply should appear in your Gmail drafts!

--

