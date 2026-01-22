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
Membership: Dynamic users

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

<img width="1362" height="613" alt="1" src="https://github.com/user-attachments/assets/e9f3a57a-e94e-4196-8304-a49a8b0a93a4" />

<img width="1358" height="614" alt="2" src="https://github.com/user-attachments/assets/798ba769-02a3-44b9-88f2-1ca7f7ac664b" />

<img width="1365" height="618" alt="3" src="https://github.com/user-attachments/assets/256edb24-f20c-4027-aade-a51ffd899be9" />

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

<img width="1330" height="184" alt="10" src="https://github.com/user-attachments/assets/82bfc06e-7389-404b-867c-86cca58e1f98" />

<img width="1083" height="567" alt="11" src="https://github.com/user-attachments/assets/f7fadb76-f1fc-4c2a-876d-0e28fbe4bed9" />

<img width="1089" height="568" alt="12" src="https://github.com/user-attachments/assets/386eee0f-1482-4f21-b98d-ce47b04d3134" />

<img width="606" height="577" alt="13" src="https://github.com/user-attachments/assets/95eaffbf-b958-43a0-9c4d-280464c8ec08" />

<img width="590" height="567" alt="14" src="https://github.com/user-attachments/assets/046a3171-564a-463b-8c34-45abfdf09135" />

<img width="586" height="565" alt="15" src="https://github.com/user-attachments/assets/7a732870-3382-4c96-a13a-06d5267fa28d" />

<img width="583" height="558" alt="16" src="https://github.com/user-attachments/assets/d1627907-1e18-41a1-b566-c75e91c74268" />

<img width="1091" height="559" alt="17" src="https://github.com/user-attachments/assets/58d27c2c-6452-4999-bf1c-655738125da2" />

---

## ✅ STEP 4 — Configure authentication (Redirect URI)

Path:  
App registrations → ENT-RBAC-Portal → Authentication

Add a platform: Web

Add Redirect URI:

https://jwt.ms

Save.

📸 Screenshot: Authentication page showing jwt.ms

<img width="1107" height="581" alt="18" src="https://github.com/user-attachments/assets/d6e19680-ddaf-43d5-8c07-b6f192b31add" />

<img width="1085" height="575" alt="19" src="https://github.com/user-attachments/assets/421fac85-aeff-4d04-9da0-854c64706c27" />

<img width="1092" height="560" alt="20" src="https://github.com/user-attachments/assets/e3cd48b7-9cca-40f9-816c-d5fcc05261a0" />

<img width="1085" height="578" alt="21" src="https://github.com/user-attachments/assets/b1d71849-c00f-41dd-8902-21466a704e37" />

<img width="1093" height="578" alt="22" src="https://github.com/user-attachments/assets/e4210a88-c674-4cee-ad39-6cff7358e1bc" />

<img width="1083" height="563" alt="23" src="https://github.com/user-attachments/assets/12b78b6e-a37a-4dbd-8bd3-551d6ff33f35" />

<img width="1087" height="570" alt="24" src="https://github.com/user-attachments/assets/75764fa1-813f-41a9-9a4b-0610c4738f87" />

<img width="1081" height="565" alt="25" src="https://github.com/user-attachments/assets/cb14cfc4-2583-4cee-83a5-e0591385bc79" />

<img width="589" height="568" alt="Screenshot 2026-01-21 223005" src="https://github.com/user-attachments/assets/fb38d010-bb1b-47fa-8d96-2a1499e710aa" />

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

<img width="1091" height="581" alt="26" src="https://github.com/user-attachments/assets/56a26be5-69f1-498c-a22b-73c618c43ba2" />

<img width="1077" height="558" alt="27" src="https://github.com/user-attachments/assets/5df80137-5349-457d-96df-7243df5fcd80" />

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

<img width="1080" height="571" alt="31" src="https://github.com/user-attachments/assets/f7519cf6-0c5f-4655-81a2-a557dbf3ff49" />

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

<img width="523" height="393" alt="28" src="https://github.com/user-attachments/assets/07534330-9fb3-42e9-9c19-2d6f8294515a" />

<img width="1358" height="609" alt="29" src="https://github.com/user-attachments/assets/c871bc97-7d1a-4b8b-ba00-74f526a60581" />

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

<img width="1087" height="575" alt="30" src="https://github.com/user-attachments/assets/07627328-e826-4df5-80a2-40d6e90fbb8c" />

---

# 📊 Skills Demonstrated

- Microsoft Entra ID (Azure AD)
- App registrations (OIDC identity object)
- Enterprise applications (service principal access control)
- Group-based RBAC design
- Token claims configuration (groups claim)
- My Apps access validation
- Sign-in log troubleshooting using correlation IDs
