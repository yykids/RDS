## Database > RDS for MySQL > Release Notes

### January 19, 2021
#### More Features
- Added an option used to configure Ping Interval (the master instance checking interval) when using High Availability (HA).
- Added a feature to pause/resume High Availability (HA)
- Added a feature used to configure the access control direction (inbound/outbound) in the **Access Control Settings** dialog box
- Changed so that t2.c1m1 Flavor cannot be created anymore.
- Changed so that the existing instances created with t2.c1m1 Flavor can no longer be switched to High Availability (HA).


### December 15, 2020
#### More Features

- Added a function that enables users to set the --ftwrl-wait-timeout option value


### November 10, 2020
#### Bug fixes
- Fixed the issue where automatic backup generation would occasionally fail
- Fixed the issue where automatic deletion of expired backup would occasionally fail


### October 13, 2020

#### Bug Fixes 

- Fixed an issue in which innodb_buffer_pool_size cannot be modified as intended
- Fixed failed copy of the ha candidate master instance, when the require_secure_transport is on
- Fixed delays in the backup of large-scale instance

### September 22, 2020

#### More Features

- New region opened in Korea (Pyeongchon) 

### September 15, 2020

#### More Features 

- Supports Monitoring API 

### August 11, 2020

#### Bug Fixes

- Fixed an issue in which an invalid subnet appears on the list when user VPC subnet is unavailable 

### July 14, 2020

#### More Features 

- Further supports MySQL 8.0.18  

### December 10, 2019

#### More Features

- Added the feature of database file encryption (Korea Region)

### November 12, 2019 

#### Feature Updates

- Updated failure detection and restoration of candidate master 

#### Bug Fixes

- Fixed infrequent backup failures 

### September 24, 2019 

#### Feature Updates 

- Improved speed for creating an instance (About 28 minutes -> 13 minutes, for HA instances)
- Updated UX to allow new backups for time restoration, at the restart by using failover 
- Changed UI for enabling default alarm 

### August 13, 2019

#### Feature Updates

- Allowed to view event logs related to high availability more intuitively 

#### Bug Fixes

- Fixed the occasional failure in creating or restoring database instances
- Fixed failed delivery of mails, notifying the deletion of database instances 

### July 23, 2019

#### More Features

- Default Alarm added
- Monitoring Item added

#### Updates

- Backup-related events no longer support alarms.

### June 27, 2019

#### More Features

- Japan Region added

### June 25, 2019

#### More Features

- High Availability added

#### Updates

- Event period exposed on the page of instance details changed from 1 day to 7 days

#### Bug Fixes

- Point-in-time recovery is available from when restoration is possible.

### May 14, 2019

#### Updates

- Stronger authentication when instance is created or modified
- Added UX to select/unselect all notification events

#### Bug Fixes

- Fixed instances, which were sometimes unavailable to be deleted while they were being created
- Fixed the issue in which data volume was not properly changed when data storage was full

### March 12, 2019 

#### Feature Updates 

- Updated error messages that are vague with unpleasant looks. 
- Updated to allow modifying transaction-isolation on the console 

#### Bug Fixes

- Removed the probability of long backup time which may take more than a day for 1TB database

### February 26, 2019 

#### More Features 

- Added the feature of SSD volume as storage for instance data  

#### Feature Updates 

- Updated to set recipients of notification from project members 
- Updated features for x1, u2 flavor 

### January 29, 2019

#### Feature Updates

- Changed the maximum instance volume to 1000G 

### December 14, 2018

#### Bug Fixes 

- Fixed failed exposure of r2.c8m64  
- Fixed general logs that are not visible 
- Fixed bugs in the VPC subnet selection 

### December 11, 2018 

#### Feature Updates 

- Removed the peering feature 
- Feature updated to the method of network communication by using user VPC subnet  

### October 23, 2018 

#### Feature Updates 

- Shows description message for input items when instance is created/restored/replicated 
- Shows the mysql transaction_isolation option 

### October 16, 2018 

#### More Features 

- Added the feature of changing instance flavor 
- Added the feature of extending instance storage 

### August 28, 2018

#### More Features 

- Allows to secure instance volume by deleting binary log files 

### July 24, 2018

#### More Features

- Also supports MySQL 5.7.15 

#### Bug Fixes

- Fixed an issue in which an instance of the MySQL 5.7.19 version cannot be created, without floating IP 
- Fixed auto backups at particular situations, in which it takes twice the usual time 

### May 29, 2018

#### More Features

- Newly supports MySQL 5.7 

### April 24, 2018

#### Feature Updates

- With port change of the master, the master access information is automatically changed for read only slave
- Delete unnecessary logs after backup 

#### Bug Fixes

- Fixed pagination, in which Search Result > Create instance takes you to the search result page 
- Fixed the missing of a warning sign when it is tried to create an instance with Confirm Password left in blank 

### March 22, 2018 

#### Bug Fixes

- Fixed an issue in which backup retention period remains on the list, even after it was changed to 'N/A'
- Fixed the bug in which instance status shows Changing, even without instance setting updated 
- Fixed an issue in which QPS shows as negative number when an instance restarts 
- Fixed the bug in which only data is updated without date or time updates, at the click of Period Setting on the Monitoring page 

### February 22, 2018 

#### New Releases 

- TOAST Cloud Relational Database Service (RDS) provides Relational Database in the cloud environment. 
- No complicated configuration is required to enable relational database. 
- Supports MySQL 5.6.33.  
