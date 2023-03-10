# Red Team Hiring Process

Red Teaming is a skill that, in many cases, requires you to know about multiple technical domains. Because Red Teaming requires many areas of technical expertise, it can lead to being asked a wide range of questions during an interview process. Additionally, it's essential to understand that many roles exist on a Red Team, including Operator, Infrastructure, Tool developer, C2 developer, exploit developer, and many others. Meeting Red Teamers with Developer or Operations (System Administrator) backgrounds is also common. With all that said, below is a list of questions and hands-on exercises I've experienced during the Red Team interview process.

## Hands-on exercises

It is always possible that you will be required to do hands-on challenges during an interview process.

Here is a list of challenges I've faced during the interview process:

* Review C code and discover the vulnerability 
* Illustrate the stack required to exploit the previously mentioned vulnerability in C code
* Discover the vulnerability in a web lab environment and achieve RCE on the machine
* Exploit a staging website (owned by the company) that currently has an unresolved vulnerability
* Port scan a lab environment and provide dialogue on how I would prioritize and discover an initial foothold
* Perform testing on a web application and discover as many vulnerabilities as possible, exploit if possible


## Red Team Interview Questions

The following list contains the most common questions I've encountered during an interview. These questions will only prepare someone who has done the work to be ready for a Red Team interview. The intention is to assess readiness and identify gaps in knowledge. Your answers may vary depending on your experience and the question asked. Because of this, I'll give details about what to expect instead of the exact answer to the questions.


### What is the difference between Penetration Testing and Red Teaming?

A few key points define the difference.

Penetration Test:
* Defined scope
* Defined duration
* Result is a list of vulnerabilities

Red Team:
* Limited or no restriction on the scope
* Chaining exploits together for business impact
* Results in a report that describe the entire engagement and outcomes
* A predefined business impact may be agreed upon, e.g., reach this database and dump customer records

These points are a good starting point, but be prepared to answer this question in more detail to give the interviewer confidence that you understand the role.

### Explain how you would start a Red Team engagement if given only the company name

This question can present itself in many variations, but the idea is that the interviewer is trying to determine your methodology for starting a Red Team engagement. A typical answer would likely involve data sources you use to collect company information and reconnaissance you perform to start identifying assets.

### In the interviewer's scenario, how would you gain an initial foothold inside a target?

After you answer the previous question, the interviewer will likely ask you for more detailed information. In the past, the question involved giving details about how I would perform a targeted spear phishing scenario or crack the perimeter to gain access.

### What is a TTP

TTP stands for Tactics, Techniques, and Procedures. The following article describes them far better than I can in a short response.

* [What's in a name? TTPs in Info Sec](https://posts.specterops.io/whats-in-a-name-ttps-in-info-sec-14f24480ddcc)


### What is the difference between Adversary Emulation and Attack Simulation?

Adversary Emulation is when you emulate the TTPs of an existing group. Typically an attack has already taken place, and the details of that attack are known and are used to mimic the attack. This approach can gauge an organization's readiness to detect and disrupt a similar attack. Attack simulation typically refers to creating a simulated attack using any means when one has not taken place to emulate. The following post is called [What's in a name? Thoughts on Red Team nomenclature](https://blog.nviso.eu/2020/01/23/thoughts-on-red-team-nomenclature/) and explains this in more detail.

### If given an assumed compromise foothold in an organization, how would you begin testing?

It is a common scenario to be provided an assumed compromise foothold in a company as a starting point for a Red Team engagement. Typically this approach is used when the customer wants you to focus your time on the impact an attacker would have inside their network. Describing how you would begin to gain situational awareness and achieve your goals is a common question asked during a Red Team interview.

### What is your area of expertise?

When asked about your expertise, expect the interviewer to dig deeper into the topic to discover if you're a specialist in this area. Sometimes the team or company may have an individual who can interview you who specializes in that area. In short, if you claim to specialize in a topic, prepare for an in-depth evaluation.

If you have additional questions, feel free to submit a pull request.
