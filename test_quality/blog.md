# Why should one extend sys_user table? #

This is something I encountered in a project where custom application was built for Social & Health Care sector. 

Frankly, I can't come up with a good reason. 

Initially I had a thought that having application's users in a separate table would simplify data security configurations. However, even though one would set well thought out ACL structure for extended user table, the users in the extended table would still be found in sys_user, and the contents would be available through sys_user ACLs.

Also things would start to get messy when wanting to filter data utilizing custom table columns. Many base tables have references to sys_user. If one would try to build a report on a table that references sys_user, it would not be possible to dot walk into custom fields created to extended table.

I can think of only benefit for custom tables in this situation, and that would be being able to set the security rules for the additional columns created for the exteneded table. But I don't believe that is a common use case or that it would be worth the more complex architecture.

Rather add more columns to sys_user in custom application scope, and utilize view rules and ACLs to achieve the desired end result.