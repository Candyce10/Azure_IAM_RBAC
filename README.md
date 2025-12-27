# Cloud IAM Lab: Azure RBAC & Identity Management

## Overview
This lab demonstrates hands-on implementation of cloud Identity and Access Management (IAM) using Microsoft Azure and Microsoft Entra ID. The focus is on group-based RBAC, least privilege, and access validation across different user roles.

The lab simulates a small organization with specific user roles and validates access behavior using real Azure resources.

<br>



## Architecture & Identity Model
The identity layer was implemented using Microsoft Entra ID, with users and security groups representing organizational roles.

### Identities Created
- HR user (read-only access)
- Finance user (read-only access)
- IT admin user (resource management)

### Security Groups
- Cloud-HR-Read  
- Cloud-Finance-Read  
- Cloud-IT-Admin  

All access is granted via groups, not directly to users, following IAM best practices.

<br>
<img width="1920" height="923" alt="Entra ID Users" src="https://github.com/user-attachments/assets/7fc0eead-696e-4b6d-acd9-3b32e61ece9b" />
<img width="1920" height="930" alt="Entra ID Groups" src="https://github.com/user-attachments/assets/62509fd8-18c6-4a9a-aed1-3cea2aae4bd3" />

<br>



## Azure RBAC Design
Authorization is enforced using Azure Role-Based Access Control (RBAC) at the resource level.

### Resource Used
- Azure Storage Account  
- Scope: This resource only (not subscription-wide)

### RBAC Assignments
- Reader → Cloud-HR-Read  
- Storage Blob Data Reader → Cloud-HR-Read  
- Contributor → Cloud-IT-Admin  

This design separates:
- Management-plane access (Reader / Contributor)
- Data-plane access (Storage Blob Data Reader)

<br>
<img width="1863" height="848" alt="IAM Role Assignments" src="https://github.com/user-attachments/assets/4969f2a5-aa9d-4a13-b0cf-343552e6a324" />

<br>



## 👤 Access Validation & Least Privilege
Access was validated by signing in as different users and confirming expected behavior.

### HR User (hr.cloud)
- Can view the storage account
- Cannot modify settings
- Cannot assign roles
- Cannot perform administrative actions

This confirms read-only access and least-privilege enforcement.

<br>
<img width="1920" height="920" alt="storage account visible by HR" src="https://github.com/user-attachments/assets/c88c5bfe-be07-44bc-afd3-0e87eadc80b0" />

<img width="1920" height="938" alt="disabled IAM in HR account" src="https://github.com/user-attachments/assets/921b4cd0-75a9-4cca-bbf3-a275b223e3ca" />


<br>



### IT Admin User (it.admin)
- Can manage storage account configuration
- Cannot modify RBAC role assignments
- Restricted from identity security policy management

This enforces separation of duties between resource administrators and access administrators.

<br>
<img width="1918" height="922" alt="IT account contributor" src="https://github.com/user-attachments/assets/7f56ff87-4cbf-4be0-9eef-ac4602174738" />


<br>



## IAM Concepts Demonstrated
- Cloud identity management using Microsoft Entra ID  
- Group-based access control (RBAC)  
- Least privilege enforcement  
- Management-plane vs data-plane permissions  
- Separation of duties between roles  
- Access validation using non-admin accounts  

<br>



## Lessons Learned
- Azure RBAC role assignment requires elevated permissions (Owner/User Access Administrator)
- Contributor role does not allow access control changes
- Data-plane roles do not grant visibility in the Azure portal without management-plane roles
- Access must always be validated from the user’s perspective

<br>



## Next Steps
- Extend lab with IAM governance (access reviews)
- Implement AWS IAM for cross-cloud comparison
- Explore Conditional Access when licensing permits

<br>



**Author:**  
Built as part of hands-on Cloud IAM skill development.
