# EMail Configuration

The ADempiere Application can communicate through email if the email is configured properly. The System Administrator sets the System level email for support and server-level communications. Each Client can setup individual email configurations for use by the Client processes.

Email configurations are created on the **EMail Configuration** window found in the **System &gt; General Rules &gt; Server** menu. The fields should be self-explanatory for anyone familiar with adding an e-mail account to an application. ADempiere supports SMTP, IMAP or POP3 Protocols. Check with your email provider for the correct email configuration settings to use.

Once the email configuration is saved, select the configuration in the **Client** window/tab in the _**EMail Configuration**_ field. Complete the configuration by adding the _**Request EMail**_ , the _**Request User**_ and the _**Request User Password**_. These three fields are used when Client sends emails as the "From" addressee.

You can test the configuration by clicking the "Test Email" button in the Form View. A test email is sent from the Request Email to the Request Email.

{% hint style="info" %}
The Test Email process will also check that the _**Request Folder**_ exists and will send test emails from any Web Store record that has a Web Store EMail defined.
{% endhint %}

