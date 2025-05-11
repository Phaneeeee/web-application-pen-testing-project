# Cybersecurity Project: Network Reconnaissance and Web Application Testing

## 🎯 Objective
The goal of this project is to demonstrate basic cybersecurity testing by performing network reconnaissance and testing for common web application vulnerabilities. Tools like **Nmap** and **Burp Suite** were used on a deliberately vulnerable web application (**DVWA**) to simulate real-world ethical hacking techniques.

---

## 🧰 Tools Used
- **Nmap** – For scanning networks, discovering open ports, services, and OS information  
- **Burp Suite Community Edition** – Used to intercept and modify HTTP requests  
- **DVWA (Damn Vulnerable Web Application)** – A training platform for web vulnerabilities  
- **XAMPP** – Local server stack used to host DVWA  
- **Google Chrome** – Browser configured to work with Burp Proxy  

---

## 🛠️ Steps Performed

### 1. Environment Setup
- Installed and configured **XAMPP** to run DVWA on `localhost`
- Launched **Burp Suite**, set up browser proxy, and configured Burp CA certificate
- Temporarily disabled system and browser protections to allow traffic interception

### 2. Network Scanning with Nmap
- Executed the following scan:
  ```bash
  nmap -sS -sV -O 127.0.0.1
  ```
- Results:
  - Open Ports Detected: `80`, `135`, `443`, `445`, `2869`, `3306`, `8080`
  - Operating System: Microsoft Windows 10
  - Port 8080 returned Burp Suite's web interface but was marked as "unrecognized" — indicating that Nmap couldn't match the fingerprint exactly

### 3. Web Application Testing

#### ✅ Burp Suite
- Captured and analyzed HTTP traffic between DVWA and browser using the **HTTP History** tab

#### 🔐 XSS Test
- Injected script:
  ```html
  <script>alert("Hacked")</script>
  ```
- No popup appeared at first due to input sanitization at higher DVWA security levels  
- After setting DVWA security to **Low**, the alert popup was displayed — confirming an XSS vulnerability

#### 🛡️ SQL Injection
- Injected payload:
  ```sql
  ' OR 1=1 --
  ```
- DVWA returned an **Uncaught mysqli_sql_exception** error — confirming improper input sanitization and a potential SQL injection vulnerability

---

## 📸 Screenshots
- DVWA login/dashboard interface
- Burp Suite HTTP Interception interface
- Nmap terminal output (aggressive scan)
- XSS test field and popup
- SQL Injection error screen

---

## 📊 Key Findings
- **Multiple open ports** were discovered during the Nmap scan
- **SQL Injection vulnerability** caused raw SQL error responses
- **XSS was partially mitigated** at higher security levels, but exploitable at lower settings
- **Server error messages** exposed backend logic and database details

---

## ✅ Conclusion
This project illustrates how ethical hacking techniques can reveal weak points in web applications and servers. It highlights the importance of:
- Proper input validation
- Error handling
- Avoiding default configurations

---

## 📤 How to Run This Project
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/cybersecurity-project.git
   ```
2. Open `README.md` for detailed instructions
3. Follow the setup steps using DVWA, Nmap, and Burp Suite

---

## 🛡️ Recommendations
- Do not test live systems without explicit permission
- Follow responsible disclosure practices
- Re-enable protections and reset browser settings after testing
