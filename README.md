# 🔐 Dynamic RBAC Application Access with Microsoft Entra ID  
**(Custom App Registration + Enterprise Application Integration)**

---

## 📘 Project Overview

This project demonstrates how to design and implement **role-based access control (RBAC)** using **Microsoft Entra ID** by creating a **custom application in App registrations** and integrating it with an **Enterprise Application** for access governance.

Instead of using a gallery app, this lab simulates how IAM engineers build and secure internal applications using:

- Security groups  
- App registrations  
- Enterprise applications (service principals)  
- Token configuration (claims)  
- Group-based authorization models  

---

## 🎯 Objectives

- Create a custom Entra application using **App registrations**
- Integrate the app as an **Enterprise Application**
- Implement **group-based RBAC**
- Configure **token claims** for authorization
- Control access using **security groups**
- Validate behavior through **My Apps** testing
- Capture authentication results and troubleshooting evidence

---

## 🏗️ Architecture Summary

- **App Registration:** `ENT-RBAC-Portal`  
- **Enterprise Application:** Service principal created automatically for the app registration  
- **RBAC Groups:**
  - `ENT-HR-Users`
  - `ENT-Finance-Users`
  - `ENT-IT-Admins`
- **Redirect URI:** `https://jwt.ms`
- **Claims:** Groups claim added for token-based authorization testing

---

# 🧱 PHASE 1 — Foundation Setup

## ✅ STEP 1 — Create RBAC security groups

Path:  
Microsoft Entra ID → Groups → New group

Create:

- ENT-HR-Users  
- ENT-Finance-Users  
- ENT-IT-Admins  

Type: Security  
Membership: Assigned

📸 Screenshot: group list

<img width="770" height="557" alt="4" src="https://github.com/user-attachments/assets/547bd71b-e76b-43a2-a9be-4e33bf326cb2" />

<img width="1068" height="503" alt="5" src="https://github.com/user-attachments/assets/d49f9fd6-6dc6-44c7-94c6-b7851036757e" />

<img width="1095" height="572" alt="6" src="https://github.com/user-attachments/assets/0e501772-a298-45e4-b442-8727e01e17ab" />

---

## ✅ STEP 2 — Create and verify test users

Path:  
Microsoft Entra ID → Users → New user

Create at least:

- HR user  
- Finance user  
- IT user  

Assign each user to the matching RBAC group.

📸 Screenshot: users + group membership

---

# 🧱 PHASE 2 — Application Identity Build (App Registrations)

## ✅ STEP 3 — Create custom App Registration

Path:  
Microsoft Entra ID → App registrations → New registration

Name:  
ENT-RBAC-Portal

Supported account type:  
Accounts in this organizational directory only (Single tenant)

Click: Register

📸 Screenshot: app registration overview

---

## ✅ STEP 4 — Configure authentication (Redirect URI)

Path:  
App registrations → ENT-RBAC-Portal → Authentication

Add a platform: Web

Add Redirect URI:

https://jwt.ms

Save.

📸 Screenshot: Authentication page showing jwt.ms

---

## ✅ STEP 5 — Configure token claims (Groups)

Path:  
App registrations → ENT-RBAC-Portal → Token configuration

Add optional claim:

- Groups
- Token type: ID token
- Emit: Security groups

Save.

📸 Screenshot: Token configuration showing groups claim

---

# 🧱 PHASE 3 — Enterprise Application Integration (Access Control)

## ✅ STEP 6 — Assign RBAC groups to the Enterprise Application

Path:  
Microsoft Entra ID → Enterprise applications → ENT-RBAC-Portal → Users and groups

Assign:

- ENT-HR-Users  
- ENT-Finance-Users  
- ENT-IT-Admins  

This controls who can see and launch the app in **My Apps**.

📸 Screenshot: group assignments inside the enterprise app

---

# 🧱 PHASE 4 — Access Validation (My Apps)

## ✅ STEP 7 — Test access using My Apps

Open Incognito / Private window.

Go to:  
https://myapps.microsoft.com

Test logins:

- HR user → launch ENT-RBAC-Portal  
- Finance user → launch ENT-RBAC-Portal  
- IT user → launch ENT-RBAC-Portal  

Capture the results (success or failure screens) and correlation IDs if present.

📸 Screenshot: My Apps portal showing ENT-RBAC-Portal  
📸 Screenshot: launch attempt result page

---

# 🧱 PHASE 5 — Monitoring & Troubleshooting Evidence

## ✅ STEP 8 — Review sign-in logs

Path:  
Microsoft Entra ID → Monitoring → Sign-in logs

Filter:

- Application: ENT-RBAC-Portal
- User: (HR/Finance/IT)

Open an event and review:

- Status / Failure reason  
- Conditional Access tab  
- Authentication details  
- Correlation ID + timestamp  

📸 Screenshot: Sign-in log details

---

## ✅ STEP 9 — Review audit logs (optional)

Path:  
Microsoft Entra ID → Monitoring → Audit logs

Filter:

- Activity related to group membership changes
- App assignment changes (if applicable)

📸 Screenshot: audit log events

---

# 📊 Skills Demonstrated

- Microsoft Entra ID (Azure AD)
- App registrations (OIDC identity object)
- Enterprise applications (service principal access control)
- Group-based RBAC design
- Token claims configuration (groups claim)
- My Apps access validation
- Sign-in log troubleshooting using correlation IDs
