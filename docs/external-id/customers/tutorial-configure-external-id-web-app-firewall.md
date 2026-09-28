---
layout: Conceptual
title: Configure Microsoft Entra External ID with Azure Web Application Firewall - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/tutorial-configure-external-id-web-app-firewall
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to configure Microsoft Entra External ID with Azure Web Application Firewall.
ms.reviewer: kengaderdus
ms.topic: how-to
ms.custom: it-pro
ms.date: 2025-01-09T00:00:00.0000000Z
locale: en-us
document_id: 95e8f95f-f650-17c5-021d-4dd2e03d8078
document_version_independent_id: 95e8f95f-f650-17c5-021d-4dd2e03d8078
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/tutorial-configure-external-id-web-app-firewall.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/tutorial-configure-external-id-web-app-firewall
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/tutorial-configure-external-id-web-app-firewall.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e8fdebed-2921-4997-a75a-fa863723a535
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf1e63a8-325f-42be-b60c-d84a95a42b1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b0508259-a1f3-2e3d-40d0-cfef3aaad48d
---

# Configure Microsoft Entra External ID with Azure Web Application Firewall - Microsoft Entra External ID | Microsoft Learn

In this article, you learn how to enable the [Azure Web Application Firewall](/en-us/azure/web-application-firewall/ag/ag-overview) (WAF) service for a Microsoft Entra External ID tenant. Azure WAF protects web applications from common exploits and vulnerabilities such as cross-site scripting, Distributed Denial-of-Service (DDoS) attacks, and malicious bot activity.

## Prerequisites

- **An Azure subscription**. If you don’t have one, [get an Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) for free.
- **A Microsoft Entra External ID tenant**. Authorization server that verifies user credentials with user flows in the tenant, also known as the identity provider (IdP). Learn how to [create an external tenant](how-to-create-external-tenant-portal).
- **Azure Front Door Premium**. [Azure Front Door](/en-us/azure/frontdoor/) enables custom domains for the Microsoft Entra External ID tenant with security optimization and access to WAF managed rule sets.
- **Azure Web Application Firewall** (requires Premium SKU). [Azure WAF](https://azure.microsoft.com/services/web-application-firewall/) manages traffic that the authorization server receives.
- **A custom domain**. Use with the custom domain features in Azure Front Door. Learn how to [enable custom URL domains for apps in external tenants](how-to-custom-url-domain).

Important

After you configure the custom domain, [test your custom domain](how-to-custom-url-domain#test-your-custom-url-domains) before you use it.

## Enable Azure Web Application Firewall

To enable WAF for protection, configure a WAF policy and associate it with Azure Front Door Premium. Microsoft optimizes Azure Front Door premium for security and manages the rule sets provided by the WAF to protect against common vulnerabilities including cross-site scripting and JavaScript exploits. Additionally, Azure WAF provides rule sets that help protect against malicious bot activity and provide layer 7 DDoS protection for your application.

### Create Azure Web Application Firewall policy

Use the following steps to create the WAF policy.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Under **Azure services**, select **Create a resource**.
3. In the search bar, type **Azure WAF**, then select **Azure Service Web Application Firewall (WAF) from Microsoft**.
4. Select **Create**.
5. Go to **Create a WAF policy**.
6. Select **Basics**.
    - For **Policy for**, select **Global WAF (Front Door)**.
    - For **Front Door SKU**, select the Premium SKU.
    - For **Subscription**, select your Front Door subscription name.
    - For **Resource group**, select your Front Door resource group name.
    - For **Policy name**, enter a unique name for your WAF policy.
    - For **Policy state**, select **Enabled**.
    - For **Policy mode**, select **Detection**.
7. Go to **Create a WAF policy** &gt; **Association**.
8. Select **+ Associate a Front Door profile**.
9. **Front Door**: Select the Front Door name that you associated with your Microsoft Entra External ID custom domain.
10. **Domains**: Select the Microsoft Entra External ID custom domains to which to associate the WAF policy.
11. Select **Add**.
12. Select **Review + create**.
13. Select **Create**.

## Configure default rule set

After you create a new WAF policy, Azure Front Door automatically deploys with the latest version of the [Azure-managed default rule set](/en-us/azure/web-application-firewall/afds/waf-front-door-drs) (DRS). This rule set protects web applications from common vulnerabilities and exploits. Azure-managed rule sets protect against common security threats. Azure manages and updates these rule sets as needed to protect against new attack signatures. The DRS includes the [Microsoft Threat Intelligence Collection rules](/en-us/azure/web-application-firewall/afds/waf-front-door-drs#microsoft-threat-intelligence-collection-rules) that provide increased coverage, patches for specific vulnerabilities, and better false positive reduction.

## Configure bot manager rule set

By default, the Azure Front Door WAF deploys with the latest version of the Azure-managed [bot manager rule set](/en-us/azure/web-application-firewall/afds/afds-overview#bot-protection-rule-set). This rule set categorizes bot traffic into good, bad, and unknown bots. The WAF platform manages and dynamically updates the bot signatures behind this rule set.

## Configure rate limiting

[Rate limiting for Azure Front Door](/en-us/azure/web-application-firewall/afds/waf-front-door-rate-limit) enables you to detect and block abnormally high traffic from any socket IP address. Use Azure WAF in Azure Front Door to mitigate some types of denial-of-service attacks. Rate limiting protects clients accidentally misconfigured to send large volumes of requests in a short time. You must use custom rules to [manually configure rate limiting on the WAF](/en-us/azure/web-application-firewall/afds/waf-front-door-rate-limit-configure).

## Configure detection and prevention modes

After you create a WAF policy, Azure starts the policy in **Detection mode**. Leave the WAF policy in **Detection mode** while you tune the WAF for your traffic. In **Detection mode**, the WAF doesn’t block requests. Instead, the WAF logs requests that match the WAF rules after you [enable logging](/en-us/azure/web-application-firewall/afds/waf-front-door-monitor#logs-and-diagnostics).

After you enable logging and your WAF receives request traffic, look through your logs and [tune your WAF](/en-us/azure/web-application-firewall/afds/waf-front-door-tuning).

The following query shows the requests that an example WAF policy blocked in the previous 24 hours. The details include rule name, request data, action that the policy took, and policy mode.

```kusto
AzureDiagnostics
| where TimeGenerated >= ago(24h)
| where Category == "FrontdoorWebApplicationFirewallLog"
| where action_s == "Block"
| project RuleID=ruleName_s, DetailMsg=details_msg_s, Action=action_s, Mode=policyMode_s, DetailData=details_data_s
```

| RuleID | DetailMsg | Action | Mode | DetailData |
| --- | --- | --- | --- | --- |
| DefaultRuleSet-1.0-SQLI-942430 | Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12) | Block | Detection | Matched Data: CfDJ8KQ8bY6D |

Review the WAF logs to determine if your WAF's rules caused any false positives. Then use exclusions to mitigate those WAF false positives. [Configure web application firewall exclusion lists](/en-us/azure/web-application-firewall/afds/waf-front-door-exclusion-configure). Configure [Web Application Firewall with Azure Front Door exclusion lists](/en-us/azure/web-application-firewall/afds/waf-front-door-exclusion).

After you set up logging and your WAF receives traffic, you can assess the effectiveness of your bot manager rules in handling bot traffic. The following query shows the actions that the example bot manager rule set took categorized by bot type. While in **Detection mode**, the WAF only logs bot traffic actions. After you switch to **Prevention mode**, the WAF begins actively blocking unwanted bot traffic.

```kusto
AzureDiagnostics
| where Category == "FrontDoorWebApplicationFirewallLog"
| where action_s in ("Log", "Allow", "Block", "JSChallenge", "Redirect") and ruleName_s contains "BotManager"
| extend RuleGroup = extract("Microsoft_BotManagerRuleSet-[\\d\\.]+-(.*?)-Bot\\d+", 1, ruleName_s)
| extend RuleGroupAction = strcat(RuleGroup, " - ", action_s)
| summarize Hits = count() by RuleGroupAction, bin(TimeGenerated, 30m)
| project TimeGenerated, RuleGroupAction, Hits
| render columnchart kind=stacked
```

## Switch from Detection mode to Prevention mode

To observe activity on requested traffic, select **Switch to Prevention mode** from your WAF policy's **Overview** page in the Azure portal. This selection changes the mode from **Detection mode** to **Prevention mode**. The WAF blocks requests that match the rules in WAF policy and logs them in the WAF logs. The WAF takes the prescribed action when a request matches one or more rules and logs the results. By default, the DRS sets to [anomaly scoring mode](/en-us/azure/web-application-firewall/afds/waf-front-door-drs#anomaly-scoring-mode); the WAF doesn’t take action on a request unless it meets the anomaly score threshold.

To revert to **Detection mode**, select **Switch to Detection mode** from the **Overview** page.