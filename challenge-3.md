# Challenge 03: Create Agent Flow for Document Access Request

## Introduction

Your Internal Knowledge Navigator agent can now answer employee questions by searching through the Contoso SharePoint knowledge base. However, a truly useful enterprise agent should go beyond just providing answers - it should also be able to take actions on behalf of employees. One common workplace scenario is when an employee needs a specific document sent to their inbox or wants to submit a formal access request for restricted content.

In this challenge, you'll extend your agent's capabilities by creating an agent flow that sends document access request emails via the Office 365 Outlook connector. This flow will be created directly within Copilot Studio and will be ready to integrate with a conversational topic in Challenge 4.

## Challenge Objectives

- Create an agent flow within Copilot Studio for sending document access request emails
- Configure flow inputs (employee email, document name, description) and outputs (email status)
- Add the Send an email (V2) action via Office 365 Outlook
- Publish the flow and verify it is ready for integration

## Prerequisites

Before starting this challenge, ensure you have:
- Completed Challenge 1 (created the **Internal Knowledge Navigator** agent)
- Completed Challenge 2 (connected SharePoint knowledge source)
- Access to **Microsoft Copilot Studio**

## Steps to Complete

### Step 1: Navigate to Agent Actions

1. In your **Internal Knowledge Navigator** agent, click **Topics** in the navigation pane.

1. Click **+ Add a topic**.

1. Select **Add from description with Copilot**.

1. Enter the following details:

   - **Name:** `EmailDocument`
   
   - **Description:**

      ```
      This topic handles when employees want to submit a document access request via email. It should trigger for phrases like "submit a document request", "request document access", "email me a document", "send me a document", and "I want to request a document". Ask the user to type the name of the document they need as a text response. Ask the user to type their email address as a text response. Ask the user to briefly describe why they need the document as a text response. After collecting all the details, send a message saying their request has been submitted and the admin team will review it.
      ```

1. Click **Create**.

1. Review the generated topic.

1. **Important:** If you see an error about limited scope or variables:
   - Open the **Variables** pane.
   - Click on each variable under **Topic**.
   - Enable the checkbox for **Receive values from other topics** or **Return values to original topics** for Variables which shows error.

1. Click **Save**.

### Step 2: Create the Agent Flow

1. In the **EmailDocument** topic, after the **Message** node at the end, select the **+** icon below to add a new node.

1. From the options, select **Add a tool**, and then under **Basic tools**, choose **New Agent flow**.

1. This will open the flow designer.

1. You should already be seeing two flow nodes precreated: **When an agent calls the flow** and **Respond to the agent**.

1. In the **When an agent calls the flow** trigger node, click **+ Add an input**.

1. Select **Text** as the input type.

1. Enter **EmployeeEmail** as the input name and press Enter.

1. Click **+ Add an input** again and add:
   - Type: **Text**
   - Name: **DocumentName**

1. Click **+ Add an input** one more time and add:
   - Type: **Text**
   - Name: **DocumentDescription**

1. You should now have 3 input parameters: EmployeeEmail, DocumentName, and DocumentDescription.

### Step 3: Add Email Action

1. Between the **When an agent calls the flow** and **Respond to the agent** nodes, select the **+** icon to add a new step.

1. In the search box, type **Send an email (V2)** and select **Send an email (V2)** from **Office 365 Outlook**.

1. If prompted to sign in, use Lab credentials: **<inject key="AzureAdUserEmail"></inject>**

1. In the **Confirmation required** pane, select **I have verified this request and trust the source**, and then choose **Allow access**.

1. Configure the email action:

   - **To:** Enter **<inject key="AzureAdUserEmail"></inject>**
   
   - **Subject:** Type: `Document Access Request - ` and then select **DocumentName** from dynamic content.
   
   - **Body:** Enter the following text and add dynamic content where indicated:

      ```
      Hello Admin,

      An employee has submitted a request for access to the following document.

      Requested Document: [Click and add DocumentName dynamic content]
      Reason: [Click and add DocumentDescription dynamic content]
      Requested By: [Click and add EmployeeEmail dynamic content]

      Please review the request and share the document with the employee.

      Thank you,
      Internal Knowledge Navigator
      ```

### Step 4: Configure Output and Publish

1. In the **Respond to the agent** node, click **+ Add an output**.

1. Configure output as follows:

   - Type: **Text**
   - Name: `EmailStatus`
   - Value: Type `Email sent successfully`

1. Click **Publish** in the top-right corner.

1. In the **Your agent flow published successfully!** popup, select **Stay in Flow**.

### Step 5: Rename the Flow

1. In the Flow page, select the **Overview** tab to view the flow details.

1. In the **Overview** tab, select **Edit** to modify the flow details.

1. In the flow designer, click on the flow name at the top (it will have a default name).

1. Change the name to the following:
   ```
   Email Document Flow
   ```

1. Click **Save** to save the renamed flow.

## Success Criteria

- Created the **EmailDocument** topic using generative AI with proper trigger phrases
- Created the **Email Document Flow** agent flow with 3 input parameters (EmployeeEmail, DocumentName, DocumentDescription)
- The flow includes a configured **Send an email (V2)** action via Office 365 Outlook
- The flow has an output parameter (EmailStatus) confirming successful email delivery
- The flow is published and ready for use

## Additional Resources

- [Create flows for Microsoft Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/advanced-flow)
- [Office 365 Outlook connector](https://learn.microsoft.com/connectors/office365/)

Click **Next** at the bottom of the page to proceed to the next page.

   ![](./media/auto-it-gt-gr-g6.png)
