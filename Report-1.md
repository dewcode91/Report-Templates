# Unrestricted Admin Features Exposed via robots.txt

#### Description

Vertical privilege escalation occurs when an application fails to restrict access to sensitive or administrative functionality, allowing users with insufficient privileges to access powerful features. In many cases, admin interfaces are not linked in standard user navigation, but if access controls are missing, anyone who knows (or discovers) the URL can reach them.

Frequently, sensitive locations such as admin panels are inadvertently disclosed in files intended for web crawlers, like `robots.txt`. For example:

- Admin Control Panel: `https://insecure-website.com/admin`
- robots.txt location: `https://insecure-website.com/robots.txt`

When a sensitive path is present in `robots.txt`, attackers can discover it by reviewing the file's contents. Even if not listed, common wordlists allow brute-forcing such endpoints.

#### Steps to Reproduce

1. Navigate to the application and access `robots.txt` by appending `/robots.txt` to the base URL.
2. Observe the presence of a `Disallow` directive referencing the admin panel path.
3. Replace `/robots.txt` in the address bar with the disclosed admin path (e.g., `/administrator-panel`) to access the admin interface.
4. Demonstrate impact by performing privileged actions, such as deleting a user (e.g., user `carlos`).

#### Impact

Exposure of admin functionality to unauthorized users enables vertical privilege escalation. As a result, an attacker could carry out actions reserved for administrators, such as:

- Modifying or deleting sensitive system data  
- Changing configuration settings  
- Managing user accounts, including granting themselves elevated permissions  

Such access puts the application's integrity, confidentiality, and availability at significant risk.
