# SQL Injection Vulnerability Discovery at PT Parna Raya

This repository documents the discovery of an **SQL Injection** vulnerability on the website **[https://www.parnaraya.co.id/en/newsdet.php](https://www.parnaraya.co.id/en/newsdet.php)**.

## Tools Used:

* **Hackbar Extension**: Used to manipulate request parameters and identify vulnerabilities.
* **Google Dorking**: Used for searching vulnerable parameters that might be susceptible to SQL injection.

## Vulnerability Description:

An **SQL Injection** vulnerability was found by manipulating the parameters in the **GET request** to **[https://www.parnaraya.co.id/en/newsdet.php?id=58](https://www.parnaraya.co.id/en/newsdet.php?id=58)**. By injecting a **payload** into the **id** parameter, we were able to bypass the **Web Application Firewall (WAF)** and access sensitive data in the database.

### Exploit:

The **SQL Injection** allowed us to retrieve information from the database, including table names and column names. In the example below, we successfully retrieved data from two databases: **edm_about** and **edm_admin**.

#### Payload Example:

```sql
' UNION SELECT 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24--
```

#### Screenshot of Exploit:

![SQL Injection Screenshot](images/BUG_PT_Parna_Raya.png)

### Retrieved Data:

* **Database**: k4157206_dbprg
* **Tables**: edm_about, edm_admin
* **Columns**: id, tglmasuk, bsa, tsm, status, password, fullname, and others.

## Steps to Reproduce:

1. Visit **[https://www.parnaraya.co.id/en/newsdet.php?id=58](https://www.parnaraya.co.id/en/newsdet.php?id=58)**.
2. Modify the **id** parameter using **Hackbar extension** to inject the **SQL payload**.
3. The server will return the database contents, allowing unauthorized access to sensitive data.

## Mitigation Recommendations:

* Implement **parameterized queries** or **prepared statements** to prevent SQL Injection attacks.
* Use **input validation** to ensure user input does not interfere with SQL queries.
* Apply proper **WAF** configurations to block common **SQL Injection** payloads.

## License:

This project is intended for **educational purposes** and **ethical hacking** only. Always ensure that any security testing is conducted responsibly and with proper authorization.
