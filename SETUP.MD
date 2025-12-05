# ✅ How to Set Up Git with SSH on Windows

This guide will help you configure SSH keys for GitHub so you can push and pull code securely without entering your password every time.

***

## **1. Check if Git and OpenSSH are Installed**

Open **PowerShell** and run:

```powershell
git --version
ssh -V
```

If Git or SSH is not installed:

*   Download Git: <https://git-scm.com/downloads>
*   SSH comes with Windows 10/11 by default.

***

## **2. Enable and Start SSH Agent**

Run these commands in **Command Prompt (Admin)**:

```cmd
sc config ssh-agent start= auto
net start ssh-agent
```

✅ This ensures the SSH agent starts automatically.

***

## **3. Generate SSH Key**

In **PowerShell**, run:

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

*   Press **Enter** to accept default location (`C:\Users\<YourUser>\.ssh\id_ed25519`).
*   Set a passphrase (optional).

***

## **4. Add SSH Key to Agent**

Run:

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

***

## **5. Copy Public Key**

Run:

```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub
```

Copy the entire line starting with `ssh-ed25519`.

***

## **6. Add Key to GitHub**

*   Go to GitHub → Settings → SSH and GPG keys
*   Click **New SSH key**.
*   Paste the key.
*   Save.

***

## **7. Test SSH Connection**

Run:

```powershell
ssh -T git@github.com
```

Expected output:

    Hi <your-username>! You've successfully authenticated.

***

## **8. Configure Git Remote**

Inside your project folder:

```powershell
git remote add origin git@github.com:<username>/<repo>.git
git remote -v
```

***

## **9. Push Your Code**

```powershell
git push -u origin main
```

***
