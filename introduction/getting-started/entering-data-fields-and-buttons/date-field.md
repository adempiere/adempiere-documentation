---
description: Using the Date field
---

# Date Field

## Date ![Image:Icon\_Calendar24.png](../../../.gitbook/assets/calendar24.gif)

The Date control maintains data as a time stamp in a format consistent with the locale and language of the user's system. The format definitions follow the Java class [SimpleDateFormat](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html). If no default format is found, the JDBC standard will be used "yyyy-MM-dd". Local formats will be converted to contain at least "dd" and "MM" numbers in the format code. Year codes will be increased to at least four digits.

The Date control operates like a text field where data can be input by keyboard entry. The digit being entered is enclosed in blue square brackets and format characters are ignored - just type the numbers.

Alternatively, the [Calendar Tool ](../dialogs-and-forms/calendar-tool.md)can be opened and used to enter a date.

The pop-up menu displays the following options:

* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

