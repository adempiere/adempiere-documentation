---
description: Information on the function and use of the Binary Data Field
---

# Binary Data Field

Binary Data fields can be used to store pretty much anything that can be found in a computer's file system. The binary data is stored as a BLOB or Binary Large OBject. The Binary field appears in ADempiere as a [Button](button-field.md). Clicking the button will open the File Chooser and allow you select a BLOB \(any file\) and save it to the database. The button text will show the following:

* "-" if there is no data stored
* "\#xyz" where xyz is the size of the data in bytes
* The name of the class object stored
* "?" if the data is not byte data and not a class.

If a blob is already saved, clicking the button will allow you to reverse the process and save the BLOB to the file system.

ADempiere does not make direct use of Binary fields in windows and tabs but they are used by the software for [Attachments](http://wiki.adempiere.net/Attachment), Images, Migration scripts and class instances. However, nothing prevents you from using Binary fields in any custom windows and tabs you develop.

