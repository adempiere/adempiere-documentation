# Launching the Application

There are two ways of accessing the ADempiere application: through a java software client that runs on the user's computer or through a web user interface \(webui\) which can be accessed through a browser. Both these applications communicate with the ADempiere Application Server. Which you use will be determined by your system implementation. In general, the two methods are similar and provide the same functionality. The User Guide will focus on the java client and will discuss the web version where it differs.

## Launching the ADempiere JAVA Client using Web Start

To launch the application, you will need the ADempiere Application Server URL. It may be provided as a link on your company's intranet or you can ask the System Administrator. It may look like

```text
http://mycompany.com:8088/admin
```

Open the Application Server URL. It will look something like the following image.

![](../../.gitbook/assets/image_appserver_admin-1.png)

### Accessing the Web Application

To log in to the Web Application, click the link for the **ADempiere ZK Webui** in the administration page above. You may also have been given the address directly. It will look something line this:

```text
http://mycompany.com:8088/webui
```

The web page shown will be the login page to the Web Application running on the server. See [Logging In](logging-in.md) for more information.

### Launching the Java Client Using WebStart

The WebStart option automatically makes sure that the your computer will use the latest version of the ADempiere JAVA Client.

From the Application Server web page, click on the blue WebStart button and you will see the WebStart Dialog:

![](../../.gitbook/assets/webstart_download_progress.jpg)

{% hint style="info" %}
If the application Java Client does not start immediately after this, you may need to ask your System Administrator to ensure the Java JNLP file is associated with the Java Web Starter application \(javaws\).
{% endhint %}

If a security window appears, click on "Always trust content from this publisher".

The very first time the application starts, you will see a license dialog. Accept the license terms.

The application client should start at this point and present a log in dialog. See [Logging In](logging-in.md) for more information.

