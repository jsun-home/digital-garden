---
title: How to Log In to a Salesforce Environment on a Remote VPS
---

To authenticate a VPS without a browser:

- Authorize the sandbox on your local machine
- Export the session URL
- Import it into your VPS

## 1. Authenticate locally

**On your laptop**

Run the web login command for your sandbox. This will open your local browser to log in:

```bash
sf org login web --instance-url https://test.salesforce.com --alias my-sandbox
```

## 2. Export the Auth URL

**On your laptop**

Export the connection details to a JSON file:

```bash
sf org display --target-org my-sandbox --verbose --json > auth.json
```

Open `auth.json` and copy the long string next to the `"sfdxAuthUrl"` key. It will look like `force://PlatformCLI...`.

## 3. Create the auth file

**On your remote VPS**

Create a new text file to hold the URL:

```bash
nano auth-url.txt
```

Paste the entire `force://...` string into this file, save, and exit.

## 4. Import to the VPS CLI

**On your remote VPS**

Log in using the URL file you just created:

```bash
sf org login sfdx-url --sfdx-url-file auth-url.txt --alias my-sandbox --set-default
```

## 5. Clean up

**Security best practice**

Delete the text file from your VPS so your active authentication token isn't left lying around:

```bash
rm auth-url.txt
```

To verify the connection was successful, run `sf org list` on your VPS to ensure `my-sandbox` shows up as connected.
