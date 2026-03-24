# Web Exploitation Lab — SQL Injection (DVWA)

## Overview
This project demonstrates the exploitation of a classic web vulnerability — SQL Injection — using a deliberately vulnerable web application.

The objective was to simulate a real-world attack scenario by manipulating user input to interfere with database queries and extract unintended information.

---

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Metasploitable2
- Application: DVWA (Damn Vulnerable Web Application)
- Virtualization: VirtualBox
- Network: Host-Only Adapter

---

## Tools Used

- Web Browser (Firefox)
- DVWA
- Kali Linux
- VirtualBox

---

## Application Setup

The DVWA application was accessed through the target machine:
```
http://<TARGET_IP>/dvwa
```

Default credentials:
- Username: admin
- Password: password

Security level was set to:
- Low

---

## Vulnerability: SQL Injection

SQL Injection occurs when user input is not properly sanitized, allowing an attacker to manipulate backend database queries.

---

## Testing Input Behavior

Initial test using a valid ID:

```sql
1
```
![Normal Input](https://github.com/user-attachments/assets/f43322b9-2349-4562-bfc2-2ce0d548d8d0)

---

## Exploitation

A malicious payload was injected into the input field:
```sql
1' OR '1'='1
```

---

## Explanation

The payload modifies the original SQL query:
```sql
SELECT * FROM users WHERE id = '1'
```
Into:
```sql
SELECT * FROM users WHERE id = '1' OR '1'='1'
```
Since '1'='1' is always true, the condition bypasses the intended query logic, forcing the database to return all records.
![Sql Injection](https://github.com/user-attachments/assets/aa8cefe6-9bff-4564-97d8-005be95bdfff)

---

## Proof of Concept (PoC)

After injecting the payload, multiple user records were returned, confirming successful SQL Injection.

---

## Impact
An attacker could:

- Retrieve sensitive data from the database
- Bypass application logic
- Enumerate users and credentials
- Potentially escalate access depending on the system

---

## Mitigation
- Use prepared statements (parameterized queries)
- Validate and sanitize user input
- Implement least privilege on database accounts
- Use web application firewalls (WAF)

---

## Conclusion

This lab highlights how improper input validation can lead to critical vulnerabilities in web applications.
SQL Injection remains one of the most dangerous and common web security flaws, emphasizing the need for secure coding practices.
