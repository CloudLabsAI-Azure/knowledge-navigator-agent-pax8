# Challenge 02: Connect SharePoint Knowledge Source

## Introduction

Now that you've created your Internal Knowledge Navigator agent and uploaded Contoso company documents to SharePoint in Challenge 1, it's time to connect that SharePoint site to your agent as a knowledge source. This will enable your agent to search through the company documents and provide accurate answers to employee questions.

In this challenge, you'll connect the SharePoint site to Copilot Studio, verify the knowledge source is properly indexed, and test basic knowledge retrieval to ensure your agent can answer questions using the Contoso documents.

## Challenge Objectives

- Connect the SharePoint site as a knowledge source in Copilot Studio
- Configure knowledge source settings
- Verify the agent returns grounded answers with source citations

## Prerequisites

Before starting this challenge, ensure you have:
- Created the **Internal Knowledge Navigator** agent in Challenge 1
- Created the SharePoint site **contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>** in Challenge 1
- Uploaded all 10 Contoso documents to the SharePoint site in Challenge 1
- Saved the SharePoint site URL

## Steps to Complete

### Step 1: Add SharePoint Knowledge Source

1. Open **Microsoft Copilot Studio** in your browser:

   ```
   https://copilotstudio.microsoft.com
   ```

1. Ensure you're in the **ODL_User<inject key="DeploymentID" enableCopy="false"></inject>** environment (check the environment selector in the top-right).

1. Select your **Internal Knowledge Navigator** agent from the agents list.

1. On the **Start building your agent** page, scroll down and select **+ Add knowledge** to add knowledge sources.

1. Select **SharePoint** from the **Add Knowledge** window.

   > **HINT:** Select **SharePoint** from the *Featured* section, as choosing other SharePoint options may result in errors.

1. Enter the **SharePoint site URL** that you copied in Challenge 1 and select **Add**.

   ```
   https://yourdomain.sharepoint.com/sites/contoso-documents-######
   ```

   > **Important:** The URL must point to the SharePoint site root (ending in `/sites/contoso-documents-######`). Do not use a Documents library URL, a file share link, or a URL that contains `/Shared%20Documents` - these will cause an error. If needed, open your SharePoint site in a new tab, click the site name in the breadcrumb to go to the home page, and copy the URL from there.

1. Select **Add to agent** to add the SharePoint knowledge source.

1. Wait for the confirmation message that the SharePoint site has been added.

   > **What's happening:** Copilot Studio is now connecting to your SharePoint site and will automatically index all 10 documents you uploaded in Challenge 1.

### Step 2: Verify Knowledge Source Connection

1. After adding SharePoint, navigate to **Knowledge** in the left navigation pane.

1. You should see the SharePoint site listed as a knowledge source with the name: **contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>**

1. Wait for the status to change to **Ready**.

   > **Note:** The SharePoint connector will automatically index all documents in the Documents library. You don't need to upload individual files.

1. If the status shows **Failed** or **Error**, verify the SharePoint site URL is correct.

### Step 3: Test Knowledge Retrieval

1. Click the **Test** button to open the test panel on the right side.

1. Type: `What is the expense reimbursement policy?`

1. Verify the agent searches the SharePoint knowledge base and provides a relevant answer with a source citation.

1. Try another query: `How do I request new hardware?`

1. Confirm the agent returns information from the IT documents with proper citations.

   > **Note:** The agent should now be able to answer questions grounded in the documents you uploaded. If it says it doesn't have information, wait a few more minutes for indexing to complete and try again.

## Success Criteria

- SharePoint knowledge source is connected to Copilot Studio
- Knowledge source status shows **Ready**
- Agent returns grounded answers with source citations from uploaded documents

## Additional Resources

- [Add knowledge sources to your copilot](https://learn.microsoft.com/microsoft-copilot-studio/nlu-boost-conversations)  
- [Generative answers with uploaded files](https://learn.microsoft.com/microsoft-copilot-studio/nlu-boost-node)  

Click **Next** at the bottom of the page to proceed to the next page.
