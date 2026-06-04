# Challenge 07: Publish Agent to Microsoft Teams

## Introduction

The final step is to deploy your Internal Knowledge Navigator agent to Microsoft Teams, making it accessible to employees in your organization. Teams is the perfect channel for knowledge sharing, as employees can get help directly where they already collaborate and communicate.

In this challenge, you will publish your agent, add it to Teams, and test the complete user experience.

## Challenge Objectives

- Publish the agent to Microsoft Teams
- Test topics and flows in Teams

## Steps to Complete

### Step 1: Publish the Agent to Microsoft Teams

1. In **Copilot Studio**, ensure you're in your **Internal Knowledge Navigator** agent.

1. Select **Channels**, and then choose **Teams and Microsoft 365 Copilot** under *Microsoft channels*.

1. Uncheck the **Make agent available in Microsoft 365 Copilot** checkbox, review the **Agent preview** section, and then click **Add channel**.

1. After the channel is added successfully, select **See agent in Teams** under *Agent preview*.

1. If prompted with **Open Microsoft Teams?**, select **Cancel** to proceed.

1. On the Teams welcome page, select **Use the web app instead** to continue in the browser.

1. In Microsoft Teams, select **Add** to install the **Internal Knowledge Navigator** app.

   > **Note:** If you do not see the **Add** option, return to the previous steps and reperform.

1. After the app is added successfully, select **Open** to launch **Internal Knowledge Navigator**.

### Step 2: Test Your Agent in Teams

Test the topics you created and the agent's knowledge search capability:

#### Test Knowledge Search:

1. In the agent chat in Teams, type:
   ```
   Where can I find information about employee benefits?
   ```

2. Verify the agent searches the SharePoint knowledge base and provides relevant information.

3. Verify generative answers are provided from the knowledge base.

#### Test EmailDocument Topic:

1. Click **New test session** to start a fresh conversation.

2. Type:
   ```
   Raise a email document request
   ```

3. Follow the conversation:
   - Provide the document name (e.g., "HR Handbook")
   - Provide your email address
   - Provide a brief reason

4. Verify the agent confirms that the request has been submitted.

5. Check your email inbox (**<inject key="AzureAdUserEmail"></inject>**) to verify you received the document access request email with the document name, reason, and requester email.

#### Test DepartmentSupport Topic:

1. Click **New test session** to start a fresh conversation.

2. Type:
   ```
   I need help from IT
   ```

3. Verify the agent responds with the IT department support message.

4. Try another branch:
   ```
   What HR policies are available?
   ```

5. Verify the agent responds with the HR department message.

<validation step="9751e1d6-33e8-49fa-96b2-31b3df217ba5" />
 
> **Congratulations** on completing the Challenge! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding Challenge. If you receive a success message, you can proceed to the next Challenge. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help.

## Success Criteria

- Agent is published to Microsoft Teams
- Knowledge search returns grounded answers in Teams
- EmailDocument topic triggers the flow and sends the email successfully from Teams
- DepartmentSupport topic responds correctly with department-specific guidance in Teams

## Additional Resources

- [Publish your agent](https://learn.microsoft.com/microsoft-copilot-studio/publication-fundamentals-publish-channels)  
- [Deploy to Microsoft Teams](https://learn.microsoft.com/microsoft-copilot-studio/publication-add-bot-to-microsoft-teams)  
- [Analyze agent performance](https://learn.microsoft.com/microsoft-copilot-studio/analytics-overview)  
- [Share your agent](https://learn.microsoft.com/microsoft-copilot-studio/admin-share-bots)

## Congratulations!

You have successfully built and deployed an **AI-powered Internal Knowledge Navigator Agent** using Microsoft Copilot Studio!

If you still have time remaining, proceed to the **Level Up Challenge** to expand your agent into a full enterprise-grade production assistant.

Click **Next** at the bottom of the page to proceed to the Level Up Challenge.
