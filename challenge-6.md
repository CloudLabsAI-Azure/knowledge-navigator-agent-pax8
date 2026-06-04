# Challenge 06: Tune Agent Intelligence - Fallback, Greeting, and Generative Settings

## Introduction

You now have a working agent with topics, flows, and a knowledge source - but it is still behaving like a prototype. Real production agents need to handle edge cases gracefully: what happens when a user asks something completely outside the agent's scope? What does the agent say the moment a conversation opens? How aggressively should it use the knowledge source to generate answers?

In this challenge, you will move beyond topic authoring and tune the agent's underlying intelligence layer. You will customize two critical system topics (Fallback and Greeting), adjust the generative AI settings that control how the knowledge source answers, and polish the agent's profile so it looks like a real enterprise product before it goes live in Teams.

## Challenge Objectives

- Customize the **Fallback** system topic to redirect unrecognized queries to the DepartmentSupport topic instead of dead-ending the user
- Personalize the **Greeting** system topic with a branded Contoso welcome message
- Configure the agent's **Generative Answers** settings to control how the knowledge source is used
- Validate that fallback routing, the greeting, and generative settings all behave correctly in the test panel

## Prerequisites

Before starting this challenge, ensure you have:
- Completed Challenge 5 (EmailDocument topic wired to Email Document Flow and tested end-to-end)
- Access to **Microsoft Copilot Studio**

## Steps to Complete

### Step 1: Customize the Fallback System Topic

The Fallback system topic fires whenever a user sends a message that does not match any authored topic trigger phrase and cannot be answered from the knowledge source. By default it displays a generic "I'm not sure how to help" message and stops. In a production agent, you should redirect the user to a helpful next step instead.

1. In your **Internal Knowledge Navigator** agent, click **Topics** in the navigation pane.

1. At the top of the Topics list, click the **System** tab to switch from custom topics to system topics.

   > **Note:** System topics are pre-built topics that Copilot Studio manages automatically. You can customize their contents but cannot delete or disable them.

1. Locate the **Fallback** topic in the list and click it to open it.

1. Review the existing nodes in the Fallback topic. You will see a default **Message** node with text similar to "I'm sorry, I'm not sure how to help with that."

1. Click on the existing Message node and replace the text with:

   ```
   I am sorry, I could not find an answer to your question. Let me connect you to the right department so you can get the help you need.
   ```

1. Below the Message node, select the **+** icon to add a new node.

1. Select **Redirect to another topic**.

1. In the topic picker, select **DepartmentSupport**.

   > **Note:** This redirect means that whenever the agent cannot answer a query, it automatically routes the user into the DepartmentSupport topic where they can pick their department, get guidance, and optionally request a document. This turns dead-end failures into productive conversations.

1. Click **Save**.

### Step 2: Personalize the Greeting System Topic

The Greeting system topic fires the moment a user opens a conversation. The default message is generic. You will replace it with a branded Contoso message that sets the right context.

1. In the **System** topics tab, locate the **Greeting** topic and click it to open it.

1. Find the existing **Message** node. It will contain default text like "Hi! How can I help you today?"

1. Click on the Message node and replace the entire text with:

   ```
   Welcome to the Contoso Knowledge Navigator!

   I am your internal AI assistant. I can help you:
   - Find company policies and procedures across HR, Finance, and IT
   - Connect you with the right department team
   - Send a document access request to the admin team on your behalf

   What can I help you with today?
   ```

1. Click **Save**.

1. To test the greeting, click the **Test** button to open the test panel.

1. Click **New test session** to start a fresh conversation.

1. Verify the agent opens with your new branded Contoso greeting message.

### Step 3: Configure Generative Answers Settings

Generative answers control how the agent uses your SharePoint knowledge source to respond to questions. You will review and configure this to ensure the agent uses the knowledge source confidently without fabricating information.

1. In the left navigation pane, click **Settings** (the gear icon).

1. Select **AI** from the Settings menu.

1. Under **Generative AI**, review the current configuration options:
   - **Content moderation** - controls how strictly the agent filters responses
   - **Knowledge** - controls whether the agent searches the connected knowledge source

1. Set **Content moderation** to **Moderate**. This setting balances helpfulness with safety, allowing the agent to provide detailed policy information without over-filtering.

   > **Note:** **High** causes the agent to refuse many legitimate policy questions. **Low** allows unrestricted responses. **Moderate** is the recommended setting for an internal HR/IT knowledge agent.

1. Under the **Knowledge** section, verify that your SharePoint knowledge source (**contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>**) appears in the list with its toggle turned **on** (blue).

1. Click **Save** to apply the settings.

### Step 4: Validate Fallback Routing in the Test Panel

Test that your fallback customization works correctly by sending a query the agent cannot recognize.

1. Click the **Test** button to open the test panel.

1. Click **New test session**.

1. Type a message that would not match any topic or knowledge document:

   ```
   What is the weather like in Narnia?
   ```

1. Verify the agent:
   - Shows your new custom fallback message (*"I am sorry, I could not find an answer..."*)
   - Automatically transitions into the **DepartmentSupport** topic and presents the department selection menu

1. Select a department option to confirm the full redirect flow completes successfully.

### Step 5: Update the Agent Profile and System Instructions

Before publishing, update the agent's display name, description, and system instructions so it presents professionally to employees in Teams.

1. In the left navigation pane, click **Settings**.

1. Select **Agent details**.

1. Update the **Name** field to:

   ```
   Internal Knowledge Navigator
   ```

1. Update the **Description** field to:

   ```
   Your internal Contoso AI assistant for finding company policies, procedures, and documents across HR, Finance, and IT. Available 24/7 to answer questions and connect you with the right team.
   ```

1. Update the **Instructions** field (agent-level system prompt) to:

   ```
   You are the Internal Knowledge Navigator for Contoso. Your role is to help employees find accurate information from company documents stored in SharePoint. Always ground your answers in the connected knowledge source. Do not speculate or invent policy details. If you cannot find an answer, offer to connect the employee with the right department or help them request the document via the email document flow.
   ```

1. Click **Save** to apply all changes.

1. Open the test panel, start a **New test session**, and type:

   ```
   What is the company stock price?
   ```

1. Confirm the agent responds helpfully without fabricating financial data - either acknowledging it does not have that information or routing through the Fallback redirect.

## Success Criteria

- The **Fallback** system topic shows a custom redirect message and routes users to **DepartmentSupport** instead of a dead end
- The **Greeting** system topic displays the branded Contoso welcome message at the start of every new conversation
- **Generative Answers** content moderation is set to **Moderate** and the SharePoint knowledge source toggle is confirmed on
- Agent details (name, description, instructions) are updated and saved
- All test-panel validations pass as described

## Additional Resources

- [Customize system topics](https://learn.microsoft.com/microsoft-copilot-studio/authoring-system-topics)
- [Configure generative answers](https://learn.microsoft.com/microsoft-copilot-studio/nlu-boost-conversations)
- [Set agent instructions](https://learn.microsoft.com/microsoft-copilot-studio/nlu-generative-answers-custom-data)
- [Manage agent settings](https://learn.microsoft.com/microsoft-copilot-studio/configure-bot-greeting)

Click **Next** at the bottom of the page to proceed to Challenge 7.
