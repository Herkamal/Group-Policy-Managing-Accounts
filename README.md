<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

# Group Policy: Managing Accounts and Lockouts

This lab demonstrates how to configure an Account Lockout Policy using Group Policy, test account lockouts, reset locked accounts, disable/enable user accounts, and review related logs in both the Domain Controller and Client machines.

---

## 🧰 Technologies Used

- Microsoft Azure (Virtual Machines, Networking)
- Windows Server 2022 (Domain Controller - DC-1)
- Windows 10 Pro ( Client-1)
- Group Policy Management Console (GPMC)
- Event Viewer
- Active Directory Users and Computers (ADUC)

---

## 🎯 Objectives

- Trigger an account lockout by repeated failed login attempts  
- Configure Group Policy to lock out accounts after failed attempts  
- Unlock and reset a locked account  
- Disable and re-enable a user account  
- View related logs on both server and client systems  

---

## 🖥️ Step-by-Step Lab

### 🔐 Step 1: Configure Account Lockout Policy via GPO

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/group-lockout.png?raw=true" width="80%"/>
</p>

On **DC-1**, open the Group Policy Management Console (`gpmc.msc`) and create or edit a GPO with the following settings under:

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`

- **Account Lockout Threshold**: 5 invalid attempts  
- **Account Lockout Duration**: 30 minutes  
- **Reset Account Lockout Counter After**: 15 minutes  

---

### 🔄 Step 2: Update Group Policy on Client

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/update.png?raw=true" width="80%"/>
</p>

Run `gpupdate /force` in Command Prompt on **Client-1** to apply the new policy settings immediately.

---

### ❌ Step 3: Simulate Account Lockout

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/fail-password.png?raw=true" width="80%"/>
</p>

Log into **Client-1** and attempt to sign in with a domain user using an incorrect password **at least 6 times**. This simulates a real-world lockout event and confirms the policy is working as intended.

---

### 🔓 Step 4: Unlock the Locked Account

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/unlock.png?raw=true" width="80%"/>
</p>

In **ADUC**, locate the locked user account, right-click and choose **Unlock Account**. Optionally, reset the user’s password to something known.

---

### 🚫 Step 5: Disable the User Account

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/disable.png?raw=true" width="80%"/>
</p>

To test user suspension, right-click the user account and select **Disable Account**. Try logging in with this account — it will fail with an error indicating the account is disabled.

---

### ✅ Step 6: Re-enable the User Account

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/enable.png?raw=true" width="80%"/>
</p>

Re-enable the user account in **ADUC** and log in successfully with the correct password to confirm functionality.

---

### 📊 Step 7: Observe Security Logs

<p align="center">
  <img src="https://github.com/Herkamal/Group-Policy-Managing-Accounts/blob/main/observe.png?raw=true" width="80%"/>
</p>

Check **Event Viewer** logs on both DC-1 and Client-1 to observe events related to account lockout, logon attempts, and authentication errors.  
Look under:  
`Windows Logs > Security`

---

## ✅ Summary

In this lab, we successfully:

- Simulated and responded to account lockouts  
- Configured Group Policy for account lockout settings  
- Managed account status (lock, disable, enable)  
- Viewed real-time logs for authentication events  

These are core administrative tasks every Windows domain admin should master to maintain account security and troubleshooting efficiency.

---
