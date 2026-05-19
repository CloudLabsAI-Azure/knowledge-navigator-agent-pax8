# Bonus Challenge: Expand to Full Enterprise Agent and Re-Publish

## Introduction

Congratulations on completing the core lab! In this bonus challenge, you will expand your Knowledge Navigator Agent from a focused 10-document assistant into a full enterprise-grade knowledge hub covering 40+ documents across all Contoso departments. You will also create a second generative AI topic for new employee onboarding and re-publish the enhanced agent to Teams.

## What You Will Do

1. Upload the remaining 30+ Contoso documents to your existing SharePoint site
2. Create a new generative AI topic for new employee onboarding
3. Connect the onboarding topic to the existing Email Document Flow
4. Re-publish the enhanced agent to Microsoft Teams and validate

## Part 1: Expand the SharePoint Knowledge Source

1. Navigate to your SharePoint site: **contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>**

1. Go to the **Documents** library.

1. From the extracted dataset you downloaded in Challenge 1, upload all remaining documents from the **Procurement**, **Sales**, **Support**, and **Operations** folders. This should bring your total to 40+ documents.

1. Wait for all uploads to complete.

1. Return to **Copilot Studio** and navigate to your agent's **Knowledge** section.

1. The SharePoint knowledge source should automatically pick up the new documents. If needed, remove and re-add the SharePoint site URL to force a re-sync.

1. Wait for the knowledge source status to return to **Ready**.

1. Test a cross-department query in the test panel, for example:
   - "What is the vendor onboarding process?"
   - "Tell me about the sales playbook"

1. Verify the agent now answers queries from the newly added departments.

## Part 2: Create New Employee Onboarding Topic

1. In your agent, click **Topics** in the navigation pane.

1. Click **+ Add a topic** and select **Add from description with Copilot**.

1. Enter the following:

   - **Name:** `NewEmployeeOnboarding`
   
   - **Description:**

      ```
      Assist new employees who are learning about the company. Help them understand company policies, procedures, organizational structure, benefits, workplace resources, and onboarding requirements. Use generative answers to search the SharePoint knowledge base for information from documents like the HR Handbook, Onboarding Checklist, IT Governance Policy, Employee Travel Reimbursement guidelines, and other relevant company documents. Provide helpful responses to help new employees get started.
      ```

1. Click **Create** and review the generated topic.

1. If you see variable scope errors, open the **Variables** pane and enable **Receive values from other topics** or **Return values to original topics** for any flagged variables.

1. Click **Save**.

## Part 3: Connect Onboarding Topic to Agent Flow

1. Open the **NewEmployeeOnboarding** topic.

1. At the end of the conversation flow, add a **Message** node asking: "Would you like me to email you any specific onboarding document?"

1. Add a **Question** node to capture the employee's response (Yes/No).

1. If the employee says Yes, add nodes to collect:
   - Document name
   - Employee email
   - Reason (pre-fill with "New employee onboarding")

1. After collecting variables, add the **Email Document Flow** as a tool action (same flow from Challenge 3).

1. Map the variables to the flow inputs (EmployeeEmail, DocumentName, DocumentDescription).

1. Click **Save**.

## Part 4: Re-Publish and Validate

1. In Copilot Studio, click **Publish** to push the updated agent.

1. Return to **Microsoft Teams** and open your **Internal Knowledge Navigator** app.

1. Test the following scenarios:

   - **Cross-department knowledge query:** Ask about procurement or sales policies to confirm the expanded knowledge base works.
   - **New Employee Onboarding topic:** Type "I'm a new employee" or "Help me get started" and walk through the onboarding conversation.
   - **Onboarding document request:** During the onboarding flow, request a document and verify the email is sent.
   - **Original EmailDocument topic:** Confirm the original flow still works correctly.

## Success Criteria

- SharePoint knowledge source expanded to 40+ documents
- Agent answers cross-department queries (Procurement, Sales, Support, Operations)
- NewEmployeeOnboarding topic created and functional
- Onboarding topic connects to the Email Document Flow
- Agent re-published to Teams with all features working

## Congratulations!

You have built a full enterprise-grade **Internal Knowledge Navigator Agent** covering 40+ documents, multiple conversational topics, and automated email actions - all deployed to Microsoft Teams without writing a single line of code!

### Real-World Applications:

This solution can improve knowledge management across:
- **HR and Employee Services:** Onboarding, policies, benefits inquiries
- **IT Support:** Self-service help desk, documentation access
- **Compliance and Training:** Policy distribution, procedure guidance
- **Sales Enablement:** Playbooks, product information, pricing guidelines
- **Operations:** Process documentation, vendor management, procurement workflows
