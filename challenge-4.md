# Challenge 04: Build a Department Support Topic with Conditional Branching

## Introduction

So far you have built an agent that can answer knowledge questions from SharePoint documents and collect document access requests through an AI-generated topic. However, real enterprise agents often need structured conversations where the agent guides users through a series of choices and responds differently depending on what the user selects. This is done through manual topic authoring, where you design the conversational flow node by node.

In this challenge, you will manually create a **DepartmentSupport** topic that presents employees with a department selection menu (HR, Finance, IT, or General) and then routes the conversation to tailored guidance for each choice. You will also add a redirect so that any branch can hand off to the **EmailDocument** topic if the employee wants to request a specific document.

## Challenge Objectives

- Create a new topic manually (without using the AI generator)
- Add trigger phrases so the agent knows when to start this topic
- Use a Question node with multiple-choice options to collect a department selection
- Add Condition nodes to branch the conversation based on the user's choice
- Configure a unique response Message for each department branch
- Add a Question node offering to redirect to the EmailDocument topic for document requests
- Use a Redirect node to hand off to the EmailDocument topic
- Test all branches in the test panel

## Prerequisites

Before starting this challenge, ensure you have:
- Completed Challenge 3 (created the **EmailDocument** topic and published the **Email Document Flow**)
- Access to **Microsoft Copilot Studio**

## Steps to Complete

### Step 1: Create the Topic

1. In your **Internal Knowledge Navigator** agent, click **Topics** in the navigation pane.

1. Click **+ Add a topic** and select **From blank**.

1. At the top of the authoring canvas, click on the default topic name (usually **Untitled**) and rename it to:

   ```
   DepartmentSupport
   ```

1. Click **Save** to save the topic name.

### Step 2: Configure Trigger Phrases

1. In the authoring canvas, click on the **Phrases** box inside the **Trigger** node at the top.

1. Add the following trigger phrases one at a time by typing each phrase and pressing **Enter** after each:

   ```
   I need department help
   ```
   ```
   department support
   ```
   ```
   help from HR
   ```
   ```
   help from IT
   ```
   ```
   help from Finance
   ```
   ```
   contact a department
   ```
   ```
   which department handles
   ```

1. You should now see 7 trigger phrases listed in the Trigger node.

1. Click **Save**.

### Step 3: Add a Welcome Message Node

1. Below the **Trigger** node, select the **+** icon to add a new node.

1. Select **Send a message**.

1. In the Message node, type the following welcome text:

   ```
   Hello! I can connect you with the right department resources. Please select the department you need help with.
   ```

1. Click **Save**.

### Step 4: Add a Department Selection Question Node

1. Below the **Message** node, select the **+** icon to add a new node.

1. Select **Ask a question**.

1. In the **Question** node, enter the following question text:

   ```
   Which department do you need support from?
   ```

1. In the **Identify** dropdown (the field that says what type of answer to expect), select **Multiple choice options**.

1. Under **Options for user**, click **+ New option** and add the following four options one by one:

   - `HR - Human Resources`
   - `Finance`
   - `IT - Information Technology`
   - `General / Other`

1. Under **Save response as**, the system will auto-create a variable. Click on the variable name and rename it to:

   ```
   SelectedDepartment
   ```

1. Ensure **Save response as** is set to **Topic** scope.

1. Click **Save**.

### Step 5: Add Condition Nodes for Each Department Branch

After saving the Question node, Copilot Studio should automatically create a **Conditions** node with branches for each of your four options. If it does not, add one manually:

1. Below the **Question** node, select the **+** icon and choose **Add a condition**.

1. You should see a branching structure with one branch per option (HR, Finance, IT, General/Other) plus an **All other conditions** branch.

   > **Note:** If the branches are not auto-populated, click each branch condition and configure it to check that `SelectedDepartment` is equal to the corresponding option value.

#### Configure the HR Branch:

1. Click the **+** icon under the **HR - Human Resources** branch condition.

1. Select **Send a message** and enter:

   ```
   The HR team covers topics such as employee onboarding, leave policies, the Code of Conduct, and travel reimbursement. Our knowledge base includes the Contoso_HR_Handbook.docx, Contoso_Employee_Leave_Policy.docx, and Contoso_Code_of_Conduct.docx. You can ask me any HR policy question and I will search these documents for you.
   ```

#### Configure the Finance Branch:

1. Click the **+** icon under the **Finance** branch condition.

1. Select **Send a message** and enter:

   ```
   The Finance team handles expense policies, budget guidelines, and procurement approvals. Our knowledge base includes the Contoso_Finance_Expense_Policy.docx, Contoso_Finance_Budget_Guidelines.docx, and Contoso_Finance_Procurement_Approval.docx. Feel free to ask me any finance-related policy question.
   ```

#### Configure the IT Branch:

1. Click the **+** icon under the **IT - Information Technology** branch condition.

1. Select **Send a message** and enter:

   ```
   The IT team manages hardware requests, security guidelines, and IT governance policies. Our knowledge base includes the Contoso_IT_Governance_Policy.docx, Contoso_IT_Hardware_Request_Process.docx, and Contoso_IT_Security_Guidelines.docx. Ask me anything about IT policies or hardware processes.
   ```

#### Configure the General / Other Branch:

1. Click the **+** icon under the **General / Other** branch condition.

1. Select **Send a message** and enter:

   ```
   For general inquiries not covered by a specific department, I will do my best to search the knowledge base. You can also ask me to connect you with the right team. Please describe your question and I will find the most relevant information from the Contoso documents.
   ```

### Step 6: Merge Branches and Offer Document Request

After all four branch messages are configured, add a shared follow-up action after the branches converge.

1. At the bottom of each department branch, there is an **End of branch connector**. These should converge into a single node below the conditions block. If they do not connect automatically, select the **+** at the bottom of each branch and choose **Go to another node**, then select the shared **Message** node you will create below.

1. Below the Conditions block (after all branches merge), select the **+** icon to add a new node.

1. Select **Ask a question** and enter:

   ```
   Would you like me to send you a specific policy document by email?
   ```

1. Set **Identify** to **Multiple choice options** and add two options:

   - `Yes, send me a document`
   - `No, thank you`

1. Save the response as a variable named:

   ```
   WantsDocument
   ```

### Step 7: Add a Redirect Node for Document Request

1. Below the follow-up Question node, add a **Condition** node to check the user's answer.

1. Configure the condition:
   - **If** `WantsDocument` **is equal to** `Yes, send me a document`

1. Under the **Yes** branch, select the **+** icon and choose **Topic management** > **Go to another topic**.

1. Search for and select **EmailDocument** from the topic list.

   > **What this does:** This Redirect node hands off the conversation to the EmailDocument topic, which will collect the document name, email address, and reason from the user and trigger the Email Document Flow to send the request email.

1. Under the **No, thank you** branch, select the **+** icon and choose **Send a message**. Enter:

   ```
   No problem! Feel free to ask me any other policy question or type your query and I will search our knowledge base for you.
   ```

1. Click **Save**.

### Step 8: Test the DepartmentSupport Topic

1. Click the **Test** button to open the test panel.

1. Click **New test session** to start a fresh conversation.

#### Test the IT Branch:

1. Type one of the trigger phrases:

   ```
   I need help from IT
   ```

1. Verify the agent presents the department selection menu with 4 options.

1. Select **IT - Information Technology**.

1. Verify the agent responds with the IT department message referencing the IT governance and security documents.

1. When asked if you want a document sent, select **No, thank you**.

1. Verify the agent responds with the closing message.

#### Test the HR Branch with Document Redirect:

1. Click **New test session** to reset the conversation.

1. Type:

   ```
   department support
   ```

1. Select **HR - Human Resources** from the options.

1. Verify the HR department message is displayed.

1. When asked if you want a document sent, select **Yes, send me a document**.

1. Verify the agent transitions into the **EmailDocument** topic and prompts you for the document name.

1. Complete the EmailDocument flow by providing:
   - Document name: `HR Handbook`
   - Your email: **<inject key="AzureAdUserEmail"></inject>**
   - Reason: `Need to review HR leave policies`

1. Verify the agent confirms the document request has been submitted.

#### Test the Finance Branch:

1. Click **New test session** to reset.

1. Type:

   ```
   which department handles expenses
   ```

1. Select **Finance** from the options.

1. Verify the Finance department message is displayed with references to the Finance documents.

## Success Criteria

- Created the **DepartmentSupport** topic from blank (not AI-generated) with 7 trigger phrases
- Topic has a Question node with 4 multiple-choice department options (HR, Finance, IT, General/Other)
- Each department branch has a unique informational message referencing the relevant Contoso documents
- A follow-up Question node offers to send a document by email
- A Redirect node successfully hands off to the **EmailDocument** topic when the user selects Yes
- All tested branches respond correctly in the test panel
- The IT, HR (with redirect), and Finance branches all work as expected

## Additional Resources

- [Author topics manually in Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/authoring-create-edit-topics)
- [Use condition nodes](https://learn.microsoft.com/microsoft-copilot-studio/authoring-using-conditions)
- [Redirect to another topic](https://learn.microsoft.com/microsoft-copilot-studio/authoring-topic-management)
- [Work with variables](https://learn.microsoft.com/microsoft-copilot-studio/authoring-variables)

Click **Next** at the bottom of the page to proceed to the next page.

   ![](./media/auto-it-gt-gr-g7.png)
