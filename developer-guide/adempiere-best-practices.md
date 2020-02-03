---
description: Outlines the practices to be followed for development within Adempiere.
---

# ADempiere Best Practices

## Overview

This page outlines the practices to be followed for development within Adempiere. The rules and processes described are intended to ensure that the project is able to maintain the high standard of quality that is expected from a business critical application.

## Commit Policy

The following guidelines describe the best practice when committing code in the Adempiere repository.

### **General Principles**

1. We work as a team. A good team working together and sharing ideas will be smarter than any single developer. Communicate your ideas and intent, seek feedback, be kind with criticism, accept criticism with grace, help out and don't hold back.
2. Use the Pull Request model as much as possible.  It provides a means for others to review your code.  The Continuous Integration service can test your build prior to merge.  Help out by reviewing pull requests submitted by others.
3. The ability to commit to the Adempiere repository is a privilege, not a right.
4. To have autonomy you need a high degree of responsibility and authority. You get these by working with the team. There is no place for loners or loose cannons here.
5. Committers \(those that commit directly to the project repository\) are expected to take responsibility for their actions and to not use that privilege to bypass the software development process.
6. If you break something, you should make every effort to fix it yourself, rather than relying on others to clean up for you. 

### **Documentation**

All changes to the code base need to be adequately documented so that others can easily find out why a change was made and have the necessary information to allow them to assist with maintaining the new code.  The level and amount of documentation should be in proportion to the degree the proposed change will impact on the behavior of Adempiere.

All pull requests/commits must have some associated documentation such as a pull request, bug report or feature request.  At a minimum, an issue should be opened on Github and referenced in the commit.  The issue should be descriptive.  A one-line description is not sufficient to allow others to review your work in a meaningful way.  

Issues or bugs reported should include a description of how to reproduce the issue in the GardenWorld demo or a System account.  If it's not easily reproducible in GardenWorld, explain in detail what the issue is, in which scenarios the issue appears and the proposed solution \(if any\).

1. If you are reporting a feature request also provide a suggested use case. When you have implemented the feature request you must then explain how to use the new functionality.
2. Larger changes are better documented in a a wiki page that also provides end user guidance.
3. It is not acceptable to leave it up to others to "read the code" to work out how your contribution works. [\[3\]](http://sourceforge.net/forum/forum.php?thread_id=2681108&forum_id=610548)
4. Technical Documentation. Ideally the committer should endeavour to provide some technical documentation. This ensures that if the original committer is unavailable, others will be able to maintain the code without resorting to reverse engineering.

   **Approval**

5. Bug fixing can be done directly. If you are confident that you have found a bug and that you have a fix that does not have any adverse side effects, it is acceptable to commit directly without waiting for community consultation.
   1. However, if there is any doubt, committers are advised to request further feedback before proceeding. [\[4\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
6. Feature requests require community approval. To ensure that all new features will be useful to the community at large and properly implemented a process of community consultation must be undertaken.
   1. This involves proposing the contribution, addressing any concerns raised by community members \(paying particular attention to functional specialists\), and receiving a positive vote for the request. See the section on voting below.
   2. Getting community approval for implementing a feature request is not sufficient to guarantee acceptance of a contribution. All the other requirements outlined here must also be met.
7. New features entering trunk should be submitted for review in an separate branch or through a patch

   1. Community approval may be withheld until others are able to review the actual code, either by the code being committed to a "sandbox" branch, or submitted as a patch.
   2. Other committers may vote against a proposed feature until such a submission is provided for them, if they do so, they should make every effort to review the submission as quickly as possible.[\[5\]](http://sourceforge.net/forum/message.php?msg_id=5828131)

   **Implementation**

8. The implementation in code of a bug fix or feature contribution must adhere to the following guidelines.
   1. To integrate into trunk a contribution must be complete, documented and testable
   2. Do not commit half finished code into trunk in the hope that someone else will take it over.
   3. If you wish to contribute work that you are unable to complete, supply it as a patch or separate branch. [\[6\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
9. Don't drop existing elements or functions.
   1. Don't drop "not-added-by-you" things \(db elements or functionalities\). We must assume that any existing part of Adempiere may be being used by someone's implementation.
   2. Unless there is a good reason to drop it, for example functionality is really broken, do not drop it.
   3. If there is a valid reason then please first ask in forums before considering the drop. [\[7\]](http://sourceforge.net/forum/forum.php?thread_id=2667992&forum_id=610548)
10. Always review collateral effects of your changes
    1. Every time you touch one line of code or application dictionary please review the dependencies \(collaterals\). Eclipse helps a lot pointing to the name of the method/variable + right click + references -&gt; workspace. For other code \(like callouts, processes, etc\) sometimes you need to check the dictionary to see where is it called \(I normally review Adempiere\_pg.dmp\).[\[8\]](http://sourceforge.net/forum/forum.php?thread_id=2668000&forum_id=610548)
11. Do not commit a change if you only implemented it for one database
    1. We officially support multiple databases and all changes should work exactly the same on both every database platform. Do not assume that someone else will port it for you. [\[9\]](http://sourceforge.net/forum/forum.php?thread_id=2668000&forum_id=610548) and [\[10\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
12. Support both Java 5 and Java 6
    1. We officially support both these versions of Java. If you are coding against Java 6 please ensure that code is backwards compatible with 5. [\[11\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
13. Only use the current trunk version of ModelGenerator

    1. There must be just one official version of ModelGenerator. Private versions of ModelGenerator must be avoided. [\[12\]](http://sourceforge.net/forum/forum.php?thread_id=2663645&forum_id=610548)

    **Code Style**

14. Code must be properly indented
    1. But don't re-indent fully working code just because it doesn't look exactly right in your IDE. The code might be indented nicely in someone elses IDE and if we keep reformatting according to our particular IDE we'll end up with a lot of commits but nothing really done. We won't be able to track "real" changes. [\[13\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
15. Proper usage of variable names [\[14\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
16. All comments and variables in english [\[15\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
17. No duplicated code [\[16\]](http://sourceforge.net/forum/message.php?msg_id=5828131)
18. Use constants or MSysConfig instead of hardcoded things [\[17\]](http://sourceforge.net/forum/message.php?msg_id=5828131)

    **Committing**

19. Follow the best practices for using SVN when committing. [\[18\]](http://svn.collab.net/repos/svn/trunk/doc/user/svn-best-practices.html)
20. All commits should be atomic:
    1. that is they are the complete code patch that addresses a Bug Report \[**BR**\] or Feature Request \[**FR**\] in sourceforge.
    2. If the contribution is unusually large it may be committed in small parts but then commit should be distinct functional parts. 
    3. Preferably a commit must solve one and only one tracker - this is to ease integration with other branches or maintained versions.
21. Commit Early in YOUR day:
    1. Only commit if you are around to support or even revert in case of a problems.
22. Update before commit:
    1. Do an SVN update and ensure all still compiles locally before you commit.
23. Reference the BR/FR in the commit comments:
    1. include the full url to the sourceforge BR/FR, but also include a short, but descriptive, comment that does not require the reader to go to the BR/FR in sourceforge unless they require details. Example:

       ```text

       ```

       \[ 2354040 \] Implementation Replication Mode, Type, Eventhttp://sourceforge.net/tracker/index.php?func=detail&aid=2354040&group\_id=176962&atid=879335Enhance replication to allow export and import of documents and then execute the document status action.
24. Synchronise & Build:
    1. after committing sync again with the repository and confirm all still builds without errors.
25. On successful commit Update the BR/FR:

    1. include the SVN revision reference and set the status & resolution fields as appropriate.

    **Rules suggested on Nov-2007 to reach TRUNK**

    [http://sourceforge.net/forum/forum.php?thread\_id=1881039&forum\_id=611167](http://sourceforge.net/forum/forum.php?thread_id=1881039&forum_id=611167)

26. Proof of stability. This should be base on community feedback on binary release. Optional: Production site, unit and functional test case.
27. Sample Data. There should be some sample data available.
28. Maintainer. Must have dedicated maintainer \( individual or company \). Must follow existing Adempiere Developer's criteria.
29. Branding and copyright issue. No vendor branding, must prove to be original work.
30. Migration script. Support all supported databases, i.e oracle and postgresql and pl/java
31. Migration scripts for ADempiere &gt;342 + 353a shouldn't use or implement new pl/java functions.
32. Migration Process COMPLETE and documented. For new module that replace or enhance existing functionality, it is very important to have the migration process documented.

    **Voting**

    **For new functionality**

33. Vote takes place in SourceForge forums or trackers

    1. Active members of the community are entitled to vote
    2. A minimum of 72 hours must pass from the call for a vote before the matter can be considered decided
    3. The vote is decided in favour of the simple majority of the participating voters. At least one vote most be received for a vote to count.
    4. A positive vote only indicates that the proposed new functionality is in principle suitable for inclusion in Adempiere. It does not override a fact that a particular implementation of that functionality must also meet all the other requirements listed above.

    **Suggestions about hiring sponsored developments to ease inclusion in trunk**

    [http://sourceforge.net/forum/forum.php?thread\_id=1785728&forum\_id=611167](http://sourceforge.net/forum/forum.php?thread_id=1785728&forum_id=611167)

34. See also [Sponsorship rules](http://wiki.adempiere.net/Sponsorship_rules)

    **Advices suggested on Jul-2007**

    **License GPLv2**

35. Sponsored development must be released under "GPLv2 or any later version"
36. If some development is put in wiki, discussed with community, enhanced with community ideas, etc.
37. The best practice can be to release it with the same Adempiere license. Very possibly community would not help or opine in a sponsored development that will be released as proprietary.

    **Contributor Agreement**

38. All sponsored development must be contributed signing an Adempiere Contributor Agreement \(just one agreement by developer\) like the one proposed here: [Contributor\_Agreement](http://wiki.adempiere.net/Contributor_Agreement)
39. Initially contributor agreements must be sent to a selected trustee.
40. This is helping to ensure the first clause. It's a common practice in Open Source projects after the SCO vs IBM case.

    **Credit for the Author**

41. It is especially important in an open-source project to ensure that the developers and authors of the code are given proper recognition for their work. The credit should include sufficient detail that future developers working on that code can find information about the rational for the design and a point of contact for additional information.
42. As a minimum, each commit/patch should include modifications to file header that provide the credit for the author. The credit should include references to additional information in the trackers, feature requests and/or patches by both reference number and a url.
43. Developers should add this information when submitting patches or code for commit. This will make it easier for others to commit the work on the developer's behalf.
44. Commiters should ensure that the information is included in the patches or code and, if not, add it. Commiters should, where practical, also include the author's name in the commit comment. The committer's name should appear as the "author" \(-u option in Mercurial\) of the commit. [\[19\]](http://www.adempiere.com/FT/TT_meeting_minutes_December_5th_2011)

    ```text
    /******************************************************************************
     * Product: Adempiere ERP & CRM Smart Business Solution                       *
     * Copyright (C) <Company or Author Name> All Rights Reserved.                *
     * This program is free software; you can redistribute it and/or              *
     * modify it under the terms of the GNU General Public License                *
     * as published by the Free Software Foundation; either version 2             *
     * of the License, or (at your option) any later version.                     *
     * This program is distributed in the hope that it will be useful,            *
     * but WITHOUT ANY WARRANTY; without even the implied warranty of             *
     * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.                       *
     * See the GNU General Public License for more details.                       *
     * You should have received a copy of the GNU General Public License along    *
     * with this program; if not, write to the Free Software Foundation, Inc.,    *
     * 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA.                     *
     *                                                                            *
     * @author <autor name>, <autor@email.com>                                    *
     * BF [ <number> ] or FR [ <number> ] Description about the bug tracker       *
     * URL of Tracker                                                             *
     *  			                                                       *
     *****************************************************************************/
    ```

    [See an example](http://adempiere.hg.sourceforge.net/hgweb/adempiere/adempiere/file/5c83f57ac3e8/client/src/org/compiere/apps/APanel.java)

    **Peer review**

45. Sponsored development must follow peer review from a committer to be included in trunk

    1. if the developer is a committer, then must have peer review from other committer \(same as all contributions in trunk\)

    **Tools used**

46. In order to ease inclusion in core, the development must follow guidelines from the project - about tool used for integration:

    1. SQL migration scripts
    2. if the developer have problems with migration scripts, he must at least provide 2pack package

    **Must follow Adempiere conventions**

47. Developer must follow Adempiere conventions, i.e. code, directory tree, naming
48. Adempiere conventions are not clearly written, but Adempiere is big enough to get some conventions just looking what currently we have.

    **Test Cases**

49. It would be good developer provide/document simple test cases for the contribution
50. It's a good advice for sponsors when hiring a developer put the condition that deliverables must include documentation and test cases. The developer must know if the money is enough to make such work.
51. [TestFramework](http://wiki.adempiere.net/TestFramework) Prototype framework for creating user tests

    **Visibility**

52. Try to keep updated the advance in a wiki page
53. Simple advice that also can be put as a condition from sponsor to developer in order to maximize the community involvement.

    **Sponsored developments must be made in a branch and updated frequently**

    **About branches**

54. Branches are allowed \(and in fact they're encouraged\) to conduct experiments, to work in specific projects or in tasks, or to coordinate team work.
55. Private branches are allowed - owner\(s\) of branch rule the branch \(all these rules are suggested in this case, but the owner\(s\) can expand or shrink these rules\)

    **About releases**

56. Official releases must come from trunk
57. Official release must be tagged as alpha, beta, release candidate or stable.
58. This is subject to the number of errors open, the completeness of functionalities, and other issues related to quality of release.
59. Unofficial releases are allowed from branches

    1. in this case the release must have the name of the branch
    2. in this case the release must NOT be tagged as alpha, beta, release candidate or stable, unless community votes and after a review of open bugs, completeness of functionalities, and other issues related to quality of release.

    **Suggested policies for extensions**

    **Meeting 2008-11-05**

60. According to suggestions received on [meeting nov-5-2008](http://wiki.adempiere.net/CC_Meeting_Full_20081105) convoked by the [more boring ruler](http://wiki.adempiere.net/User:CarlosRuiz).

    **Generate ID's from centralized dict**

    **Assign specific entity type and prefix rules**

61. It's suggested also to follow entity type and prefix rules for all columns and tables created.

    **Build on top and not changing kernel**

62. Sometime an extension might replace some code in core but that is usually just a problem in the core rather than changing the definition of an extension
63. Definition of kernel: common functionalities, like PO, like window management, etc - none related to business rules ...

    **Work in a branch**

64. It's encouraged to work in an adempiere branch and open for adempiere committers. But anyways it can be analyzed if extension developer wants to open an own project in sourceforge \(or any open source hosting site\).
65. You don't need permissions to experiment in your own branch/project - and add things to core. If you want something integrated in trunk you must follow rules stated in this document.
66. Extension developers must have a playground where they can develop without asking too much about permissions - following some recommendations to allow easy integration.

    **If several extensions are in competence - is suggested to let them compete as extensions, not including any on trunk**

    Integrating several extensions at the same time can lead to column collision problems.

    **Follow the recommended extension architecture**

67. Write Callouts
68. Write ModelValidator
69. Don't generate model for your columns \(but you can for your new tables\), instead of this use the generic getters and setters available in PO.java

    **License**

70. License must be "GPLv2 or any later version". An explanation can be found at [http://www.gnu.org/licenses/gpl-2.0.html](http://www.gnu.org/licenses/gpl-2.0.html) \(term 9\).

    **No hiding sources**

71. It's encouraged to avoid the SaaS loophole to hide sources \(or any other loophole within this license\).
72. Code must be open for everybody in any release.

    **Certification**

73. If you follow the suggested policies here - you can be certified as adempiere friendly extension - and we can consider including it within the official release.

    **Coding Standards**

    **Suggestion & Questions Coding Standards**

    **Coding Style**

74. See [File:Libero-formatter.xml](http://wiki.adempiere.net/File:Libero-formatter.xml) .
75. Do not use the conversion from Integer to int, Double to double and so on, because from java5 is doing autoboxing.
76. Allways use bracelets {}. It is improving code readability and can evict hard to detect bugs.
77. Don't use transaction names if is not necessary. Better put null.
78. Known issues:

    1. At present eclipse formatter is not supporting fluent interfaces \(see [eclipse bug \#196001](http://bugs.eclipse.org/bugs/show_bug.cgi?id=196001)\)

    **How to change parameters of existing method from ADempiere core**

79. ALWAYS keep the old method for backward compatibility and add the @deprecated tag in the javadoc of the method @deprecated since 3.5.3a. Please use {@link \#myMethod\(...\)} instead
80. Search for all places from ADempiere core where the old method is using and replace with the new one. In this way you will leave the old method with no calls in core and ready to be dropped after some releases.

    **How to use Adempiere Query class?**

    **How to return only ONE persistent object?**

81. ```text
    StringBuilder whereClause = new StringBuilder();
    		whereClause.append("AD_Client_ID=?");          // #1
    		whereClause.append(" AND AD_Org_ID=?");        // #2
    		whereClause.append(" AND C_AcctSchema_ID=?");  // #3
    		whereClause.append(" AND Account_ID=?");       // #4

     MAccount existingAccount = new Query(ctx, I_C_ValidCombination.Table_Name, whereClause.toString(), null)
     		.setParameters(new Object[]{AD_Client_ID, AD_Org_ID, C_AcctSchema_ID, Account_ID})
     		.first();
    ```
82. Use the interface to put the Table Name I\_C\_ValidCombination.Table\_Name
83. Use the StringBuilder when the **Where Clause** is built
84. Use the final String whereClause when the **Where Clause** is not built If you know that your query should return ONLY one result, then you can assert this, and use **firstOnly** method instead of **first** method:
85. ```text
     MAccount existingAccount = new Query(ctx, I_C_ValidCombination.Table_Name, whereClause, null)
     		.setParameters(new Object[]{AD_Client_ID, AD_Org_ID, C_AcctSchema_ID, Account_ID})
     		.firstOnly();
    ```

    **How to return ARRAY of objects?**

86. ```text
     public static MAchievement[] getOfMeasure (Properties ctx, int PA_Measure_ID)
     {
     	final String whereClause = COLUMNNAME_PA_Measure_ID+"=?"; 
     	List<MAchievement> list = new Query(ctx, I_PA_Achievement.Table_Name, whereClause, null)
     		.setParameters(new Object[]{PA_Measure_ID})
     		.setOrderBy(COLUMNNAME_SeqNo+", "+COLUMNNAME_DateDoc)
     		.list();
     	return list.toArray(new MAchievement[list.size()]);
     }
    ```

    **How to return ARRAY of objects and process elements?**

87. ```text
    public static MAchievement[] getOfMeasure (Properties ctx, int PA_Measure_ID)
    {
    	String whereClause = COLUMNNAME_PA_Measure_ID+"=? AND "+COLUMNNAME_IsAchieved+"=?"; 
    	List<MAchievement> list = new Query(ctx, MAchievement.Table_Name, whereClause, null)
    		.setParameters(new Object[]{PA_Measure_ID, true})
    		.setOrderBy(COLUMNNAME_SeqNo+", "+COLUMNNAME_DateDoc)
    		.list();
    	for(MAchievement achievement : list)
    	{
    	  s_log.fine(" - " + achievement);
    	  // do some processing here
    	}
    	return list.toArray(new MAchievement[list.size()]);
    }
    ```

    **How to return one member of an object?**

88. ```text
    	public static int getWindow_ID(String windowName)
            {
    	    int retValue = 0;
     	    String whereClause = COLUMNNAME_Name+"=?";
    	    MWindow win = new Query(Env.getCtx(), MWindow.Table_Name, whereClause, null)
    		  .setParameters(new Object[]{windowName})
     		  .first();	
     	     return = win.getAD_Window_ID(); 
            }
    ```

    **How to pass Timestamp parameter?**

89. ```text
    Timestamp dateAcct = ...;
    String trxName = ...;

    StringBuilder whereClause = new StringBuilder();
    		whereClause.append("C_CashBook_ID=?");				//	#1
    		whereClause.append(" AND TRUNC(StatementDate)=?");		//	#2
    		whereClause.append(" AND Processed=?");				//	#3
		
    MCash retValue = new Query(ctx, MCash.Table_Name, whereClause.toString(), trxName)
    	.setParameters(new Object[]{C_CashBook_ID, TimeUtil.getDay(dateAcct), true})
    	.first()
    ;
    ```

    **How to use Query class with complex where clause: EXISTS?**

90. ```text
    StringBuilder whereClause = new StringBuilder();
    	whereClause.append("C_Cash.AD_Org_ID=?");			// #1
    	whereClause.append(" AND TRUNC(C_Cash.StatementDate)=?");	// #2
    	whereClause.append(" AND C_Cash.Processed='N'");		
    	whereClause.append(" AND EXISTS (SELECT * FROM C_CashBook cb");
    	whereClause.append(" WHERE C_Cash.C_CashBook_ID=cb.C_CashBook_ID AND cb.AD_Org_ID=C_Cash.AD_Org_ID");
    	whereClause.append(" AND cb.C_Currency_ID=?)");			// #3
    MCash retValue = new Query(ctx, MCash.Table_Name, whereClause, trxName)
    	.setParameters(new Object[]{AD_Org_ID,TimeUtil.getDay(dateAcct),C_Currency_ID})
    	.first()
    ;
    ```

    **How to use Adempiere Callout class?**

91. For new callout code i always recomend to use GridTabWrapper class that is wrapping an GridTab object to an "persistent interface". For more info, there is an example on javadoc of the class. I am copy-paste here too:
92. ```text
 
    I_A_Asset_Disposed bean = GridTabWrapper.create(mTab, I_A_Asset_Disposed.class);  
    Timestamp dateDoc = (Timestamp)value;  
    bean.setDateAcct(dateDoc);  
    bean.setA_Disposed_Date(dateDoc);  
    ```

    Benefits:

    * cleaner code
    * write algorithms once \(and not 1 method for PO and other for GridTab\)
    * eliminate error prone strings

    **How to use PreparedStatement/ResultSet ?**

93. If you really need to use JDBC queries, then here is a template for that:

    ```text
     final String sql = "''your SQL SELECT code''";
     PreparedStatement pstmt = null;
     ResultSet rs = null;
     try
     {
          pstmt = DB.prepareStatement(sql, trxName);
          DB.setParameters(pstmt, new Object[]{...''parameters''...});
          rs = pstmt.executeQuery();
          while(rs.next())
          {
              ''// process fetched row''
          }
     }
     // If your method is not throwing Exception or SQLException you need this block to catch SQLException
     // and convert them to unchecked DBException
     catch (SQLException e)
     {
          throw new DBException(e, sql);
     }
     // '''ALWAYS''' close your ResultSet in a finally statement
     finally
     {
          DB.close(rs, pstmt);
          rs = null; pstmt = null;
     }
    ```

    **Always use DB.getSQLValue\*Ex**

94. DB.getSQLValue\*Ex methods which have same functionality as their counterpart but in case of an SQLException\(checked\) then a DBException\(unchecked\) will be thrown.
95. This will help us to assure data integrity and to distinguish between exceptions and null values. See: [FR 2448461 - Introduce DB.getSQLValue\*Ex methods](http://sourceforge.net/tracker/?func=detail&atid=879335&aid=2448461&group_id=176962)

    **Always use Trx.run methods**

96. If you want to run a fragment of code that is changing the database data, and if something if failing you need to rollback entire transaction or to rollback to a savepoint, then Trx.run methods are the best option:
97. Trx.run\(TrxRunnable r\) - creates a new transaction, runs the runnable object and if something fails then rollbacks the transaction and throw AdempiereException \(extends RuntimeException\). If all is ok, the transaction is commited.
98. Trx.run\(String trxName, TrxRunnable r\) - similar with previous run method, but instead of creating a new transaction it is creating a new savepoint.

    ```text
    Example 1:
        ...
        /**
         * saves the partner, user and employee
         */
        private void cmd_save()
        {
            Trx.run(new TrxRunnable() {
                public void run(String trxName) {
                    MBPartner bp = new MBPartner(getCtx(), bpartner_id, trxName);
                    bp.setValue(fValue.getText());
                    bp.setName(fName.getText());
                    if (bp.get_ID() <= 0) {
                        bp.setIsEmployee(true);
                    }
                    bp.saveEx();
                    ......
                }
            });
        }

    Example 2:
        ...
        /**
         * get Connection object
         */
        private void cmd_save()
        {
            Trx.run(new TrxRunnable() {
                public void run(String trxName) {
                    try
                    {
                        Trx trx = Trx.get(trxName, true);
                        conn = trx.getConnection();
                        ...
                    }
                    catch (SQLException e)
                    {
                        throw new AdempiereException(e);
                    }
                }
            });
        }
    ```

    **References**

    [EE Best Practices](http://www-128.ibm.com/developerworks/websphere/techjournal/0701_botzum/0701_botzum.html?ca=dgr-jw17Java-EE-Best-Practices)

    [Precise Java](http://precisejava.com/)

    **Sugesstion & Questions Coding Style**

99. When on a single thread class, StringBuilder should be used for String concatenation. If the class is not single threaded, then, StringBuffer should be used for String concatenation.

    **Testing Policy**

100. Submit your changes to local testing or a peer review before committing unless you are approved by 1st level committer
101. Publish your test results pls edit according to SF link findings above\)

     **Test Units**

102. The use of [FitnesseSlim](http://wiki.adempiere.net/FitnesseSlim) is thoroughly explored in [Cost Engine/Testing](http://wiki.adempiere.net/Cost_Engine/Testing) with a complete case [contribution](http://sourceforge.net/projects/adempiere/files/Adempiere%20Packages/CostEngineTesting.pdf/download).

     **Documentation Policy**

103. Document your sourcecode changes in this wiki under appropriate topic.
104. Solicit help from others if you cannot document well. Or just start a stub and allow others to expand it.
105. Intentionally hiding information may get your contribution categorised as proprietary and not fit for admission into trunk.
106. New features, windows or fields need help text at least in english.

     **Communication**

     **Bringing ideas \(or collecting votes\) for a development or bug fix**

107. open a discussion forum and try to keep the discussion in forums \(it can be in a tracker, but we have noticed that forums get much more attention than trackers\)
108. after the discussion ends in some proposal then open a tracker - and add a link in the comment to the forum THREAD \(to the thread, not to a single message\)
109. after tracker is opened try to keep the discussion on the tracker - unfortunately we cannot close the forum thread \(still, maybe in phpbb we can\)

     **When committing**

110. Try to keep all communication related to one theme in one single thread
111. Every commit must have a related tracker previously opened
112. It's recommended the commit message have a link to the tracker and a brief explanation of what was done
113. After the commit add a comment in tracker pointing to the review, it's recommended to add a link to the svn log
114. To make comments about code please use the tracker - this is to keep ALL information related in just one site

     1. Please avoid writing to the cvslog maillist - writing comments there is spreading related information, so people trying to follow history of an issue must review forums, then trackers, then maillist. This policy is trying to keep all information related and linked properly.

     **Lawful Vote and Review of Best Practices**

115. For more info please see [Project\_Charter\#Political](http://wiki.adempiere.net/Project_Charter#Political).
116. Review is now ongoing until 31st December 2008, where it is accepted and voted en bloc by the whole community in January 2009.
117. It has to be a full turn-out consensus vote first time round from the active common members in order for it to carry the weight of enforceable law.
118. Subsequent reviews shall be periodic minimally each quarter and not amended adhoc prior to review date.
119. Next review date should be not earlier than March 2009.

     **Mentor Policy**

120. All committers should also seek a mentor or coach among the senior committers already mentioned in the [Commit Committee](http://wiki.adempiere.net/Commit_Committee).
121. Mentees \(who are under Mentors\) have to assist in providing review and other administrative assistance \(this is due to resources constraints at the moment to manage the team\).

     **Adempiere Official Domains and Subdomains**

     **Fair use**

122. Some policies were proposed on this [thread](http://sourceforge.net/projects/adempiere/forums/forum/610546/topic/3426534):
     1. Money collected from these sites \(i.e. advertising\) must go to German Foundation and help to sustain the project
     2. Site sponsor, site seeder, and site maintainer can be advertised within a sponsors page and with a little box at the end of each page
     3. If there are zkwebui interface then some advertising links are allowed in the initial page
     4. Collecting visitor statistics must be made public for all community, or at least to project admins on request
     5. The sites must not collect user information - ask for registration - or anything about \(unless by the nature of the site it's needed\)
     6. No forums or support must happen on these sites - all support must be redirected to sourceforge forums
     7. No wiki must be set up on these sites - all documentation must be redirected to adempiere wiki
     8. The maintainer must be active, it the website becomes outdated more than one month then we must consider dropping the site, or calling for a new maintainer.
     9. Adempiere citizens can call for vote on closing a site if there are at least 3 persons that think it's being abused or not following fair use practices.
     10. Name of the subdomain must be previously discussed with community to reflect the goal and status of the site
     11. Citizens can ask to add or cut advertising on the subdomain sites \(via voting process\)

[Categories](http://wiki.adempiere.net/Special:Categories): [Community](http://wiki.adempiere.net/Category:Community) \| [Documentation](http://wiki.adempiere.net/Category:Documentation) \| [Code snippets](http://wiki.adempiere.net/Category:Code_snippets)

* [page](http://wiki.adempiere.net/ADempiere_Best_Practices)
* * [discussion](http://wiki.adempiere.net/Talk:ADempiere_Best_Practices)
* * [view source](http://wiki.adempiere.net/index.php?title=ADempiere_Best_Practices&action=edit)
* * [history](http://wiki.adempiere.net/index.php?title=ADempiere_Best_Practices&action=history)
* [Log in](http://wiki.adempiere.net/index.php?title=Special:UserLogin&returnto=ADempiere_Best_Practices)

**main links**

* [Home](http://wiki.adempiere.net/ADempiere_ERP)

**documentation**

* [Table of Contents](http://wiki.adempiere.net/Table_of_Contents)
* [Documentation](http://wiki.adempiere.net/Category:Documentation)
* [Tutorials](http://wiki.adempiere.net/Tutorials)
* [Development](http://wiki.adempiere.net/Development)
* [Technical HOWTOs](http://wiki.adempiere.net/Technical_HOWTOs)
* [Functional HOWTOs](http://wiki.adempiere.net/Functional_HOWTOs)
* [Training](http://wiki.adempiere.net/Category:Training_Course)
* [Features](http://wiki.adempiere.net/Features)
* [Concepts](http://wiki.adempiere.net/Category:ERP_concepts_and_functionalities)
* [Glossary](http://wiki.adempiere.net/Glossary)

**project links**

* [adempiere.net](http://www.adempiere.net/)
* [SourceForge.net](http://sf.net/projects/adempiere)
* [GoogleSearch](http://www.google.com/coop/cse?cx=016889972604713699431%3Avravql1hghw)
* [download](http://sourceforge.net/projects/adempiere/files/)
* [Support](http://sourceforge.net/projects/adempiere/support)
* [Track Bugs](http://wiki.adempiere.net/Bug_Triage)

**wiki help**

* [Community portal](http://wiki.adempiere.net/ADempiere_ERP_Wiki:Community_Portal)
* [Recent changes](http://wiki.adempiere.net/Special:RecentChanges)
* [Random page](http://wiki.adempiere.net/Special:Random)
* [Help](http://wiki.adempiere.net/Help:Contents)

**search**

**toolbox**

* [What links here](http://wiki.adempiere.net/Special:WhatLinksHere/ADempiere_Best_Practices)
* [Related changes](http://wiki.adempiere.net/Special:RecentChangesLinked/ADempiere_Best_Practices)
* [Special pages](http://wiki.adempiere.net/Special:SpecialPages)
* [Printable version](http://wiki.adempiere.net/index.php?title=ADempiere_Best_Practices&printable=yes)
* [Permanent link](http://wiki.adempiere.net/index.php?title=ADempiere_Best_Practices&oldid=54389)



* [Disclaimers](http://wiki.adempiere.net/ADempiere_ERP_Wiki:General_disclaimer)

## Source

Adapted from [http://wiki.adempiere.net/ADempiere\_Best\_Practices](http://wiki.adempiere.net/ADempiere_Best_Practices) by Michael McKay.

Original contributors:

1. Teo Sarca
2. Cristina Ghita Metas 
3. Trifon D3Soft
4. Victor Perez e-Evolution
5. Dominik Zajac BayCIX GmbH
6. Carlos Ruiz
7. Paul Bowden
8. Redhuan D. Oon

