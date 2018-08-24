# Launching the Application

There are two ways of accessing the ADempiere Application: through a java software client that runs on the user's computer or through a web user interface \(webui\) which can be accessed through a browser. Both these applications communicate with the ADempiere Application Server. Which you use will be determined by your system implementation. In general, the two methods are similar and provide the same functionality. The User Guide will focus on the Client software and will discuss the web version where it differs.

## Launching the ADempiere Client using Web Start

To launch using Web Start, you will need the ADempiere Application Server URL. It may be provided as a link on your company's intranet or you can ask the System Administrator. It may look like `http://mycompany.com:8088/admin`.

Open the Application Server URL. It will look something like the following image.

![](../../.gitbook/assets/image_appserver_admin-1-1.png)

The WebStart option automatically makes sure that the your computer will use the latest version of the ADempiere Client.

From the Application Server web page, click on the blue WebStart button and you will see the WebStart Dialog:

![](../../.gitbook/assets/webstart_download_progress.jpg)

Note: If the application client does not start immediately after this, you may need to ask your System Administrator to ensure the java JNLP file is associated with the Java Web Starter application \(javaws\).

If a security window appears, click on "Always trust content from this publisher".

The very first time the application starts, you will see a license dialog. Accept the license terms.

The application client should start at this point and present a log in dialog.

