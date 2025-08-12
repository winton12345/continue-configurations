# Configure Continue + AWS Credentials

This guide explains:
1. How to locate and edit the **Continue** extension’s configuration file (`config.yaml`).
2. How to manually create AWS credential files (without installing the AWS CLI).

---

## 1. Locate the `.continue` folder (Continue configuration)

Continue stores its global settings inside a hidden folder named `.continue` in your **user directory**.

### Steps to find it:
1. Open your **File Explorer** (Finder on macOS, File Explorer on Windows).
2. Navigate to your **user folder**:
   - **Windows:** `C:\Users\<YourUsername>\`
   - **macOS / Linux:** `/Users/<YourUsername>/`
3. Enable **"Show Hidden Files"** if the `.continue` folder is not visible.
4. Inside `.continue`, you should see a file named: `config.yaml`.

## 2. Edit `config.yaml`

1. Open `config.yaml` in VS Code or any text editor.
2. Adjust the settings according to your needs — this is where you control Continue’s behavior and integrations.
3. Save the file after making changes.
4. **Restart VS Code** or reload the window (`Ctrl+Shift+P` → “Reload Window”) so Continue applies the updated configuration.


Open `config.yaml` in VS Code and paste the **entire** example below.

> This config uses AWS Bedrock for LLaMA 3 (Meta 70B) and Claude 3.7 Sonnet, and enables common context providers.

```yaml
name: Local Assistant
version: 1.0.0
schema: v1

models:
  - name: LLaMA 3 (Meta 70B Instruct)
    provider: bedrock
    model: meta.llama3-70b-instruct-v1:0
    env:
      region: us-gov-west-1
      profile: bedrock
    defaultCompletionOptions:
      maxTokens: 1024
    roles:
      - chat
      - edit
      - apply

  - name: Claude 3.7 Sonnet (Anthropic)
    provider: bedrock
    model: anthropic.claude-3-7-sonnet-20250219-v1:0
    env:
      region: us-gov-west-1
      profile: bedrock
    defaultCompletionOptions:
      maxTokens: 4096
    roles:
      - chat
      - edit
      - apply

context:
  - provider: file
  - provider: code
  - provider: codebase
    params:
      nFinal: 10
  - provider: docs
  - provider: diff
  - provider: folder
  - provider: terminal
```




# AWS Credentials Setup (No AWS CLI Required)

Follow these steps to configure AWS credentials for use with Continue or any tool that needs AWS authentication.

---

## 1) Create AWS credentials in your user directory

### windows
1. Open your **File Explorer** (Finder on macOS, File Explorer on Windows).
2. Navigate to your **user folder**:
   - **Windows:** `C:\Users\<YourUsername>\`
   - **macOS / Linux:** `/Users/<YourUsername>/`
3. Create a new folder called .aws and within that folder you create a new file called credentials.
4. Open the credentials file with a text editor (e.g., Notepad on Windows, TextEdit on macOS).
5. Add the following content to the credentials file:

[bedrock]
aws_access_key_id = "your own credentials"
aws_secret_access_key = "your own credentials"
region = us-gov-west-1


2) if you already have the aws cli installed simply edit the credentials file in the .aws folder.


AWS issues and bugs:

1) if your credentials arent reading make sure to take the .txt out of the name of the  file 
