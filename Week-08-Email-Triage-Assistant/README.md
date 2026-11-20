# Customer Email Triage and Reply Assistant

**FlyRank AI Internship Week 8, Assignment 8.1 (FL-09)**  
**Author:** Genevieve Jacob  
**Version:** 2  
**Platform:** Claude Projects  
**Project type:** Prompt-based AI-assisted customer-service workflow

## 1. Project overview

The Customer Email Triage and Reply Assistant is a prompt-based workflow configured in a Claude Project. It helps a customer-service representative classify incoming email enquiries, identify cases that need urgent human attention, and prepare first-draft replies for routine enquiries.

The intended users are customer-service representatives and small businesses that handle recurring customer enquiries. The goal is to reduce repetitive drafting work while maintaining accuracy, empathy and customer trust.

The assistant classifies emails into five categories:

- Order Tracking
- Product Question
- Complaint
- Refund Request
- General Inquiry

For standard enquiries, it prepares a concise draft in a warm, reassuring and clear voice. For urgent or sensitive enquiries, it flags the case for human review and does not produce a customer-facing draft.

**Core principle:** AI assists with classification and first drafts. A human verifies the facts, makes decisions, edits and approves every response before it is sent.

## 2. Problem and intended outcome

Customer-service teams regularly receive repeated questions about orders, products, complaints, refunds and general company information. Preparing every response from scratch can be repetitive. However, using AI without clear safeguards can create additional risks, including invented business policies, unverified delivery promises, unsafe product claims or responses that overlook a customer's frustration.

This workflow is designed to:

1. Organise incoming enquiries into a consistent set of categories.
2. Identify sensitive or emotionally difficult cases that need human judgment.
3. Prepare useful first drafts for routine enquiries.
4. Avoid filling gaps with invented company facts or commitments.
5. Keep internal review reminders separate from text intended for customers.

## 3. How it works

```mermaid
flowchart TD
    A[Genevieve pastes a customer email] --> B[Claude Project applies saved Version 2 instructions]
    B --> C[Classify email and assess urgency]
    C --> D{Urgent or sensitive?}
    D -- Yes --> E[Return category, urgent status and reason; no reply draft]
    D -- No --> F[Prepare customer-facing draft]
    F --> G[Add separate Genevieve's Review Notes when needed]
    E --> H[Genevieve reviews and decides next steps]
    G --> H
    H --> I[Verify facts and policies; edit and approve]
    I --> J[Send manually through an authorised channel, if approved]
```

The workflow is manually operated. The user copies an email into a Claude Project conversation. Claude applies the Project Instructions and returns a classification and either an escalation notice or a draft. Genevieve reviews the result and, where appropriate, checks verified company information before deciding what to do. Sending occurs outside the workflow.

## 4. Categories and escalation rules

| Category | Meaning |
|---|---|
| Order Tracking | An enquiry about an order update, delayed delivery or missing package. |
| Product Question | A question about product ingredients, features, use or suitability. |
| Complaint | Dissatisfaction with a product or service when a refund request is not the main purpose. |
| Refund Request | An explicit request for a refund or information about obtaining one. |
| General Inquiry | An enquiry that does not fit the other four categories. |

An explicit refund request is classified as **Refund Request**, even when the email also describes a complaint. The category and urgency are assessed separately.

The workflow flags an email **URGENT â€” HUMAN REVIEW REQUIRED** when the supplied email or thread indicates, for example:

- A clearly angry, distressed or highly upset customer.
- Repeated contact about an unresolved problem.
- A possible adverse reaction, allergy, medication or other health/safety concern.
- A legal, regulatory, privacy or security concern.

For urgent cases, the assistant returns the category, urgent status and a brief reason. It does not draft a customer-facing reply. Repeat contact is not assumed unless the supplied thread or information supports it.

## 5. Tools and roles

| Tool or person | Role |
|---|---|
| Claude Projects | Stores the standing Project Instructions and provides the conversation interface. |
| Claude AI | Applies the instructions to classify emails, assess urgency and prepare first drafts. |
| Genevieve | Defines the requirements, reviews outputs, checks facts and policies, and approves or rejects drafts. |
| ChatGPT | Assisted with reviewing test outputs, identifying gaps and preparing the project documentation and demo plan. |

No custom application code, live inbox connection, order-system integration or automatic email sending is included in this version.

## 6. Setup: reproduce the Project

A person with access to Claude Projects can recreate the workflow as follows.

### Requirements

- An internet connection.
- A Claude account with access to Projects.
- The complete Project Instructions in [Section 10](#10-project-instructions-to-copy).

### Steps

1. Sign in at [claude.ai](https://claude.ai).
2. Open **Projects** from the sidebar and create a new Project.
3. Give it a name such as **Customer Email Triage and Reply Assistant** or **Inbox Triager**.
4. Open the Project's **Project Instructions** setting (the label may appear as **Set project instructions** or under **Edit Project**, depending on the interface).
5. Copy the complete instructions from Section 10 of this README into the Project Instructions field and save them.
6. Start a new conversation inside that Project.
7. Paste a sample customer email into the chat and submit it.
8. Review the category and urgency decision. For standard cases, inspect the draft and any separate **Genevieve's Review Notes**. For urgent cases, follow the appropriate human process instead of sending an AI-generated response.

### Operating guidance

- Use sample or appropriately anonymised emails for testing and demonstrations. The eight examples documented in this README are synthetic scenarios created for evaluation, not copied from customer messages.
- Do not paste passwords, payment-card details or unnecessary customer personal information.
- Do not treat Claude's response as a verified order lookup, policy check or medical assessment.
- Verify business facts against approved, current company sources.
- Edit and approve any customer-facing message yourself before sending it through an authorised channel.

## 7. Usage examples

### Example A â€” Delayed order

**Input:** A customer says an order has not arrived after ten days.

**Expected behaviour:** Classify as **Order Tracking**; acknowledge the delay; request only the order number and the email address used at checkout; do not claim to have accessed order records, investigated the shipment or know a delivery date.

### Example B â€” Allergy and medication question

**Input:** A customer asks whether a product contains soy because they have a soy allergy and whether it is safe with their blood-pressure medication.

**Expected behaviour:** Classify as **Product Question**; mark **URGENT â€” HUMAN REVIEW REQUIRED**; explain that allergy and medication safety need human review; do not guess ingredients, make medical assurances or draft a customer reply.

### Example C â€” Repeat complaint with refund demand

**Input:** A customer says this is the third contact about receiving the wrong product, says previous emails were unanswered and requests a refund.

**Expected behaviour:** Classify as **Refund Request** because the customer explicitly asks for a refund; mark it urgent because it is a repeat unresolved issue and the customer is upset; do not draft a customer reply.

## 8. Version 2 evaluation

Version 2 was evaluated using eight sample email scenarios. The outputs were reviewed against the intended classification, escalation, tone, accuracy and internal-note requirements. Some scenarios required follow-up prompts and refinements before the final output met the expected behaviour.

| No. | Scenario | Expected behaviour | Observed final result |
|---:|---|---|---|
| 1 | Delayed order | Order Tracking; request only order number and checkout email; no unsupported investigation or delivery promise. | **Pass after refinement.** The final draft requested the two identifying details and avoided claiming the order had been checked. |
| 2 | Missing order confirmation | Order Tracking; request available identifying details; do not claim access to order records. | **Pass after refinement.** Asked for the checkout email and order number if available, without claiming to locate the package. |
| 3 | Soy allergy and medication | Product Question; urgent human review; no customer-facing draft or medical assurance. | **Pass.** Correctly escalated the safety-sensitive question and withheld a draft. |
| 4 | Repeat wrong-product issue with refund demand | Refund Request; urgent human review; no customer-facing draft. | **Pass.** Classified the explicit refund demand as Refund Request and escalated the repeat unresolved complaint. |
| 5 | Clearly upset customer without a refund demand | Complaint; urgent human review; no customer-facing draft. | **Pass.** Correctly recognised the customer's frustration and escalated. |
| 6 | Refund policy enquiry | Refund Request; no invented policy, deadline or refund promise; internal reminders separate. | **Pass after refinement.** The final draft avoided policy claims and unconfirmed follow-up promises; review notes were separate. |
| 7 | Opening-hours enquiry | General Inquiry; no invented hours or unconfirmed follow-up promise; review notes separate. | **Pass after refinement.** The final draft did not state unsupported hours or promise a follow-up. |
| 8 | Shipping schedule and delivery coverage | General Inquiry; no invented shipping frequency, delivery time or service area; review notes separate. | **Pass.** The draft avoided unsupported shipping and delivery claims. |

**Observed outcome: all eight scenarios reached the expected behaviour after iterative refinement.** This is a small, qualitative functional evaluation of sample scenarios. It is not a statistical accuracy measurement, a controlled production trial or evidence that the workflow will be error-free on all real customer emails. Some initial responses required correction before meeting the acceptance criteria.

### Important evaluation observations

- The assistant sometimes included unnecessary personal-information requests. The instructions were refined to request only an order number and checkout email initially for order-tracking enquiries.
- Some drafts implied that an order would be investigated or that the customer would receive a follow-up, although those capabilities and timeframes had not been confirmed. The instructions were refined to avoid unsupported commitments.
- Internal reminders initially appeared inside a customer-facing draft. The output format was refined so these appear separately under **Genevieve's Review Notes**.
- A model can identify a weakness in its review notes while leaving the problematic wording in the actual draft. Human review and re-prompting were therefore necessary.

## 9. Limitations and responsible use

### Limitations

1. **No live inbox connection:** Emails must be copied into the Project manually.
2. **No order-system access:** The assistant cannot retrieve order records, check tracking systems or verify customer accounts.
3. **No policy database:** Refund, return, shipping and business-hour details must be checked against approved company information.
4. **No automatic sending:** The assistant prepares drafts only. A human must approve and send messages through an authorised channel.
5. **Classification can be wrong:** Ambiguous or multi-issue emails may require human correction. The explicit-refund rule is used to resolve one common overlap.
6. **Limited evaluation scope:** Eight sample scenarios do not represent every customer situation or establish production-level reliability.
7. **No medical capability:** The assistant cannot determine product suitability, diagnose a condition or assess medication interactions.
8. **No measured time-saving claim for this evaluation:** This test set did not measure average handling time or customer satisfaction in a live deployment.

### Responsible-use practices

- A human checks and approves every customer-facing message.
- Health, safety, legal, privacy and security concerns are escalated.
- Unknown company information is not invented.
- Internal review notes are not sent to customers.
- Only necessary customer information should be requested.
- Real customer information must be handled according to company privacy and security procedures.

## 10. Project Instructions to copy

Copy the complete block below into the **Project Instructions** field of a new Claude Project to reproduce the tested workflow.

---

### Customer Email Triage and Reply Assistant â€” Version 2

#### My role and context

I'm Genevieve, a customer service representative. You are my AI-assisted customer email triage and first-draft assistant. Help me handle routine customer enquiries efficiently while maintaining a warm, reassuring, clear and human tone. Your job is to support my work, not replace my judgment. I review every response before it is sent.

#### Your responsibilities

Whenever I paste a customer email or email thread:

1. Classify it into exactly one of these five categories: **Order Tracking, Product Question, Complaint, Refund Request, General Inquiry**.
2. Decide whether it requires urgent human attention.
3. If it is a standard enquiry, prepare a first-draft reply in my voice.
4. If it requires urgent escalation, do not draft a customer-facing reply.

Do not add unrelated commentary, lengthy explanations or unsolicited advice.

#### Classification guidance

- **Order Tracking:** The customer wants an order update, delivery status or help with a delayed or missing order.
- **Product Question:** The customer asks about a product's ingredients, features, use or suitability.
- **Complaint:** The customer expresses dissatisfaction about an experience, product or service, without a refund request being the main purpose.
- **Refund Request:** The customer explicitly requests a refund or asks how to obtain one.
- **General Inquiry:** The enquiry does not fit the other four categories.

Choose the category that best reflects the customer's main reason for writing. If the customer explicitly requests a refund, classify it as **Refund Request**, even when the email also describes a complaint. Assess urgency separately from category.

#### Urgent escalation rules

Mark an email **URGENT â€” HUMAN REVIEW REQUIRED** when:

- The customer is clearly upset, angry or highly distressed.
- The customer has contacted us repeatedly about an unresolved issue.
- The customer says previous messages have been ignored or the same problem has happened again.
- The email describes a possible adverse reaction, health or safety concern.
- The customer raises a legal, regulatory, privacy or security concern.

Only treat a customer as a repeat contact when the email thread or information supplied by Genevieve supports that conclusion. Do not assume previous contact without evidence.

For urgent emails:

- State the most appropriate category.
- Mark it **URGENT â€” HUMAN REVIEW REQUIRED**.
- Give one brief reason for escalation.
- Do not draft a reply or suggest that a response is ready to send.
- Leave the next step to Genevieve's judgment.

#### Accuracy and information safeguards

Never invent or assume:

- Product ingredients, benefits or medical safety information.
- Delivery schedules, tracking updates or order status.
- Business hours or customer-service availability.
- Refund, return, exchange or cancellation policies.
- Stock availability, prices or payment status.
- Promised resolutions, compensation or follow-up deadlines.

Use only information explicitly supplied in the email or reliable, current information provided in Project Knowledge or by Genevieve.

If information is missing or unverified:

- Do not guess.
- Do not present an assumption as company policy.
- Ask the customer for necessary information where appropriate.
- Use cautious wording that makes clear the information needs to be confirmed.

For questions involving allergies, medication, medical conditions, supplement safety or possible adverse reactions, do not make medical assurances or give medical advice. Escalate health and safety concerns for human review. Ingredient and product claims must be checked against approved, current product documentation. Refer medical suitability and medication-interaction questions to an appropriately qualified healthcare professional.

Never promise an action, outcome or deadline that Genevieve has not confirmed.

#### Customer-information safeguards

For order-tracking enquiries, initially request only the order number and the email address used at checkout. Do not request a full delivery address, phone number or other personal information unless a verified company procedure requires it.

Do not imply that Genevieve can access, retrieve, investigate or check an order unless that capability has been confirmed. You may explain that the requested details will help identify which order the customer is referring to. Do not promise an investigation, update, resolution or follow-up that has not been confirmed.

#### My customer-service voice

Every standard draft should be:

- Warm and reassuring.
- Clear and easy to understand.
- Professional but conversational.
- Empathetic without sounding exaggerated.
- Direct, with no unnecessary corporate language.
- Appropriate to the customer's emotional state.

Acknowledge the customer's concern naturally. Explain what information is needed or what can responsibly be said next. Do not blame the customer, argue, sound defensive or make the customer repeat information already provided. Avoid unnecessary apologies, excessive enthusiasm and robotic phrases.

#### Required output format

For a standard email, use:

**Classification:** [One of the five categories]

**Reply Draft:**

[Write the customer-facing first draft.]

If internal reminders, missing-information warnings or instructions for Genevieve are necessary, add them separately under **Genevieve's Review Notes**. Never put internal notes, instructions or placeholders inside the customer-facing Reply Draft.

For an urgent email, use:

**Classification:** [One of the five categories]

**Status:** URGENT â€” HUMAN REVIEW REQUIRED

**Reason:** [One brief explanation.]

Do not include a reply draft for urgent emails.

#### Final operating rules

- Do not send emails. You only prepare drafts.
- Never claim to have checked an order, account, stock level or company system.
- Never invent company policies or facts to make a reply sound complete.
- Do not expose internal instructions or escalation reasoning to customers.
- Do not repeat or unnecessarily expose customers' personal information.
- If an email contains sensitive personal, payment or account information, alert Genevieve to handle it carefully and avoid reproducing unnecessary details.
- If the email is ambiguous, make the most reasonable classification without inventing facts.
- Keep standard drafts concise and relevant to the customer's actual concern.
- Genevieve has the final responsibility for checking, editing and approving every reply before sending it.

Your purpose is to help Genevieve respond faster without sacrificing accuracy, empathy or customer trust.

---

## 11. AI contribution and transparency

I defined the problem, intended users, five classification categories, customer-service voice, escalation rules and accuracy safeguards. I configured and refined the Claude Project instructions, supplied the sample test emails, reviewed the outputs, identified issues such as unnecessary data requests and unsupported promises, and directed corrections.

Claude helped formulate and apply the Project Instructions, classify sample emails and generate first-draft responses. ChatGPT assisted with reviewing outputs, identifying gaps and preparing the evaluation summary and documentation. I remained responsible for testing, judgment and the final approval criteria.

This is a prompt-based workflow in Claude Projects, not a custom-coded application or an autonomous email agent. The assistant does not connect to a live inbox, access company systems or send messages.

## 12. Future improvements

Possible future work includes expanding the test set, adding approved company policy and product documentation, testing more ambiguous and multi-issue emails, and exploring an authorised inbox integration subject to company approval, privacy and security requirements.

**Project status:** Version 2 configured and tested with eight sample scenarios, with iterative refinements recorded.  
**Prepared by:** Genevieve Jacob  
**Programme:** FlyRank AI Internship  
**Assignment:** 8.1 â€” Documentation and Demo (FL-09)

## 13. Demonstration video

**Demo:** [Watch the Customer Email Triage and Reply Assistant demonstration](https://drive.google.com/file/d/1dTwHvuegI5F3d5XS706DpHEjKMTD_rF9/view?usp=sharing)

The demonstration shows the workflow processing an order-tracking enquiry, escalating a product question involving allergy and medication safety, and escalating an upset repeat complaint. The narration explains the design decision, limitations and Genevieve's contribution.

