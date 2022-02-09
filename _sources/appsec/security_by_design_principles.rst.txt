Security by Design Principles
=============================

Core Pillars of Information Security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Information security has relied upon the following pillars:

- **Confidentiality** – only allow access to data for which the user is permitted
- **Integrity** – ensure data is not tampered or altered by unauthorized users
- **Availability** – ensure systems and data are available to authorized users when they need it

The following principles are all related to these three pillars. Indeed, when considering how to construct a control, considering each pillar in turn will assist in producing a robust security control.

Security Principles
-------------------

These security principles have been taken from the previous edition of the OWASP Development Guide and normalized with the security principles outlined in Howard and LeBlanc’s excellent Writing Secure Code.

https://wiki.owasp.org/index.php/Security_by_Design_Principles

Minimize Attack Surface Area
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every feature that is added to an application adds a certain amount of risk to the overall application. The aim for secure development is to reduce the overall risk by reducing the attack surface area.

For example, a web application implements online help with a search function. The search function may be vulnerable to SQL injection attacks. If the help feature was limited to authorized users, the attack likelihood is reduced. If the help feature’s search function was gated through centralized data validation routines, the ability to perform SQL injection is dramatically reduced. However, if the help feature was re-written to eliminate the search function (through better user interface, for example), this almost eliminates the attack surface area, even if the help feature was available to the Internet at large.

Establish Secure Defaults
~~~~~~~~~~~~~~~~~~~~~~~~~

There are many ways to deliver an "out of the box" experience for users. However, by default, the experience should be secure, and it should be up to the user to reduce their security – if they are allowed.

For example, by default, password aging and complexity should be enabled. Users might be allowed to turn these two features off to simplify their use of the application and increase their risk.

Principle of Least Privilege
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The principle of least privilege recommends that accounts have the least amount of privilege required to perform their business processes. This encompasses user rights, resource permissions such as CPU limits, memory, network, and file system permissions.

For example, if a middleware server only requires access to the network, read access to a database table, and the ability to write to a log, this describes all the permissions that should be granted. Under no circumstances should the middleware be granted administrative privileges.

Principle of Defense in Depth
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The principle of defense in depth suggests that where one control would be reasonable, more controls that approach risks in different fashions are better. Controls, when used in depth, can make severe vulnerabilities extraordinarily difficult to exploit and thus unlikely to occur.

With secure coding, this may take the form of tier-based validation, centralized auditing controls, and requiring users to be logged on all pages.

For example, a flawed administrative interface is unlikely to be vulnerable to anonymous attack if it correctly gates access to production management networks, checks for administrative user authorization, and logs all access.

Fail Securely
~~~~~~~~~~~~~

Applications regularly fail to process transactions for many reasons. How they fail can determine if an application is secure or not.

For example::

   isAdmin = true;
   try {
     codeWhichMayFail();
     isAdmin = isUserInRole( “Administrator” );
   }
   catch (Exception ex) {
     log.write(ex.toString());
   }

If either codeWhichMayFail() or isUserInRole fails or throws an exception, the user is an admin by default. This is obviously a security risk.

Don't Trust Services
~~~~~~~~~~~~~~~~~~~~

Many organizations utilize the processing capabilities of third party partners, who more than likely have differing security policies and posture than you. It is unlikely that you can influence or control any external third party, whether they are home users or major suppliers or partners.

Therefore, implicit trust of externally run systems is not warranted. All external systems should be treated in a similar fashion.

For example, a loyalty program provider provides data that is used by Internet Banking, providing the number of reward points and a small list of potential redemption items. However, the data should be checked to ensure that it is safe to display to end users, and that the reward points are a positive number, and not improbably large.

Separation of Duties
~~~~~~~~~~~~~~~~~~~~

A key fraud control is separation of duties. For example, someone who requests a computer cannot also sign for it, nor should they directly receive the computer. This prevents the user from requesting many computers, and claiming they never arrived.

Certain roles have different levels of trust than normal users. In particular, administrators are different to normal users. In general, administrators should not be users of the application.

For example, an administrator should be able to turn the system on or off, set password policy but shouldn’t be able to log on to the storefront as a super privileged user, such as being able to “buy” goods on behalf of other users.

Avoid Security By Obscurity
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Security through obscurity is a weak security control, and nearly always fails when it is the only control. This is not to say that keeping secrets is a bad idea, it simply means that the security of key systems should not be reliant upon keeping details hidden.

For example, the security of an application should not rely upon knowledge of the source code being kept secret. The security should rely upon many other factors, including reasonable password policies, defense in depth, business transaction limits, solid network architecture, and fraud and audit controls.

A practical example is Linux. Linux’s source code is widely available, and yet when properly secured, Linux is a hardy, secure and robust operating system.

Keep Security Simple
~~~~~~~~~~~~~~~~~~~~

Attack surface area and simplicity go hand in hand. Certain software engineering fads prefer overly complex approaches to what would otherwise be relatively straightforward and simple code.

Developers should avoid the use of double negatives and complex architectures when a simpler approach would be faster and simpler.

For example, although it might be fashionable to have a slew of singleton entity beans running on a separate middleware server, it is more secure and faster to simply use global variables with an appropriate mutex mechanism to protect against race conditions.

Fix Security Issues Correctly
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once a security issue has been identified, it is important to develop a test for it, and to understand the root cause of the issue. When design patterns are used, it is likely that the security issue is widespread amongst all code bases, so developing the right fix without introducing regressions is essential.

For example, a user has found that they can see another user’s balance by adjusting their cookie. The fix seems to be relatively straightforward, but as the cookie handling code is shared among all applications, a change to just one application will trickle through to all other applications. The fix must therefore be tested on all affected applications.
