---
layout: post
comments: true
description: "What is static analysis of source code ?"
keywords: "static analysis, code review, pen testing"
---

### Static Analysis
Have you ever reviewed a code/program and looked for errors that could make it vulnerable. A person with malicious intensions can make use of the existing vulnerability and can cause some damage. In other curcumstances, this vulnerability might wait like a dormant volcano and can manifest by itself when favourable conditions arrive. People with bad intensions hunt for such vulnerabilities, which are the result of error prone human behavior. So, what can we ( as protectors of the realm ) can do about it ? we can find and fix these errors in the code before the code is released as part of a software for users to use. We should find these vulnerabilities faster, using automated means and fix or patch them as part of iterative releases of the software. I have mentioned some of the analysers below:


### static Analysers

Analyzer| Description | Link
--- | --- | --- 
Bandit |  find common security issues in Python code using this tool | https://github.com/PyCQA/bandit
ReDOS | Use this to find Regular Expressions susceptible to Denial of Service Attacks. | https://github.com/Wisdom/RegEx-DoS
FindBug | It helps in analysing Java code and is the trademark of University of Maryland.| http://findbugs.sourceforge.net/

I have listed only 03 of such tools because these are most useful in my work. However, if you want more nformation on other static analysers then it can be found at [Awesome Pentest resources](https://github.com/enaqx/awesome-pentest).
