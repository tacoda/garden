SAST and Code Review for SecDevOps
==================================

Introduction
------------

An application is only as secure as the source code it's built on. That's the philosophy behind Static Application Security Testing (SAST),
which allows security engineers to identify threats to their apps at the source code level. This is the heart of Continuous Application Security,
and it's what this course is all about. In this program, we'll be going over some of the most common SAST tools, including methods of automating
security tooling in a CI/CD pipeline. You'll spend time rolling out SAST workflows and actually 'building' security pipelines that can be
integrated into an organisation's DevOps process. Our hands-on labs will even walk you through methods to perform SAST incrementally to boost
the efficiency of security testing in your software development lifecycle. This course is designed to teach you everything you need to know about
static application security and how it ties into a sustainable DevOps practice. Our material is backed by years of security testing experience,
knowledge, and original research across our entire team. That's why we've chosen to focus on showing you practical, real-world strategies and
techniques that bring you closer to a successful DevSecOps implementation.

Pre-Commit and Commit-Time Security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Developer environment
- Commits to repository
- Continuous integration

Essential Static Analysis
-------------------------

SAST Types and Tools
~~~~~~~~~~~~~~~~~~~~

SAST test approaches:

- Regular expressions
- Abstract syntax trees
- Semantic grep or QL

SAST - Regex and AST
~~~~~~~~~~~~~~~~~~~~

Regex
+++++

- Regular expressions are useful in identifying patterns
- Can be inaccurate because they don't understand context
- Heavily dependent on the quality of regex rules

Susceptible to false positives.

AST
+++

Abstract syntax tree

Source code >> Model extraction >> Intermediate representations >> Analysis >> Results

Very accurate but your knowledge of the syntax must be complete.

- New rules can be written into SAST or Linter/Code Quality tool
- Very fast, especially if using a Linter/Code Quality tool, rather than a full-featured SAST tool
- Can be embedded into the IDE for immediate feedback loops to the developer

Lab: SAST with Bandit
~~~~~~~~~~~~~~~~~~~~~

Bandit
++++++

Bandit is a python-only tool.

Instructions
^^^^^^^^^^^^

- Step 1: Run Bandit on the ``DvFaaS`` Project and observe the results

  ::

   bandit -r -f screen /root/DVFaaS-Damn-Vulnerable-Functions-as-a-Service/Copy

- Step 2: Generate a ``.json`` report

  ::

   bandit -r -f json -o bandit_result.json /root/DVFaaS-Damn-Vulnerable-Functions-as-a-Service/Copy

- Step 3: On the IDE, go to ``/root/DVFaaS-Damn-Vulnerable-Functions-as-a-Service/`` and check the result file.

References
^^^^^^^^^^

- https://github.com/PyCQA/bandit

Good Rules for SAST
~~~~~~~~~~~~~~~~~~~

- Every check should do only one thing
- False positives abound when complexity increases
- Extending SAST with custom checks is a good idea (if you know what you're doing)
- Getting engineering teams to extend SAST should be the ultimate objective
- Custom SAST rules become necessary as you are scaling up in SAST maturity
- Custom SAST rules help identify specific cases that make sense to your applications, in terms of security
- Increases depth of your overall SAST process
- Leveraging AST is better for SAST, as it makes it more accurate

