# Reporting - Amazon 1 click device XSS

I am sharing a bug that is far from complicated but drives home the point that all user-controlled data should be sanitized and output encoded if it will return to the client. Sometimes because of the nature of the data, developers assume that certain types of input can't exist there. I've used this trick to find multiple bugs in the past few years.

My devices, such as my iPhone and iPad, have names that can trigger XSS. I achieve this by naming the device some XSS payload, such as the simple one found below:

![alt text](.img/Amazon%20-%201%20click%20XSS%20iphone%20payload.png)

My XSS payload device names have triggered XSS in different places, including notification software, routers, and in this case, Amazon. The bug triggers when software has a webpage that lists devices. In the case of Amazon, the XSS triggers when accessing the one-click devices page. The bug was reported through email, as seen in the next section.

## Reporting the bug to Amazon

Report date: July 19th, 2017

Issue fix confirmed: November 13th, 2017

Reported to: Amazon Security [security@amazon.com]

Bug Type: XSS(Stored)

Description:
Under the account settings for 1-click purchasing, found under:
Your Account> Manage Default Address and 1-Click Settings
The device names listed under 1-Click Status are not sanitized
 
POC:
My phone name is <script>alert(1)</script>, and once this is loaded into the 1-Click Status, an alert window appears with the number 1

![alt text](.img/Amazon%20-%201%20click%20XSS%20POC.png)

![alt text](.img/Amazon%20-%201%20click%20XSS%20browser%20console.png)

If you need additional information, please let me know.

Thanks,

Justin

## Discovery of mobile compatibility and reporting (Update)

Later, I found this could be triggered from a mobile phone, as seen in the example below. I reported to Amazon on August 19th, 2017:

![alt text](.img/Amazon%20-%201%20click%20XSS%20mobile%20POC.png)

## Fix implemantation

Amazon fixed this issue by adding output encoding to the device listing. Additionally, they have moved the 1-click device listing to a dedicated page under Your Account -> 1-Click settings -> Manager 1-Click for your devices:

![alt text](.img/Amazon%20-%201%20click%20XSS%20-%20fix.png)

## Conclusion

In this case, the 1-click device list is only something the user would view, and the attack vector is through the name of their device. A valid attack vector I specified to them in a later email is to attack customer representatives who assist you with your account and have to view my 1-click devices for troubleshooting. In other occurrences of this bug, I have discovered other users would be affected by my XSS payload.
