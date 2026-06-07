# Challenge 01: Create Agent and SharePoint Site

## Introduction

Employees across organizations waste valuable time searching for internal policies, procedures, and guidelines scattered across different departments. Traditional document repositories and file shares make it difficult to find relevant information quickly, leading to repeated questions to managers and colleagues.

In this challenge, you will create an AI-powered Internal Knowledge Navigator using Microsoft Copilot Studio and set up a SharePoint site with 10 key Contoso company documents covering HR, Finance, and IT departments.

## Accessing the Datasets

Please download and extract the datasets required for this challenge here:

```
https://github.com/CloudLabsAI-Azure/hack-in-a-day-data/archive/refs/heads/knowledge-nav.zip
```

> **Note:** For this challenge, you will only upload 10 documents from the HR, Finance, and IT folders. The remaining documents will be used in the Bonus Challenge if you finish early.

## Challenge Objectives

- Sign in to Microsoft Copilot Studio
- Create a SharePoint site and upload 10 key Contoso documents
- Create a new agent for internal knowledge navigation
- Configure basic agent settings and identity

## Steps to Complete

### Step 1: Create SharePoint Site

1. Navigate to the **Microsoft 365** portal:

   ```
   https://myapps.microsoft.com
   ```

1. Sign in with the provided credentials:
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>
   - **Password:** <inject key="AzureAdUserPassword"></inject>

1. If prompted with **"Stay signed in?"**, click **No**.

1. From the Microsoft 365 apps, select **SharePoint**.

   > **Note:** If you are not able to see SharePoint in the MyApps section, navigate to `https://sandboxailabs1001.sharepoint.com/` directly to access SharePoint.

1. Click on **+ Create site** and select **Team site**.

1. On **Select a template** select **Standard team** and click on **Use template**.

1. Configure the new site:
   - **Site name:** **contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>**
   - **Site description:** "Internal knowledge base for company policies and procedures"
   - **Privacy settings:** Set to **Public** (anyone in the organization can access)

1. Click **Next** and add any additional owners if needed, then click **Finish**.

1. Once the site is created, navigate to the **Documents** section.

1. Click **Upload** > **Files** and upload the following 10 documents from the extracted dataset (from the HR, Finance, and IT folders):

   - Contoso_HR_Handbook.docx
   - Contoso_Employee_Leave_Policy.docx
   - Contoso_Employee_Travel_Reimbursement.docx
   - Contoso_Code_of_Conduct.docx
   - Contoso_Finance_Expense_Policy.docx
   - Contoso_Finance_Budget_Guidelines.docx
   - Contoso_Finance_Procurement_Approval.docx
   - Contoso_IT_Governance_Policy.docx
   - Contoso_IT_Hardware_Request_Process.docx
   - Contoso_IT_Security_Guidelines.docx

1. Wait for all files to upload successfully.

1. **Copy the SharePoint site URL** from the browser address bar and paste it into **Notepad** for use in upcoming steps.

   > **Important:** Before copying the URL, click the site name in the breadcrumb (top-left of the page) to navigate back to the site home page. The URL must point to the site root, not the Documents library. Copying from the Documents library page will result in an error in Challenge 2.

   - **Correct format:** `https://yourdomain.sharepoint.com/sites/contoso-documents-######`
   - **Incorrect (do not copy this):** `https://yourdomain.sharepoint.com/sites/contoso-documents-######/Shared%20Documents/Forms/AllItems.aspx`

### Step 2: Create a New Agent

1. Navigate to **Microsoft Copilot Studio**:

   ```
   https://copilotstudio.microsoft.com
   ```

1. Ensure the environment is **ODL_User<inject key="DeploymentID" enableCopy="false"></inject>**.

1. In Copilot Studio, select **Agents** from the left navigation pane, and then click **Create blank agent** to start creating a new agent.

1. In the **Name your agent** dialog, enter the following name and click **Create**:

   ```
   Internal Knowledge Navigator
   ```

1. Wait for the agent to be provisioned.

1. On the overview pane of the agent, click on **edit** inside the Details card to edit the agent's description.

1. Add the following description:

   - **Description:** `This agent helps employees quickly find Contoso company policies, procedures, and guidelines across all departments including HR, IT, and Finance. It provides accurate answers with document citations from official company documents, guides users through common processes, and can trigger helpful actions like emailing documents or creating support tickets.`

1. Click on **Save**.

1. Once done, scroll down and add the following **instructions** by clicking on **edit** inside the Instruction card.

     ```
     - Respond only to queries related to Contoso internal company policies, procedures, business operations, and department-specific guidelines.
     - Retrieve knowledge from the uploaded Contoso company documents stored in SharePoint, including HR handbooks, IT governance policies, and finance procedures.
     - When answering questions:
       - Provide clear, accurate information based strictly on official Contoso documents
       - Always cite the source document name (e.g., Contoso_HR_Handbook.docx)
       - Use professional, helpful language appropriate for internal employees
       - If information isn't in the knowledge base, direct users to the appropriate department contact
     - For common scenarios, guide users through step-by-step processes based on documented procedures
     - Offer to email policy documents or create support tickets when appropriate
     - Maintain employee privacy and confidentiality at all times
     - Focus on providing information from official Contoso documents rather than general knowledge
     ```

1. Click on **Save**.

### Step 3: Test Basic Agent Greeting

1. Click the **Test** button to open the test panel on the right side.

1. In the test pane, the agent should greet you with the welcome message.

1. Try typing a simple question like:
   - "Hello"
   - "What can you help me with?"

1. Verify that the agent responds appropriately with the greeting.

1. Note that specific knowledge questions won't work yet. You'll add knowledge sources in the next challenge.

<validation step="e3108aa0-e0a3-40eb-aaf7-a1af8efb199e" />
 
> **Congratulations** on completing the Challenge! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding Challenge. If you receive a success message, you can proceed to the next Challenge. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help.

## Success Criteria

- Created a SharePoint site with 10 Contoso documents uploaded
- Created a new agent named **Internal Knowledge Navigator**
- Configured agent description and instructions

## Additional Resources

- [Microsoft Copilot Studio Overview](https://learn.microsoft.com/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)  
- [Create your first copilot](https://learn.microsoft.com/microsoft-copilot-studio/fundamentals-get-started)  

Click **Next** at the bottom of the page to proceed to the next page.
