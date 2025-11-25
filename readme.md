# 🚀 Claude Code + Google Gemini — Complete Free Setup  
![Free Claude Code](https://img.shields.io/badge/Claude_Code-Free_Gemini-blue?style=for-the-badge&logo=anthropic)  
**Universal Guide: Windows (PowerShell + CMD), macOS, Linux**

This repository provides the **simplest and most reliable method** to run **Claude Code completely FREE** using Google Gemini API via `claude-code-router`.

✅ Works perfectly on:  
✔ Windows PowerShell  
✔ Windows CMD  
✔ macOS Terminal  
✔ Linux Bash  

All steps tested & verified as of November 2025.

⚠️ **Most Common Problem Fixed**  
Other guides use Linux-only commands like `cat << 'EOF'` or mix Bash/PowerShell syntax, which **fails on Windows**.  
This guide gives **100% correct commands for each OS separately**.

## 📌 Table of Contents
- [Step 0 — Check Node.js](#step-0--check-node.js)
- [Step 1 — Get Free Google API Key](#step-1--get-free-google-api-key)
- [Step 2 — Install Claude Tools](#step-2--install-claude-tools)
- [Step 3 — Create Required Folders](#step-3--create-required-folders)
- [Step 4 — Create config.json](#step-4--create-config.json-correct-for-each-os)
- [Step 5 — Set Google API Key](#step-5--set-google-api-key)
- [Step 6 — Verify Installation](#step-6--verify-installation)
- [Step 7 — Daily Usage](#step-7--daily-usage)
- [Troubleshooting](#troubleshooting)
- [Video Tutorial](#video-tutorial)
- [Author](#author)

---

## 🔥 STEP 0 — CHECK NODE.JS
Open terminal and run:
```bash
node --version
```
Must show v18 or higher.
If not installed → Download from:
👉 [Node.js LTS](https://nodejs.org) (LTS version recommended)

## 🔥 STEP 1 — GET YOUR FREE GOOGLE API KEY
Go to: [Google AI Studio](https://aistudio.google.com)  
Click "Get API key"  
Click "Create API key"  
Copy your key (looks like):
```
AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

## 🔥 STEP 2 — INSTALL CLAUDE TOOLS
### Windows (PowerShell or CMD):
```powershell
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```
### macOS / Linux:
```bash
sudo npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

## 🔥 STEP 3 — CREATE REQUIRED FOLDERS
### Windows PowerShell:
```powershell
New-Item -ItemType Directory -Force -Path $HOME\.claude-code-router
New-Item -ItemType Directory -Force -Path $HOME\.claude
```
### Windows CMD:
```cmd
mkdir %USERPROFILE%\.claude-code-router
mkdir %USERPROFILE%\.claude
```
### macOS / Linux:
```bash
mkdir -p ~/.claude-code-router ~/.claude
```
*`-Force` / `-p` = no error if folder already exists*

## 🔥 STEP 4 — CREATE `config.json` (Correct For Each OS)
### 🟦 Windows (PowerShell + CMD) — Use Notepad
```powershell
notepad $HOME\.claude-code-router\config.json
```
Or in CMD:
```cmd
notepad %USERPROFILE%\.claude-code-router\config.json
```
Paste this exact JSON:
```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-1.5-flash",
        "gemini-1.5-flash-exp-0827"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-1.5-flash",
    "background": "gemini,gemini-1.5-flash",
    "think": "gemini,gemini-1.5-flash",
    "longContext": "gemini,gemini-1.5-flash",
    "longContextThreshold": 60000
  }
}
```
Save & close.

### 🟩 macOS / Linux
```bash
cat > ~/.claude-code-router/config.json << 'EOF'
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-1.5-flash",
        "gemini-1.5-flash-exp-0827"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-1.5-flash",
    "background": "gemini,gemini-1.5-flash",
    "think": "gemini,gemini-1.5-flash",
    "longContext": "gemini,gemini-1.5-flash",
    "longContextThreshold": 60000
  }
}
EOF
```

## 🔥 STEP 5 — SET GOOGLE API KEY
### Windows PowerShell (Permanent):
```powershell
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'YOUR_KEY_HERE', 'User')
```
→ Restart PowerShell, then check:
```powershell
echo $env:GOOGLE_API_KEY
```

### macOS / Linux
#### Bash:
```bash
echo 'export GOOGLE_API_KEY="YOUR_KEY_HERE"' >> ~/.bashrc
source ~/.bashrc
```
#### Zsh (default on macOS):
```bash
echo 'export GOOGLE_API_KEY="YOUR_KEY_HERE"' >> ~/.zshrc
source ~/.zshrc
```

## 🔥 STEP 6 — VERIFY INSTALLATION
```bash
claude --version
ccr version
```
For macOS/Linux:
```bash
echo $GOOGLE_API_KEY
```
For Windows:
```powershell
echo $env:GOOGLE_API_KEY
```
All should show output → Ready!

## 🔥 STEP 7 — DAILY USAGE
### Terminal 1 — Start the router:
```bash
ccr start
```
Wait for:
```
✔ Service started successfully
or
⚠️ API key is not set. HOST is forced to 127.0.0.1.
Loaded JSON config from: C:\Users\User\.claude-code-router\config.json
```

### Terminal 2 — Start Coding (Cross-Platform)
#### macOS / Linux Option 1:
```bash
ccr code
```
#### macOS / Linux Option 2 (Recommended):
```bash
# Activate Claude environment
eval "$(ccr activate)"

# Start Claude CLI
claude
```

#### Windows CMD:
```cmd
set ANTHROPIC_AUTH_TOKEN=test
set ANTHROPIC_API_KEY=
set ANTHROPIC_BASE_URL=http://127.0.0.1:3456
set NO_PROXY=127.0.0.1
set DISABLE_TELEMETRY=true
set DISABLE_COST_WARNINGS=true
set API_TIMEOUT_MS=600000
```
```cmd
claude
```

#### Windows PowerShell:
```powershell
$env:ANTHROPIC_AUTH_TOKEN = "test"
$env:ANTHROPIC_API_KEY = ""
$env:ANTHROPIC_BASE_URL = "http://127.0.0.1:3456"
$env:NO_PROXY = "127.0.0.1"
$env:DISABLE_TELEMETRY = "true"
$env:DISABLE_COST_WARNINGS = "true"
$env:API_TIMEOUT_MS = "600000"
```
```powershell
claude
```
**Test it:**  
Type `hi` → Claude should reply → 🎉 Success!

---

## ⚠️ Troubleshooting
| Problem | Solution |
| :-------------------- | :---------------------------------------------------------------------- |
| `mkdir` error | Use `-Force` (Windows) or `-p` (macOS/Linux) with `New-Item` / `mkdir` |
| "API key not found" | Restart terminal after setting environment variable |
| `ccr: command not found` | Close & reopen terminal, or restart computer |
| Port 3456 already in use | Kill process: `taskkill //F //PID <pid>` (Win) or `kill -9 <pid>` (Unix) |

## 🎥 Video Tutorial
Full step-by-step video (with voice):
👉 [Watch on YouTube](https://www.youtube.com/watch?v=HQ6dqd7QY38)

## 🙌 Author
Hamid Raza
Feel free to ⭐ star this repo if it helped you!

Made with ❤️ for the community — Enjoy unlimited free Claude Code!
