---
title: Configuring an External Client App for the CG Cloud Offline Mobile App Modeler
tags:
  - salesforce
---

To configure your local environment for the Consumer Goods (CG) Cloud Offline Mobile App Modeler in VS Code, you should set up an External Client App. While older tutorials reference Connected Apps, Salesforce restricts new Connected App creation in favor of External Client Apps. You need to enable the OAuth Web Server Flow or User-Agent Flow so the CG Cloud Simulator application can properly authenticate your sandbox user credentials during design contract development.

## 1. Create the External Client App

**In your sandbox**

- Log in to your Salesforce Developer Sandbox
- Click the gear icon → **Setup**
- In Quick Find, search for **App Manager**
- Click **New External Client App**
- Set **External Client App Name** to `CG Cloud Modeler` (or similar)
- Set **Distribution State** to `Local`

## 2. Configure OAuth settings for the Modeler

- Scroll to the **API (Enable OAuth Settings)** section and check **Enable OAuth Settings**
- Set **Callback URL** to `http://localhost:8080/` (or the local simulator port from your CG Cloud setup guides)
- Under **Available OAuth Scopes**, add:
  - `Access the identity URL service (id, profile, email, address, phone)`
  - `Manage user data via APIs (api)`
  - `Manage user data via Web browsers (web)`
  - `Perform requests at any time (refresh_token, offline_access)`
- Under **Security**, uncheck **Require Secret for Web Server Flow** if your local simulator framework needs a public-client/secretless flow
- Click **Create**

## 3. Authorize the app's policies

- Open the app's record page and click **Edit**
- Go to the **Policies** tab
- Under **OAuth Policies**, set **Permitted Users** to `Admin approved users are pre-authorized`
- Under **Profiles** or **Permission Sets**, assign your System Administrator profile or your CG Cloud development permission sets — this avoids "User authentication failed" errors during local simulation

## 4. Retrieve your Consumer Key

- Go back to the app's detail page and open the **OAuth Settings** block
- Click **Consumer Key and Secret**
- Complete the MFA or email verification prompt
- Copy the Consumer Key and paste it into your local `sfdx-project.json` or your CG Cloud Modeler configuration in VS Code

## Related

- [[how-to-get-the-salesforce-consumer-key-for-a-developer-sandbox]] — the general version of this process
- [[how-to-login-to-a-salesforce-environment-on-a-remote-machine]]
