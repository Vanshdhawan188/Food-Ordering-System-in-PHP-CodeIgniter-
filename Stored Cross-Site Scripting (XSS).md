## Vulnerability Summary

A critical **Stored Cross-Site Scripting (XSS)** vulnerability was discovered in the `edit-patient.php` file of **PHPGurukul's Hospital Management System (v4.0)**.  
Attackers can inject malicious JavaScript via the `patname` field (POST parameter), which gets persistently stored in the database and executed whenever the profile page is viewed.

### Key Details

| Property            | Value                                                                 |
|---------------------|-----------------------------------------------------------------------|
| **Affected Vendor** | PHPGurukul                                                            |
| **Vulnerable File** | `edit-patient.php`                                                   |
| **Attack Vector**   | `patname` parameter via POST request                                 |
| **Vulnerability**   | Stored Cross-Site Scripting (XSS)                                     |
| **Version Affected**| v4.0                                                                 |
| **Official Website**| [Hospital Management System](https://phpgurukul.com/hospital-management-system-in-php/) |

## Proof of Concept (PoC)
### Step-by-Step Exploitation

### Login to the Foodinator Admin Panel
Navigate to the login portal and authenticate using valid credentials.

http://localhost/foodienator/admin/login/index
![image](https://github.com/user-attachments/assets/db0dd4f0-cd63-4698-b3a0-2a220467c06e)

### Inject XSS Payload in Name Field

Go to Store (select any Store) → edit.
![image](https://github.com/user-attachments/assets/b8cc0652-5bd0-4ffa-aa1b-2bb1748f4b16)

Paste the following payload in the "Address" and "Name" input field and click Update:
<script>alert(1)</script>
![image](https://github.com/user-attachments/assets/898c693e-fdc2-4e37-a4e2-dad0349e28f3)


### Trigger the Payload

Reload the stored page. You’ll see a JavaScript alert(1) triggered — confirming the stored XSS vulnerability. Also whenever a adminn logins in the dashboard payload will be triggered and if admin navigates through dashboard payloads get's triggered again which confirms the stored Xss.
![image](https://github.com/user-attachments/assets/bf9a82d5-9fe1-4204-8e16-5a9f3e71e314)

![image](https://github.com/user-attachments/assets/6b718c1d-e8b8-4d57-b009-3fc33fd18ef8)

