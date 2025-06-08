## Vulnerability Summary

A critical **Stored Cross-Site Scripting (XSS)** vulnerability was discovered in the stores section of **Food Ordering System in PHP CodeIgniter**.  
Attackers can inject malicious JavaScript via the `patname` field (POST parameter), which gets persistently stored in the database and executed whenever the page is viewed.

### Key Details

| Property            | Value                                                                 |
|---------------------|-----------------------------------------------------------------------|
| **Affected Vendor** | CodeIgniter                                                             |
| **Vulnerable Section** | `Stores And Restaurants`                                                   |
| **Attack Vector**   | `Store Name And Adderess` parameter via POST request                                 |
| **Vulnerability**   | Stored Cross-Site Scripting (XSS)                                     |
| **Version Affected Released Date**| May 18, 2021                                                                |
| **Official Website**| https://codeastro.com/food-ordering-system-in-php-codeigniter-with-source-code/ |

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
## <script>alert(1)</script>
![image](https://github.com/user-attachments/assets/898c693e-fdc2-4e37-a4e2-dad0349e28f3)


### Trigger the Payload

Reload the stored page. You’ll see a JavaScript alert(1) triggered — confirming the stored XSS vulnerability. Also whenever a adminn logins in the dashboard payload will be triggered and if admin navigates through dashboard payloads get's triggered again which confirms the stored Xss.
![image](https://github.com/user-attachments/assets/bf9a82d5-9fe1-4204-8e16-5a9f3e71e314)

![image](https://github.com/user-attachments/assets/6b718c1d-e8b8-4d57-b009-3fc33fd18ef8)

![image](https://github.com/user-attachments/assets/0df022bd-1dab-43c1-823d-201e2ebbc0e3)

This also affects the user side as if anyone tries to open Restaurants xss will be reflected:
http://localhost/foodienator/restaurant/index

![image](https://github.com/user-attachments/assets/b294e4ad-dfa3-48ac-a192-f08f5033a928)


## 🛑 Potential Impact

- **Session Hijacking**: Steal user/admin session cookies via `document.cookie`.
- **Phishing**: Inject fake forms to harvest credentials.
- **Defacement**: Alter webpage content, defame the brand.
- **Data Exfiltration**: Steal sensitive data through background requests.
- **Malware Propagation**: Redirect users to malicious domains.
- **Privilege Escalation**: Gain access to higher-privilege accounts by exploiting stored scripts.

---

## ✅ Mitigation Strategies

### 🔒 Input Sanitization

Sanitize all user inputs on the server side using functions like `htmlspecialchars()` in PHP.

### 🧹 Output Encoding

Encode output before rendering dynamic content:

```php
echo htmlentities($user_input, ENT_QUOTES, 'UTF-8');


  Author: Subhash Paudel And Vansh Dhawan
  Date: 2025-06-08
  Severity: High
