# Level Up Challenge: From Prototype to Production-Ready Enterprise Agent

## Introduction

You built it. You tuned it. You deployed it. Now it is time to go further.

In this Level Up Challenge, you will transform your Knowledge Navigator Agent from a well-built prototype into a production-ready enterprise system. You will flood the knowledge base with 40+ Contoso documents, add a purpose-built onboarding experience for new hires, wire it all to the existing email flow, re-deploy to Teams, and then use the Copilot Studio Analytics Dashboard to measure how well your agent actually performs. This last step is what separates agents that get switched off after a week from ones that become mission-critical tools your organization depends on.

## What You Will Do

1. Upload the remaining 30+ Contoso documents to your existing SharePoint site
2. Verify the expanded knowledge source picks up the new documents
3. Create a new generative AI topic for new employee onboarding
4. Add a document request step to the onboarding topic
5. Connect the onboarding topic to the existing Email Document Flow
6. Re-publish the enhanced agent to Microsoft Teams
7. Test all new and existing capabilities in Teams
8. Open the Analytics Dashboard and review real performance data from your test conversations

## Part 1: Expand the SharePoint Knowledge Source

### Upload Remaining Documents

1. Open your browser and navigate to your SharePoint site:

   ```
   https://cloudlabssandbox.sharepoint.com/sites/contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>
   ```

1. Click **Documents** in the left navigation to open the Documents library.

1. Click **Upload** > **Files** to open the file picker.

1. From the dataset you extracted in Challenge 1, navigate to and select all documents from the following folders:
   - **Procurement** folder (all .docx files)
   - **Sales** folder (all .docx files)
   - **Support** folder (all .docx files)
   - **Operations** folder (all .docx files)

   > **Note:** You can hold **Ctrl** and click multiple files to select them all at once before clicking Open.

1. Wait for all uploads to complete. You should now have 40+ documents in the Documents library (10 original plus 30+ new ones).

1. Verify the uploads by scrolling through the Documents library and confirming documents from all departments are visible (HR, Finance, IT, Procurement, Sales, Support, Operations).

### Verify Knowledge Source Re-Index

1. Navigate to **Microsoft Copilot Studio**:

   ```
   https://copilotstudio.microsoft.com
   ```

1. Open your **Internal Knowledge Navigator** agent.

1. Click **Knowledge** in the left navigation pane.

1. Locate the **contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>** knowledge source.

1. Check the status. It may show **Syncing** while it picks up the new documents.

   > **Tip:** If the status stays at **Ready** without re-syncing, or if the agent cannot answer questions about the new documents, you can force a re-sync by clicking the knowledge source name, removing it, and then re-adding the same SharePoint site URL.

1. Wait for the status to return to **Ready** before proceeding.

### Test the Expanded Knowledge Base

1. Click the **Test** button to open the test panel.

1. Click **New test session** to start a fresh conversation.

1. Type the following queries and verify the agent responds with relevant information from the newly uploaded documents:

   - `What is the vendor onboarding process?`
   - `Tell me about the sales playbook`
   - `How does Contoso handle customer support escalations?`

1. Verify that each response cites source documents from the newly uploaded folders (Procurement, Sales, or Support).

## Part 2: Create New Employee Onboarding Topic

### Create the Topic Using AI

1. In your **Internal Knowledge Navigator** agent, click **Topics** in the navigation pane.

1. Click **+ Add a topic** and select **Add from description with Copilot**.

1. Enter the following details:

   - **Name:** `NewEmployeeOnboarding`

   - **Description:**

      ```
      Assist new employees who are just joining Contoso and learning about the company. This topic should trigger for phrases like "I'm a new employee", "help me get started", "new hire orientation", "onboarding help", and "what do I need to know as a new employee". Greet the new employee warmly and ask what they would like to know about - company policies, IT setup, benefits, workplace resources, or general procedures. Use the knowledge base to answer their questions by searching documents like the HR Handbook, IT Governance Policy, Employee Travel Reimbursement guidelines, Code of Conduct, and Finance Expense Policy. After answering their initial question, ask if they would like any specific onboarding document emailed to them.
      ```

1. Click **Create** and wait for the topic to be generated.

1. Review the generated topic nodes in the authoring canvas.

1. **Important:** If you see an error about limited scope or variables:
   - Open the **Variables** pane (click the **{x}** icon in the top toolbar).
   - Click on each variable listed under **Topic**.
   - Enable the checkbox for **Receive values from other topics** or **Return values to original topics** for any variable showing an error indicator.

1. Click **Save**.

### Add a Document Request Question

1. In the **NewEmployeeOnboarding** topic, scroll to the bottom of the authoring canvas to find the last message node.

1. After the last message node, select the **+** icon to add a new node.

1. Select **Ask a question**.

1. Enter the question:

   ```
   Would you like me to email you any specific onboarding document, such as the HR Handbook or IT Security Guidelines?
   ```

1. Set **Identify** to **Multiple choice options**.

1. Add the following two options:

   - `Yes, email me a document`
   - `No, I'm good for now`

1. Save the response as a variable named `OnboardingDocRequest`.

1. Click **Save**.

## Part 3: Connect Onboarding Topic to Agent Flow

### Add Conditional Document Collection

1. Below the **Question** node, add a **Condition** node.

1. Configure the condition:
   - **If** `OnboardingDocRequest` **is equal to** `Yes, email me a document`

### Collect Document Details in the Yes Branch

1. Under the **Yes** branch, select the **+** icon and add **Ask a question**.

1. Enter:

   ```
   What is the name of the document you would like sent to you?
   ```

1. Set **Identify** to **User's entire response** and save the response as a variable named `OnboardingDocName`.

1. Add another **Ask a question** node below it. Enter:

   ```
   What is your email address?
   ```

1. Set **Identify** to **User's entire response** and save the response as `OnboardingEmail`.

1. Add a **Message** node below, with the text:

   ```
   Thank you! I will submit a request to have that document sent to your inbox. This is a great way to build your onboarding reading list.
   ```

### Wire to the Email Document Flow

1. Below the Message node, select the **+** icon and choose **Add a tool**.

1. Select **Email Document Flow** from the list of available flows.

1. Map the flow inputs:
   - **EmployeeEmail:** Select `OnboardingEmail`
   - **DocumentName:** Select `OnboardingDocName`
   - **DocumentDescription:** Type the static text `New employee onboarding document request`

      > **Note:** For the DocumentDescription input, you can type a static string directly rather than mapping a variable, since the reason is always the same in this context.

1. Click **Save**.

### Configure the No Branch

1. Under the **No, I'm good for now** branch, select the **+** icon and add a **Message** node.

1. Enter:

   ```
   No problem! Feel free to come back anytime you have a question about company policies, IT setup, or HR procedures. Welcome to the team!
   ```

1. Click **Save**.

## Part 4: Re-Publish and Validate in Teams

> **Checkpoint:** Before republishing, make sure you have saved all changes in the NewEmployeeOnboarding topic and confirmed the Email Document Flow is still published and active. A quick check in the Flows section of the agent confirms this.

### Publish the Updated Agent

1. In Copilot Studio, click the **Publish** button (top-right of the agent canvas).

1. Click **Publish** again in the confirmation dialog.

1. Wait for the publish to complete successfully.

### Return to Microsoft Teams

1. Open **Microsoft Teams** in your browser.

1. Navigate to the **Internal Knowledge Navigator** app (already installed in Challenge 7).

1. If the app does not show updated behavior immediately, close and re-open the chat with the agent.

### Test All Scenarios in Teams

#### Test Cross-Department Knowledge Query:

1. In the Teams agent chat, type:

   ```
   What is the vendor onboarding process?
   ```

1. Verify the agent responds with information from the Procurement documents and cites a source file.

#### Test New Employee Onboarding Topic:

1. Type:

   ```
   I'm a new employee, help me get started
   ```

1. Verify the **NewEmployeeOnboarding** topic triggers and the agent greets you as a new employee.

1. Follow the conversation and ask about a topic such as company benefits or IT setup.

1. When asked if you want a document emailed, select **Yes, email me a document**.

1. Provide:
   - Document name: `HR Handbook`
   - Email: **<inject key="AzureAdUserEmail"></inject>**

1. Verify the agent confirms the request and sends the email.

1. Check your inbox (**<inject key="AzureAdUserEmail"></inject>**) to confirm the onboarding document request email was received.

#### Confirm Original Topics Still Work:

1. Click **New conversation** to reset.

1. Type:

   ```
   Raise a email document request
   ```

1. Complete the EmailDocument flow as before and verify the email arrives.

1. Start a new conversation and type:

   ```
   I need help from Finance
   ```

1. Verify the **DepartmentSupport** topic triggers and the Finance department message is displayed.

## Part 5: Read Your Agent's Performance in Analytics

Your agent is live and being used. Now you will review real data from your test conversations to understand what is working and what needs tuning. The Copilot Studio Analytics Dashboard captures every conversation, topic trigger, and unrecognized intent from the moment you published.

### Open the Analytics Dashboard

1. In **Microsoft Copilot Studio**, open your **Internal Knowledge Navigator** agent.

1. In the left navigation pane, click **Analytics**.

1. You will land on the **Overview** tab. Review the top-level metrics:
   - **Total conversations** - how many test sessions you ran
   - **Engagement rate** - percentage of conversations where the agent responded with a topic (not just the fallback)
   - **Resolution rate** - percentage of conversations where the user's need was resolved
   - **Escalation rate** - percentage of conversations that escalated to a human (or hit the Fallback topic)

   > **Note:** Since this is a lab environment, you will see a small number of conversations from your own test runs. In production, these numbers reflect real employee usage. Resolution rate is the key metric to track over time.

### Inspect Topic Performance

1. Click the **Topics** tab in the Analytics navigation.

1. You will see a table listing every topic that was triggered, ranked by the number of times it was triggered.

1. Look for the following topics in the list and note how many times each was triggered during your tests:
   - **DepartmentSupport**
   - **EmailDocument**
   - **NewEmployeeOnboarding**
   - **Fallback** (system topic - check how often the agent could not match a query)

1. Click on **DepartmentSupport** to drill into its performance. Review which branches (HR, Finance, IT, General) were triggered most often during your test conversations.

1. Click **Back** and then click on **Fallback** in the topic list. Note how many times the Fallback was triggered - this tells you how often the agent could not recognize user intent.

   > **Insight:** A high Fallback rate in production means your trigger phrases need expansion or users are asking in ways you did not anticipate. You can fix this by adding more trigger phrases to your topics or by tuning the AI settings you configured in Challenge 6.

### Review Unrecognized Utterances

1. Click the **Unrecognized** tab (may also appear as **Unrecognized phrases** depending on your tenant version).

1. This tab lists the exact messages users sent that the agent could not match to any topic.

1. Review the list from your test sessions. If you typed the "What is the weather like in Narnia?" test from Challenge 6, you should see it here.

1. For each unrecognized phrase in the list:
   - Ask yourself: should this trigger an existing topic?
   - If yes, go to that topic and add the phrase as a new trigger phrase.
   - If no, it is a genuine out-of-scope query that the Fallback redirect handles correctly.

1. Add at least one phrase from the Unrecognized list as a new trigger phrase to the most relevant topic. Click **Save** on that topic to apply the improvement.

   > **Note:** This loop - deploy, observe, improve - is the real-world agent maintenance cycle. Organizations that build high-performing agents review their Unrecognized phrases weekly and keep expanding topic coverage based on what employees actually ask.

### Check Conversation Transcripts

1. Click the **Conversations** tab.

1. Select any conversation from the list to open the transcript.

1. Read through the full conversation flow. You can see exactly which topic was triggered, which nodes were visited, and where the conversation ended.

1. Look for a conversation where you tested the EmailDocument topic. Verify the transcript shows the correct topic nodes being traversed (question nodes, variable capture, the flow action node).

1. Look for a conversation where the agent routed through Fallback to DepartmentSupport. Verify the transcript shows the full redirect path.

## Success Criteria

- SharePoint knowledge source expanded to 40+ documents covering all Contoso departments
- Agent answers cross-department queries (Procurement, Sales, Support, Operations)
- **NewEmployeeOnboarding** topic created, tested, and functional
- Onboarding topic collects document name and email, then connects to the Email Document Flow
- Onboarding document request email is received in the lab inbox
- Agent re-published to Teams with all features working
- All previously built topics (EmailDocument, DepartmentSupport) continue to work correctly after re-publish
- Analytics Dashboard reviewed: total conversations, topic triggers, and Fallback rate noted
- At least one unrecognized utterance identified and added as a trigger phrase to improve agent coverage

## You Leveled Up!

You have built and shipped a production-ready **Internal Knowledge Navigator Agent** covering 40+ documents, multiple conversational topics (AI-generated and manually authored), conditional branching, automated email actions, intelligent fallback routing, a branded greeting, generative AI tuning, deployment to Microsoft Teams, and a live analytics review loop - all without writing a single line of code.

This is not a demo. This is how real enterprise agents get built.

### Where This Goes in the Real World

This pattern powers enterprise AI transformations across many domains:

- **HR and Employee Services:** Onboarding guidance, policy lookups, leave request assistance, benefits inquiries
- **IT Support:** Self-service help desk, hardware request processing, security policy distribution, software access guidance
- **Compliance and Training:** Policy distribution, regulatory procedure guidance, audit documentation support
- **Finance:** Expense policy clarification, budget guidance, procurement approval workflows
- **Sales Enablement:** Playbook distribution, product documentation access, pricing guideline lookups
- **Operations:** Vendor onboarding, process documentation, supply chain procedure guidance

The analytics skills you practiced in Part 5 are what keep these agents improving month after month. You now know how to build them and how to measure them.
