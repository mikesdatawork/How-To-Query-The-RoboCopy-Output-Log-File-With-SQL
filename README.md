![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# How To Query The RoboCopy Output Log File With SQL
**Post Date: November 27, 2015**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's some SQL logic to help you query the RoboCopy output log file. Remember; you can query most things using an XML output so for this to work with the log file (or most text files) simply bulk insert the contents into a table, and query the table. Remember to use FOR XML PATH(''), TYPE.</p>      


## SQL-Logic
```SQL
use master;
set nocount on
 
if object_id('tempdb..#robocopy_output') is not null
drop table #robocopy_output
create table #robocopy_output
(
[output] varchar(max)
)
BULK INSERT #robocopy_output
FROM 'e:load_etls_source_backupsrobocopy_log_for_load_etls_MyDatabase_01.log'
WITH
(
fieldterminator = 't'
, datafiletype = 'char'
--, fieldterminator = ','
, rowterminator = 'rn'
);
 
select * from #robocopy_output for xml path(''), type
```
Here's what the query will look like in most cases for RoboCopy log.

![RoboCopyLog With SQL]( https://mikesdatawork.files.wordpress.com/2015/11/image001.png "Create RoboCopy Log With SQL")
 
Once you click on the XML link output you'll see the RoboCopy output file as usual. Just like you would if you clicked on the .log file from the OS.

![Read RoboCopy Log With SQL]( https://mikesdatawork.files.wordpress.com/2015/11/image002.png "Read RoboCopy Log With SQL")
 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

 
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

