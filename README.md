# xM Link - SNOW
This is an update set in service now that will allow for quick and easy set up of custom integrations with any table in service now.

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites
* Service Now
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files
* [xm_Link_update_set.xml] - This is the xml update set that needs to be imported into your service now instance.

# How it works
This integration uses 2 tables, 2 script includes and 2 (or more) business rules depending. 
Table 1: xM Condition - this table is where you will build conditions out and point to a table you want to create xMatters notifications off of. That table will also need a business rule (see example business rule in the application and copy that business rule onto whatever table you want to be watching)
Table 2: xM Outbound Queue - this table is where the paylaod is sent when it is ready to be sent to xMatters. an ASYNC business rule will pick it up on insert and send the payload (flat record off the table we are watching) to the specified xMatters endpoint.
Script Include 1: xM Condition Processor - code for processing the record and building the payload to be send to the outbound queue table.
Script Include 2: xM Send Payload - buildes a ServiceNow Rest Message v2 object and sends the payload to xMatters.
Business rule 1: ASYNC business rule running on the outbound queue table that triggers the Send Paylaod script include.
Business rule 2,3,4,...: The business rule that goes on whatever table you want to be watching. See example business rule included in the update set and copy exactly onto whatever table you want.

# Installation
Import xml on any list view in service now. Select the update set file from this repository (download it first).
Once imported, verify by going to remote update sets and making sure the application is there. (this may need work my dev instance wasn't letting me publish my application)
