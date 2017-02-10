# verify_config_files

These JSON files can be used to set up a central location for information to be used in Verify reporting python scripts 
The files contain:
- names of Verify services 
- Google sheets and tabs names to push the data to
- file to make it easier to change a RP URL to RP name 
- file to use page titles for segmenting using PIWIK

You need these files before you can run the scripts relying on this information. 

Clone the repository one level up from your script folder

```
git clone git@github.com:zilnhoj/verify_config_files.git
```

# Updating the files

Everytime a new services is added to verify that you need to report on you need to update these files 

Before you make any changes to the files:
- in terminal change directory, cd, to the config folder
- create a new Git branch i.e. git checkout -b branch-name
- follow the instructions below

## Updating sheet_tab_names.json

This file sets the Google sheet and tabs names for where the final data set will be sent to

Create a Google sheet using the format
- name to be called the name of the service [RP]
- two tabs in the sheet to be called Performance Measures and Funnel 

To update the file
- copy one of the entries
- paste to to the end of the file just before the closing curly brace
- make sure it is separated from the previous entry with a comma
- change the service name and Spreadsheet_name to the name of the new service RP - it must match the name of the spreadsheet youa are sending the data to
- save the file

```JSON
"BIS RP":{
		"Spreadsheet_name":"BIS RP",
		"tabs":["Performance Measures - Weekly","Funnel"]
	},	
```
## rp_mapping.json
In the raw data csv file each services is referred to by it's URL.  This is not very human readable.

This file is used to map the URL for the service to the service name.  

To update the file:
- copy a previous entry 
- paste it at the end of the file just before the closing brace
- change the url to the url of the new services
- change the name to the name of the new servcie - it has to be the same as the name you have used in the sheet_tab_names.json file
- make sure you separate this entry with the previous entry by using a comma
- save the file

```JSON
"https://www.ruralpayments.service.gov.uk" : "DEFRA RP",
```

## servcies.json

This file contains the names of all the services 

To update the file:
- copy one the entries
- paste it to the end of the file just before the closing brace
- change the key to the name of the service - has to be the same as used in the other files
- change the value to the name of the service - it has to be the exact same as the the segment name for the service that has been set up in PIWIK
- make sure you separate this entry with the previous entry by using a comma
- save the file

```JSON
"BIS RP" : "BIS RP",
  "DVLA VDL" : "DFT DVLA VDL",
  "DVLA F2D REPORT": "DFT DVLA F2D REPORT",
```

## pages.json

This file maps the page title needed to segment data in PIWIK
You probably will not need to make a change to this file but if you do 

- copy one the entries
- paste it to the end of the file just before the closing brace
- change the key to the name you will use to reference the page title
- change the value to the page title of the stage of the journey you are segemting on- make sure you separate this entry with the previous entry by using a comma
- save the file

Once you are finished all the changes locally you can run your script and it should pick up the new servcies for the report 

# Push changes 

To make sure that this is the canonical source for the config files push your changes as normal back to the repository

to do this type:
git add . <return>
git commit -m "your descriptive commit message" <return>
git push origin <branch-name>

Let one of your colleages know that there is a pull request waiting and they can merge it for you
Once the changes are merged return to your master branch and pull the changes to your locel machine

git checkout master
git pull

