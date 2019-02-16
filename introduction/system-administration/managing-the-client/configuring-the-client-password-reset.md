---
description: Describes the steps necessary to configure the Password Reset functionality.
---

# Configuring the Client Password Reset

Password Reset is a common feature in applications. In ADempiere, users can request a new password if they have forgotten their current one. There is a bit of configuration required to make this work though. In particular:

* The Client must have a valid email configuration setup. \(See [Email Configuration](../general-rules/server/email-configuration.md)\);
* The User must already have an account and have a valid email address;
* A **Mail Template** for a "restore password" email that will be sent to the user has to exist and must include a link to the password reset web page \(the system account provides an example of this email\); and
* The **Client Info** tab in the **Client** window has to identify the email template in the _**Restore Password Mail Text**_  field.
* The Web application must be accessible to the user via a browser in order to complete the password reset process.

{% hint style="info" %}
Password reset is not available in the Java Client application.
{% endhint %}

The User requests a password reset through the login dialog. \(See [Logging In](../../getting-started/logging-in.md).\) If they submit a valid User ID, the system will send them a email with a link to a web page where they can reset their password.

The password reset is made using a Token which grants the User access to change their password. The tokens granted can be viewed in the **Token for Access** window in the **System Admin &gt; General Rules &gt; Security** menu.

{% hint style="warning" %}
The Token expires in 5 minutes.
{% endhint %}

