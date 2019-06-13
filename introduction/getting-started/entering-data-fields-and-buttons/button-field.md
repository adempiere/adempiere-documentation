---
description: Use of Button fields
---

# Button Field

Buttons perform a command of some sort - starting a process, running a script or performing some other task.

The Button is defined as a field in the database, but data may not be stored there. Instead, the record in the Column definition includes information that determines how the Button is to function. There are a few special cases.

If the column name is:

* **Record\_ID** \([![Image:Icon\_Zoom24.png](http://wiki.adempiere.net/images/7/7c/Icon_Zoom24.png)](http://wiki.adempiere.net/File:Icon_Zoom24.png)\), then the button performs the [Zoom](http://wiki.adempiere.net/Zoom) function, going directly to the default window and tab for that record. This is useful in situations where the current window is reporting on the status of another record, such as in the [Workflow](http://wiki.adempiere.net/Workflow) windows. The Record\_ID value is pulled from the context. There are a few special cases of this as well:
  * If the current tab does not have a Record\_ID and the key column name is "AD\_Language", the Record\_ID is set to the AD\_Language\_ID value.
  * If the current tab does not have a Record\_ID and the process associated with the Button is "Un-Do Changes" or "Re-Do Changes", then the Record\_ID is set to the AD\_Changelog\_ID.
* **PaymentRule** \([![Image:Icon\_Payment24.png](http://wiki.adempiere.net/images/1/13/Icon_Payment24.png)](http://wiki.adempiere.net/File:Icon_Payment24.png)\), clicking the Button will pop-up the [Payment Dialog](http://wiki.adempiere.net/Payment_Dialog). If the invoice is not completed, the [Payment Dialog](http://wiki.adempiere.net/Payment_Dialog) will be limited to payments types. If the invoice is completed, the [Payment Dialog](http://wiki.adempiere.net/Payment_Dialog) will allow you to complete a full payment. This is very useful in POS applications when using POS Orders or Credit Orders with Invoice Indirect and immediate payment. The button text will reflect the payment method chosen.
* **DocAction** \([![Image:Icon\_Process24.png](http://wiki.adempiere.net/images/e/eb/Icon_Process24.png)](http://wiki.adempiere.net/File:Icon_Process24.png)\), clicking the Button will open the [Document Action Dialog](http://wiki.adempiere.net/Document_Action_Dialog). This dialog allows you to set the status \(Drafted, In Progress, Completed, Closed, etc...\) of the document. Changing the status will trigger the associated workflow process, if any, the document processing engine and the accounting engine. The button text will reflect the next document action in the normal workflow.
* **CreateFrom** \([![Image:Copy24.png](http://wiki.adempiere.net/images/c/c6/Copy24.png)](http://wiki.adempiere.net/File:Copy24.png)\) and there is no process associated with the Button, clicking the Button will open a [Create From Dialog](http://wiki.adempiere.net/Create_From_Dialog) where lines from an associated document can be selected and used to create lines in the current document. See the [Create From Dialog](http://wiki.adempiere.net/Create_From_Dialog) page for more information.
* **Posted** \([![Image:Icon\_InfoAccount24.png](http://wiki.adempiere.net/images/b/be/Icon_InfoAccount24.png)](http://wiki.adempiere.net/File:Icon_InfoAccount24.png)\) and the User's role has **Show Accounting** in the [**Role Window**](http://wiki.adempiere.net/ManPageW_Role), then if the document is processed and posted, clicking the button will open the [Account Info](http://wiki.adempiere.net/Account_Info) dialog with the Select Document set to the current document. The accounting consequences or financial accounting details of the posting will be shown. Note that the **Re-post** button will be enabled. If the document has not been posted yet, clicking the button will open a dialog that asks "Post Immediate?". Confirming this dialog will cause the record to be posted. Typically, the Posted button is hidden and will only appear once the document has been completed, closed, reversed or voided. The label of the button will reflect the status of the posting.

If none of the above apply, the software checks to see if a process is defined for the Button and attempts to run that process or invoke a custom form.

