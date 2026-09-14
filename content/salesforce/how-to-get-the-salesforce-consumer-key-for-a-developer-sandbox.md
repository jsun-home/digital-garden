---
title: How to Get the Salesforce Consumer Key for a Developer Sandbox
tags:
  - salesforce
---

Salesforce now favors **External Client Apps** over the older Connected Apps for new OAuth clients. Use this path unless you're maintaining an existing Connected App.

## 1. Create the External Client App

**In your sandbox**

- Log in to your Salesforce Developer Sandbox
- Click the gear icon → **Setup**
- In Quick Find, search for **External Client App Manager**
- Click **New External Client App**
- Give it a name and set **Distribution State** to `Local`

## 2. Enable OAuth settings

Still on the app creation form:

- Check **Enable OAuth Settings**
- Set a **Callback URL** (e.g. `http://localhost:8080/` for local tooling)
- Add the OAuth scopes you need, typically:
  - `Manage user data via APIs (api)`
  - `Perform requests at any time (refresh_token, offline_access)`
- Click **Create**

## 3. Authorize who can use it

Open the app's record page, click **Edit**, and go to the **Policies** tab:

- Set **Permitted Users** to `Admin approved users are pre-authorized`
- Assign the profiles or permission sets that need access

## 4. Retrieve the Consumer Key

Back on the app's detail page:

- Open the **OAuth Settings** section
- Click **Consumer Key and Secret**
- Complete the identity verification prompt (email code or MFA)
- Copy the displayed **Consumer Key**

Paste it into your `sfdx-project.json` or wherever your tooling expects it.

---

If you're working with an older **Connected App** instead, the key lives in the same place under a different label: open the app in **App Manager** → dropdown → **View** → **Manage Consumer Details**, then verify your identity to reveal the key.

## Related

- [[how-to-login-to-a-salesforce-environment-on-a-remote-machine]]
- [[configuring-external-client-app-for-cg-cloud-offline-mobile-app-modeler]] — a walkthrough of this same process for a specific use case (CG Cloud Offline Mobile App Modeler)
