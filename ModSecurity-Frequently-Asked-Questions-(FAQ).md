= ModSecurity Frequently Asked Questions (FAQ) =
Version 3.0 / (March 1, 2011)
== Who Leads the ModSecurity Project? ==
ModSecurity is supported by Trustwave's SpiderLabs Team [https://www.trustwave.com/spiderLabs.php] and includes the following team members:
*Ryan Barnett - ModSecurity Project Lead and OWASP ModSecurity Core Rule Set Project Lead
*Breno Silva - ModSecurity Lead Developer
*Brian Bebeau - ModSecurity Developer
*Rodrigo Montoro - ModSecurity Rules/Signature Developer
*Steve Ocepek - SpiderLabs Research Team Lead

Suggestions for enhancements of this document are always welcome. Please email them to the Mod-Security-Users mailing list [http://lists.sourceforge.net/lists/listinfo/mod-security-users].

= Background and Support =

== What exactly is ModSecurity? ==

ModSecurity™is an open source, free web application firewall (WAF) Apache module. With over 70% of all attacks now carried out over the web application level, organizations need all the help they can get in making their systems secure. WAFs are deployed to establish an external security layer that increases security, detects and prevents attacks before they reach web applications. It provides protection from a range of attacks against web applications and allows for HTTP traffic monitoring and real-time analysis with little or no changes to existing infrastructure.

== Where do I get more help on ModSecurity? ==

The ModSecurity website is the definitive location for all documentation - http://www.modsecurity.org/ Other good resources are available in the source distribution, including the ModSecurity Reference Manual on the Documentation page - http://www.modsecurity.org/documentation/. There is also a excellent mailing list, mod-security-users. You can find info on how to signup at http://lists.sourceforge.net/lists/listinfo/mod-security-users. You can also join the #modsecurity channel on irc.freenode.net.

== Do I need to sign up for the Mod-User Mail-list before I can send emails? ==

Yes, only subscribers are able to post messages. As mentioned in the previous section, you will need to visit the mail-list website to register.

== Is there anything that I should do prior to sending emails to the mail-list? ==

Yes. There is a good chance that the issue you are facing has already been discussed and, most likely, a fix has already been presented. You can review the mail-list archive online at the ModSecurity project site on SourceForge. You can also use the Search interface available for topic threads that are archived to the various mirror sites. For example, if you had a quesiton about Exceptions and ModSecurity, you could use the following search to find past mail-list threads on this topic. If you can not find an answer to your question after doing some research, you should then send an email to the mod-security-users mail-list.

== Where can I find books about Web Application Firewalls and ModSecurity? ==

Books

ModSecurity Handbook is "The definitive guide to the popular open source web application firewall", written by Ivan Ristic (original author of ModSecurity). The book is available from Feisty Duck in hardcopy or with immediate access to the digital version which is continually updated.


ModSecurity 2.5 is "A complete guide to using ModSecurity", written by Magnus Mischel. The book is available from Packt Publishing in both hardcopy and digital forms.


Apache Security is a comprehensive Apache Security resource, written by Ivan Ristic for O'Reilly. Two chapters (Apache Installation and Configuration and PHP) are available as free download, as are the Apache security tools created for the book.


Preventing Web Attacks with Apache. Building on his groundbreaking SANS presentations on Apache security, Ryan C. Barnett reveals why your Web servers represent such a compelling target, how significant exploits are performed, and how they can be defended against.

Training
Trustwave's SpiderLabs offers a variety of web applicaiton security training options include open source ModSecurity rule writing classes. Please use this contact form for more information. Ask about:

ModSecurity: Deployment and Management
ModSecurity: Rules Writing Workshop
ModSecurity: Virtual Patching Workshop

== Will I always get an immediate answer to my question on the open source mod-security-users mail-list? ==

The open source mod-security-users mail-list is "best effort" support meaning that we will aspire to respond to emails as quickly as possible however the actual response time may vary depending on factors such as time of day, time of week and complexity of the question. If your email is sent on the week-end or if your question involves setting up test systems, unique configurations or interactions with a custom application then it may take some time to respond.

== If I don't get an immediate response, should I send an email to the Trustwave Technical Support email address? ==

No. The Trustwave Technical Support email address is for commercial ModSecurity customers only.

= Getting Started =

== What type(s) of security models does ModSecurity support? ==

There is a common misconcpetion that ModSecurity can only be used for negative policy enforcement. This is not the case. ModSecurity does not have any default security model "out-of-the-box." It is up to the user to implement appropriate rules to acheive the desired security model. That being said, these are the security models which are most often employed:

Negative Security Model - looks for known bad, malicious requests. This method is effective at blocking a large number of automated attacks, however it is not the best approach for identifying new attack vectors. Using too many negative rules may also negatively impact performance.

Positive Security Model - When positive security model is deployed, only requests that are known to be valid are accepted, with everything else rejected. This approach works best with applications that are heavily used but rarely updated.

Virtual Patching - Its rule language makes ModSecurity an ideal external patching tool. External patching is all about reducing the window of opportunity. Time needed to patch application vulnerabilities often runs to weeks in many organizations. With ModSecurity, applications can be patched from the outside, without touching the application source code (and even without any access to it), making your systems secure until a proper patch is produced.

Extrusion Detection Model - ModSecurity can also monitor outbound data and identify and block information disclosure issues such as leaking detailed error messages or Social Security Numbers or Credit Card Numers.

== What's new in ModSecurity and why should I upgrade if I am already using ModSecurity 1.x? ==

There are many significant changes and enhancemnts in ModSecurity 2.5 over the 1.x branch, including:

In order to use the OWASP ModSecurity Core Rules, you must use the 2.x version of ModSecurity as it takes advantage of specific features not available in previous versions.

Five processing phases (where there were only two in 1.9.x). These are: request headers, request body, response headers, response body, and logging. Those users who wanted to do things at the earliest possible moment can do them now.

Per-rule transformation options (previously normalization was implicit and hard-coded). Many new transformation functions were added.

Transaction variables. This can be used to store pieces of data, create a transaction anomaly score, and so on.

Data persistence (can be configured any way you want although most people will want to use this feature to track IP addresses, application sessions, and application users).

Support for anomaly scoring and basic event correlation (counters can be automatically decreased over time; variables can be expired).

Support for web applications and session IDs.

Regular Expression back-references (allows one to create custom variables using transaction content).

There are now many functions that can be applied to the variables (where previously one could only use regular expressions).

XML support (parsing, validation, XPath).

For more information, it is suggested that you review the SecurityFocus interview that Ivan Ristic gave on ModSecurity 2.0 as it outlines these new features in more detail.

== How do I migrate my rules from the ModSecurity 1.x format into the 2.x format? ==

Due to the many changes in the ModSecurity 2.0 rules language, you can not directly use existing rulesets. You will need to translate the functionality of any custom rules into the new rules language. A migration matrix is available here [http://www.modsecurity.org/documentation/ModSecurity-Migration-Matrix.pdf] that will assist with this process.

== How do I install ModSecurity 2.0? ==

The installation procedures for installing ModSecurity 2.5 has changed from previous versions. It now includes a configure script that should help to identify all local settings. After running configure, you then run the make and make install commands. You no nonger use apxs directly.

== I hear that ModSecurity can be run in embedded-mode, what does that mean exactly? ==

The term "embedded" simply refers to the fact that ModSecurity, running as an Apache module, is running inside the webserver process. Most WAFs function as totally separate hosts and sit in front of the web servers. Running in embedded-mode has some advantages and disadvantages that should be considered:

Advantages
Easy to add to an existing Apache server.

Not a point of failure with respect to traffic.

Disadvantages
ModSecurity can only protect the local web server.

ModSecurity will consume local resources such as CPU and RAM.

Management of of log files and configurations can become difficult if you have multiple installations.

== I hear that ModSecurity can be run in reverse proxy-mode, how does that differ from embedded-mode? ==

The only difference with this deployment vs. an embedded one is that Apache itself is configured to function as a reverse proxy.

Advantages
Single point of access – functions as a choke point so you consolidate applying security settings and makes management easier.

Network topology is hidden from the outside world - so it will be more difficult for attackers to enumerate your web platforms.

Increased performance – if SSL accelerators/caching used.

You can implement vulnerability filters to protect and vulnerable web server or application on the backend (IIS, Netscape, ASP, PHP, etc...). See related section on Virtual Patching.

Disadvantages
A potential traffic bottleneck if the reverse proxy can not handle the network load.

A potential point of failure - if the reverse proxy goes down it may cause a denial of service to the web applications that are behind it.

Requires changes to the network.

= Configuring ModSecurity =

== Should I initially set the SecRuleEngine to On? ==

No. Every Ruleset can have false positive in new environments and any new installation should initially use the log only Ruleset version or if no such version is available, set ModSecurity to Detection only using the SecRuleEngine DetectionOnly command. After running ModSecurity in a detection only mode for a while review the evens generated and decide if any modification to the rule set should be made before moving to protection mode.

== How do I get ModSecurity to inspect request and response bodies? ==

You need to set the the following two directives:

SecRequestBodyAccess On

SecResponseBodyAccess On

== How can I verify exactly how ModSecurity is processing rules and requests? ==

You need to enable the debug log with SecDebugLog and increase the log level with SecDebugLogLevel. It you set the debug log level to 9 it will tell you exactly what tasks it is completing along with what data it is acting upon. Do be aware that while the increased debug log level does help from a trouble-shooting perspective, it does negatively impact performance.

= ModSecurity Rules Language =

== What are the OWASP ModSecurity Core Rules (CRS) and why should I use them? ==

Using ModSecurity requires rules. In order to enable users to take full advantage of ModSecurity immediately, Trustwave's SpiderLabs is sponsoring the OWASP ModSecrity Core Rule Set (CRS) Project. Unlike intrusion detection and prevention systems which rely on signature specific to known vulnerabilities, the Core Rule Set provides generic protection from unknown vulnerabilities often found in web application that are in most cases custom coded. You may also consider writing custom rules for providing a positive security envelope to your application or critical parts of it. The Core Rule Set is heavily commented to allow it to be used as a step-by-step deployment guide for ModSecurity.

== What attacks do the Core Rules protect against? ==

In order to provide generic web applications protection, the Core Rules use the following techniques:

HTTP protection - detecting violations of the HTTP protocol and a locally defined usage policy.

Common Web Attacks Protection - detecting common web application security attack.

Automation detection - Detecting bots, crawlers, scanners and other surface malicious activity.

Trojan Protection - Detecting access to Trojans horses.

Errors Hiding – Disguising error messages sent by the server

In addition the ruleset also hints at the power of ModSecurity beyond providing security by reporting access from the major search engines to your site.

== Can I use the Core Rules with ModSecurity 1.x? ==

Unfortunately, no. The Core Rules takes advantage of the ModSecurity 2.0 rules language and is therefore not backward compatible.

== How do I whitelist an IP address so it can pass through ModSecurity? ==

The first issue to realize is that in ModSecurity 2.0, the allow action i sonly applied to the current phase. This means that if a rule matches in a subsequent phase it may still take a disruptive action. The recommended rule configuration to allow a remote IP address to bypass ModSecurity rules is to do the following (where 192.168.1.100 should be substituted with the desired IP address):

SecRule REMOTE_ADDR "^192\.168\.1\100$" phase:1,nolog,allow,ctl:ruleEngine=Off

If you want to allow uninterrupted access to the remote IP address, however you still want to log rule alerts, then you can use this rule -

SecRule REMOTE_ADDR "^192\.168\.1\100$" phase:1,nolog,allow,ctl:ruleEngine=DetectionOnly

If you want to disable both the rule and audit engines, then you can optionally add another ctl action:

SecRule REMOTE_ADDR "^192\.168\.1\100$" phase:1,nolog,allow,ctl:ruleEngine=Off,ctl:auditEngine=Off

== Are there rule differences for identify missing/empty variables between ModSecurity 1.x and 2.x? ==

Yes there are. Many of these differences are outlined in the Migration Matrix document listed previously. Another common rule difference issue that arises is when you want to create white-listed ModSecurity rulesets which enforce that certain headers/variables are both present and not empty. In ModSecurity 1.x, you could create one rule that handles this while in ModSecurity 2.x you would need to write a chained rule.

On the surface, you might think "The 1.x rules way is better since you only need 1 rule..." however you need to realize that anytime you have rules or directives that implicitly enforce certain capabilities you run the risk of having false positives as it could match things that you didn't want them to. For instance, what if you have a situation where certain web clients (such as mobile devices) legitimately include some headers, however they are empty? Do you want to automatically block these clients? With the ModSecurity 1.x Rule Language, you would have to remove the entire rule. With the ModSecurity 2.x Rule Language, however, you are able to create rules to more accurately apply the logic that you desire.

Please refer to the following Blog post for more information.

== How do I handle False Positives and creating Custom Rules? ==

It is inevitable; you will run into some False Positive hits when using web application firewalls. This is not something that is unique to ModSecurity. All web application firewalls will generate false positives from time to time. The following Blog post information will help to guide you through the process of identifying, fixing, implementing and testing new custom rules to address false positives.
http://blog.spiderlabs.com/2011/08/modsecurity-advanced-topic-of-the-week-exception-handling.html

== Will using a large amount of negative filtering rules impact performance? ==

Yes. Each and every rule that you implement will comsume resources (RAM, CPU, etc...). The two most important factors to consider with creating ModSecurity rules are the total number of rules and the Regular Expression optimizations. A single rule with a complex regular expression is significantly faster than multiple rules with simple regular expressions. Unfortunately, it is quite easy to create inefficient RegEx patterns. Optimizing RegExs by utilizing Grouping Only/Non-Capturing Parentheses can cut the validation time by up to 50%. The Core Ruleset is optimized for performance.

== What is a Virtual Patch and why should I care? ==

Fixing identified vulnerabilities in web application always requires time. Organizations often do not have access to a commercial application's source code and are at the vendor's mercy while waiting for a patch. Even if they have access to the code, implementing a patch in development takes time. This leaves a window of opportunity for the attacker to exploit. External patching (also called "just-in-time patching" and "virtual patching") is one of the biggest advantages of web application firewalls as they can fix this problem externally. A fix for a specific vulnerability is usually very easy to design and in most cases it can be done in less than 15 minutes.

Trustwave's new 360 Application Security Program includes virtual patching services delivered by SpiderLabs.

= Managing Alerts =

== How do I manage ModSecurity logs if I have multiple installations? ==

If you have more then 1 ModSecurity installation, you have undoubtedly run into issues with consolidating, analyzing and responding to alert messages. Unfortunately, the original "Serial" format of the audit log was multi-line with all records held within one file. This made remote logging difficult. What was really needed was to have a mechanism to send logs onto a centralized logging host made specifically for processing ModSecurity Alert data. This is the purpose of the mlogc program. It comes with the ModSecurity source code and can be used to send individual audit log entried to a remote host in near real-time.

== Is there an open source Console to send my audit logs to? ==

Christian Bockermann has developed an outstanding free tool called AuditConsole that allows you to centralize and analyze remote ModSecurity audit log data.

== Can I send ModSecurity alert log data through Syslog? ==

Yes. If you already have a central Syslog infrastructure setup and/or if you are using some sort of SIEM application (such as Intellitactics, etc...) then you might want to include the short version ModSecurity alert messages that appear in the Apache error_log file. You can easily reconfigure Apache to send its error logs through Syslog onto a remote, central logging server however the data being forwarded is a very small subset of the entire transaction. It is only a warning message and not enough information to conduct proper incident response to determine if there was a false positive or if it was a legitimate attack. In order to determine this information, you need access to the ModSecurity Audit log files.
