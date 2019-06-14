# Can I deploy applications over SSB?

---

It would be possible to deploy applications over ssb by sending the assets for that application as an attachment.
Then other users could run that app on their local machine.

We have plans to build on this in the future.

## How will you know it is safe to run an application?

Applications would be run in a sandbox, and, since new versions of the application would be immutably published, it would always be possible to see the history of that application.
This would actually be much more secure that a normal web application.
In a normal website your browser just downloads code and runs it.
While it does run in a sandbox, it would be entirely possible to send one person a special version of the code that contained a targeted backdoor.
Since, in ssb, everyone will see the same history, it would be impossible to attack a single user like this without eventually being caught out.

## Auditing applications

Some applications require a higher quality standard, especially if they need special rights to the device's resources.

Since performing a security audit is a highly skilled task, most users will not be able to perform their own security audit.
In this case, the user could "delegate" the auditing task to another user (or users) who perform the audit, posting a message declaring a given version safe to run.
Since the user can choose their auditors independently, it would mean an attacker would have to compromise the developers and many auditors in order to get people to install malicious code.

Auditing could also be applied to application permissons.
Of course, the decision about what permissions is reasonable for a given application is much simpler than looking at code and checking there is nothing unsafe.
