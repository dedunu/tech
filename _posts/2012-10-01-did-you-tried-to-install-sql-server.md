---
layout: post
title: Did you tried to install SQL Server 2012 on Windows Server 2012?
---

Recently I tried to install SQL Server 2012 in Windows Server 2012 box. Unfortunately, it was not easy to do that for me because setup generated few errors. And then it displayed that .NET Framework 3.5 SP1 Feature was not able to activate. 

There were few reasons to occur that problem.
- Windows Server 2012 was not activated.
- Windows Server 2012 was unable to access the internet (When it is activated).

So first I realized when I tried to manually activate this feature, that I have to activate my Windows Server 2012. Then I activated my Windows Server 2012. Then I again tried to activate .Net Framework 3.5. But unexpectedly again I got failed. Then I checked what was wrong with my computer and why this installation got failed although I had inserted the installation media.
The error was like this.

Then I found on the internet that we have to show the path of the binaries to activate this feature.

1. Then I opened Server Manager and then Manage –> Add Roles and Features.

2. I followed the wizard normally.

3. Then I selected .NET Framework 3.5 from features window.

4. Then I got this dialogue box.

5. But be careful and don’t click “Install”. If you click Install it will look up for internet connection. If there is no internet connection it will fail your setup.  Click on “Specify an alternate source path”.

6. And then give your installation media folder plus “`\sources\sxs`”. It may be a share or DVD no matter whatever it is. Then Click OK and Install. It will activate .NET Framework 3.5 on your Server 2012 installation.

I found those pictures from sqlcoffe.com. And I saw that he has also tried in this way and get failed because he hasn’t specified the path of installation media. But he has an alternate method. I'll share it here too.
He had opened a cmd window. and had typed this command.

```
dism /online /enable-feature /featurename:NetFx3 /source:d:\sources\sxs
```
You can replace “`d:\sourced\sxs\`” with your path of installation media. Then I tried to install SQL Server 2012. Installation was successfully finished.

Reference: [http://www.sqlcoffee.com/Troubleshooting101.htm](http://www.sqlcoffee.com/Troubleshooting101.htm)

### Tags

- SQL Server 2012
- English
- SQL Server Installation
- Installation
- SQL Server
- Windows Server 2012