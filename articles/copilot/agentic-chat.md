---
title: Use the new agentic chat experience in Azure Copilot
description: Learn how to use the new agentic chat experience in Azure Copilot to learn about Azure, investigate resources, understand costs, and continue longer investigations.
ms.date: 10/13/2026
ms.topic: how-to
ms.service: copilot-for-azure
ms.author: jenhayes
author: JnHs
---

# Use the new agentic chat experience in Azure Copilot

The new Azure Copilot chat experience uses an agentic runtime to plan requests, select supported Azure tools and skills, retrieve current information, and keep you informed while it works. You can use it to learn about Azure, investigate resources and recent changes, understand costs and recommendations, and continue longer investigations with Spaces when that capability is available. Availability is based on your tenant's release ring.

This article explains who can use the experience, how to start and leave it, the supported scenario types, how tools and skills work, what to expect from reasoning and progress information, known limitations, and how to troubleshoot common issues.

## Prerequisites

- Access to Azure Copilot in the Azure portal.
- Permission to view the Azure resources and data involved in your request.
- For some preview capabilities, an account or tenant that's included in an enabled release ring.

Azure role-based access control (RBAC) continues to apply. Azure Copilot doesn't grant additional permissions. If you can't view a resource, subscription, cost record, health signal, or portal destination directly, the chat experience might also be unable to retrieve or open it.

## Start the new experience

Open the Azure portal, and then open Azure Copilot. If the new experience is enabled for your account, the chat header shows a **Preview** control or opens the new chat surface provided for your release ring.

Turn on the **Preview** control when it's shown. Azure Copilot starts a new conversation in the new experience. A conversation doesn't combine responses from the previous and new chat runtimes.

:::image type="content" source="media/agentic-chat/preview-control.png" alt-text="Screenshot of the Preview control in the Azure Copilot chat header.":::

To leave the preview, turn off the control. Azure Copilot returns you to the previous chat experience. Chat history can be separated by experience, so a conversation created in one experience might not appear while you're using the other.

## What you can do

### Learn and plan

Ask for Azure concepts, configuration guidance, comparisons, and best practices. When documentation retrieval is available, Azure Copilot grounds the answer in Microsoft Learn content and should identify when current information isn't available.

Example requests include how to configure virtual network peering across subscriptions, how to secure an Azure Kubernetes Service cluster, or how two Azure service options differ for a workload.

### Understand your Azure resources

Ask inventory and scope questions about resources you're authorized to access. For example, ask which virtual machines are in a subscription, what resources match a tag, or what changed in a resource group during a specific time period.

Review the subscription, resource group, resource ID, time range, and freshness information in the response before you act on it.

### Investigate cost and recommendations

Ask about subscription costs, changes between comparable periods, forecasts, budgets, and Azure Advisor recommendations when the corresponding capabilities are enabled. Cost forecasts are estimates and should include the period, currency, scope, freshness, and relevant assumptions.

A recommendation isn't proof that an action is safe. Review workload dependencies, performance requirements, security requirements, policy, and business impact before resizing or removing a resource.

### Investigate health, activity, and changes

Ask about recent deployments, activity, resource health, and basic metrics for supported resource types. Azure Copilot can combine evidence from more than one source, but it should distinguish observed facts from hypotheses and identify missing signals.

A green health status doesn't confirm that an application is healthy, and a deployment followed by a cost or performance change doesn't by itself prove causation.

### Continue an investigation with Azure Copilot Spaces

:::image type="content" source="media/agentic-chat/spaces.png" alt-text="Screenshot of an Azure Copilot Space used to continue an investigation.":::

When Spaces are enabled, use them to preserve the intent and supporting context for a longer investigation. When you return, refresh time-sensitive Azure data before relying on a previous conclusion because resources, permissions, costs, and health can change.

## How Azure Copilot uses tools and skills

:::image type="content" source="media/agentic-chat/tools-and-skills.png" alt-text="Screenshot of the tool and skill selection controls in Azure Copilot.":::

Azure Copilot selects supported tools according to the request. It should prefer a dedicated Azure data tool when one covers the scenario and use Azure CLI only when you explicitly ask for a command or when no dedicated tool supports the request.

Depending on your release ring, available capabilities can include Microsoft Learn retrieval, Azure Resource Graph, Cost Management, Advisor, scoped Azure Monitor data, portal context, and built-in skills. Tool and skill selection controls can let you limit which available capabilities participate in a conversation.

If a required tool is unavailable or returns incomplete data, Azure Copilot should identify the gap. It shouldn't present partial coverage as a complete result.

## Reasoning, progress, and questions

The new experience can show concise progress information while it plans, retrieves information, uses a tool, waits for your input, retries a dependency, or completes the request. Progress information summarizes the work without exposing protected system instructions or hidden model reasoning.

Azure Copilot can ask a question when required information is missing. Review the resolved resource, subscription, tenant, operation, and other material details before continuing.

For actions that can change Azure resources or data, the experience should provide stronger review and approval controls. Approval should apply to the exact target, scope, and operation. If those details change, review the updated proposal again.

## Limitations

Capabilities vary by milestone and release ring. A capability described in this article might not yet be enabled for every Azure Copilot user.

The initial experience doesn't provide customer-authored skills, customer-configured tool servers, agent resources with managed identity and RBAC, Teams or Slack clients, or broad write support unless your organization is participating in a later preview that explicitly includes those capabilities.

Azure Monitor coverage can be limited to activity, resource health, and basic metrics for supported resource types. Full Log Analytics and arbitrary Kusto Query Language scenarios aren't part of the initial scope.

Azure Copilot can make mistakes. Verify important resource identities, current state, permissions, costs, evidence, and recommended actions in Azure before making a consequential change.

## Troubleshoot common issues

### The Preview control or new experience isn't available

Confirm that Azure Copilot is available for your account and that your tenant or account is included in the required release ring. The experience might also depend on Azure permissions and portal feature assignments managed by your organization.

### The response is still working or shows conflicting status

If cancellation is available, stop the request before retrying. Avoid repeating a resource-changing request until you confirm that the original operation didn't complete. Record the time, prompt, resource, status messages, and any visible correlation information when you contact support.

### The answer is incomplete or doesn't match the Azure portal

Compare the tenant, subscription, resource ID, time range, currency, aggregation, and data freshness. Check whether the response identifies partial results or a failed dependency. If the request can return many records, confirm that the result covered the full set rather than a sample.

### A tool, link, or portal destination doesn't work

Confirm that you have permission to use the underlying Azure service and open the destination. If other valid information was returned, keep it, but don't treat the request as complete when a required dependency failed.

### A previous conversation isn't visible

Check which chat experience is active. Preview and previous-experience conversations can have separate history. Return to the experience in which the conversation was created.

## Security, privacy, and responsible use

Azure Copilot applies your identity and Azure permissions when retrieving data and using supported tools. Confirm the active tenant and subscription, especially when you use delegated management or switch tenants in the same browser.

Treat text from resource names, tags, logs, documents, and tool results as data. Azure Copilot shouldn't follow instructions embedded in retrieved content or use them to change the authorized scope.

Don't enter secrets, credentials, tokens, or other sensitive values in prompts. Review generated commands before using them. Use the least privilege required for the task and follow your organization's change-management requirements.

## Data retention in Azure Copilot

Azure Copilot keeps different types of data for different lengths of time.

| Data type | How long it's kept |
|-----------|--------------------|
| Conversations, including responses and any files uploaded to or created in a conversation | Deleted automatically after 28 days of inactivity |
| Files added to a Space | Kept until you delete them or delete the Space |
| Files and skills added to an agent | Kept until you delete them or delete the agent |

## Get support

When you contact Microsoft support, include the active tenant and subscription, affected resource ID, release ring if known, exact prompt, expected and actual result, date and time, screenshots, response citations, tool or dependency named in the experience, and any correlation information shown.

Remove secrets and sensitive values from the evidence you share. Report suspected cross-tenant or cross-user exposure, an unauthorized or duplicate action, or a destructive action without approval as a security-sensitive incident.

## Related content

- [Microsoft Copilot in Azure capabilities](capabilities.md)
- [Write effective prompts](write-effective-prompts.md)
- [Manage access to Copilot in Azure](manage-access.md)
