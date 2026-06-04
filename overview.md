# Knowledge Navigator Agent (Internal Copilot) - Hack in a Day

Welcome to the Knowledge Navigator Agent (Internal Copilot) Hack in a Day! In this lab, you will build an internal knowledge assistant that helps employees search and access Contoso company documents across multiple departments. You will create an agent with conversational topics, agent flows, and deploy it to Microsoft Teams.

## Scenario

As Contoso grows, employees are finding it harder to locate information spread across departments like HR, Finance, IT, Procurement, Sales, and Operations. Questions like "Where can I find the expense reimbursement policy?" or "What is the process to request new hardware?" generate thousands of internal support emails every month. To cut down on repeated questions and reduce dependency on manual help, the company decides to build a Knowledge Navigator Agent. This agent can search internal documents, answer employee questions, and let employees request access to specific documents through Outlook. The goal is to make knowledge access faster and reduce the load on support teams.

## Introduction

In this lab, you will build a **Knowledge Navigator Agent** that helps employees find information from Contoso's document library, covering HR, Finance, and IT. Using Microsoft Copilot Studio, you will create a conversational AI assistant that searches through company policies and procedures, provides answers from the knowledge base, and can trigger automated actions.

The agent acts as a central place for employees to ask questions about HR handbooks, IT governance, expense reimbursements, and more. You will also create an agent flow that sends a document access request via Outlook to the admin team, so they can review and share the right document with the employee. All of this is done without writing any code.

## Key Tools / Services

In this lab, you will work with:

- **Microsoft Copilot Studio** - Platform for building conversational AI agents without code
- **SharePoint** - For storing and indexing Contoso company documents
- **Agent Flows** - Created within Copilot Studio (not the Power Automate portal) for automated actions
- **Generative AI Topics** - AI-generated conversational topics from natural language descriptions
- **Microsoft Teams** - For deploying the agent
- **Office 365 Outlook** - For sending document access request emails through agent flows

## Learning Objectives

By the end of this Hack in a Day, you will learn how to:

- Create and configure an internal knowledge navigator agent in Microsoft Copilot Studio
- Connect SharePoint as a knowledge source with company documents
- Build an agent flow within Copilot Studio to send document access requests via Outlook
- Use generative AI to create conversational topics from natural language descriptions
- Manually author topics with conditional branching and multi-department routing
- Customize system topics (Fallback, Greeting) and generative AI settings to tune agent behavior
- Connect topics to agent flows and map variables between them
- Deploy and test your agent in Microsoft Teams

## Hack in a Day Format: Challenge-Based

This hack in a day follows a challenge-based format with seven stages that build a complete Internal Knowledge Navigator Agent. Each challenge focuses on a specific capability:

- **Challenge 1: Create Agent and SharePoint Site** - Set up a Copilot Studio agent, create a SharePoint site, and upload 10 key Contoso documents
- **Challenge 2: Connect SharePoint Knowledge Source** - Connect SharePoint to your agent as a knowledge source
- **Challenge 3: Create Agent Flow for Document Access Request** - Build an agent flow within Copilot Studio that sends a document access request email via Outlook
- **Challenge 4: Build a Department Support Topic with Conditional Branching** - Manually author a topic from scratch with department selection menus, conditional branching logic, and a redirect to the document request topic
- **Challenge 5: Connect Topic to Agent Flow and Test End-to-End** - Wire the EmailDocument topic to the published flow, map variables to flow inputs, and run end-to-end tests
- **Challenge 6: Tune Agent Intelligence - Fallback, Greeting, and Generative Settings** - Customize the Fallback and Greeting system topics, configure generative AI settings, update agent profile and instructions, and validate all behavior in the test panel
- **Challenge 7: Publish Agent to Microsoft Teams** - Deploy your agent to Teams and test all topics and flows

Throughout each challenge, you will:
- Build AI agent capabilities using no-code tools
- Configure topics and flows within Copilot Studio
- Test each topic and flow as you go
- End up with a working agent deployed to Microsoft Teams

## Level Up Challenge (For Early Finishers)

If you complete all seven challenges ahead of time, the Level Up Challenge is waiting. You will expand the agent into a full production-ready enterprise assistant by uploading the remaining 30+ Contoso documents, creating a second generative AI topic for new employee onboarding, re-publishing the enhanced agent to Teams, and analyzing real performance data using the Copilot Studio Analytics Dashboard. This is where you go from lab exercise to real-world deployment skill.

## Challenge Overview

You start by creating a new agent in Microsoft Copilot Studio, setting up a SharePoint site, and uploading 10 key Contoso company documents covering HR, Finance, and IT. You then connect this SharePoint site as your agent's knowledge source.

Next, you build an agent flow within Copilot Studio (no external Power Automate portal needed) that sends a document access request email via the Office 365 Outlook connector. When an employee asks for a document, the agent collects the document name, email address, and reason, then sends a request to the admin team to review and share it.

After that, you manually author a **DepartmentSupport** topic from scratch - no AI generation. You design the conversation flow node by node, configure a department selection question with four options (HR, Finance, IT, General), create conditional branches that respond with department-specific guidance referencing the relevant Contoso documents, and add a redirect that hands off to the document request topic when the employee wants a document emailed.

Next, you use Copilot Studio's generative AI feature to create the EmailDocument conversational topic by describing what you want in plain language. The AI generates trigger phrases, conversation flows, and variable capturing for you. You then wire this topic to your agent flow by mapping conversation variables to flow input parameters and run end-to-end tests.

Before publishing, you tune the agent's intelligence layer - customizing the Fallback system topic to redirect confused users to the DepartmentSupport topic instead of dead-ending them, personalizing the Greeting system topic with a branded Contoso welcome, adjusting generative AI content moderation settings, and updating the agent's profile and system instructions so it behaves like a real enterprise product.

Finally, you publish your agent to Microsoft Teams, test all topics and flows, and make it available to your organization.

## Support Contact

The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:

- Email Support: cloudlabs-support@spektrasystems.com  
- Live Chat Support: https://cloudlabs.ai/labs-support

Click **Next** at the bottom of the page to proceed to the next page.

   ![](./media/auto-it-gt-gr-g2.png)

## Happy Hacking!!
