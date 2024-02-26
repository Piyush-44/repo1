<h3>Prerequisites</h3>
1.)Config file <br />
Add valid credentials for for Oracle or Snowflake DB in db_credentials <br />

<code>
ORACLE_USER= <br />
ORACLE_PWD= <br />
ORACLE_DSN= <br />
</code>
 
<h3>UPDATE THE paths</h3> <br />
Modily the file with the suitable absolute paths where the raw data is present and where it should be moved into once the operation is completed. <br />
For Eg. data_processed_path = C:\Users\abc\PycharmProjects\data_processed <br />
        where data_processed directory containg sub directories such as Interaction, InteractionHistory, Notes etc.

<h3>topics to fetch the data</h3>
in the config file update the "topics_to_read" attribute, telling the script from which topics to fetch the data from
3.) <h3>Install Packages</h3>
Install all the packages imported in the snowflakeAndOracle.py file. <br />

<code>
pip install -r requirements.txt
</code>

4.)<h3>How to Create the templates</h3> <br />
Create a json file with file name similar to the topic name that's present in the data directory. <br/>
For Ex:<br/> 
![Scheme](images/img1.png) <br/>
So the name of the template can be Email.json, Work.json, WorkHistory.json<br/>
<code>
{   "DB": "ORACLE",
    "TABLE": "TEST_WORK",
    "STAGE": "TEMP_TEST_WORK",
    "ACTION": "UPSERT",
    "PRIMARYKEY": ["PEGA_CASE_ID","REQUEST_ID"],
    "COLUMN_NAME": [
        {
            "PEGA_CASE_ID": [
                "PEGA_CASE_ID"
            ]
        },
        {
            "REQUEST_ID": [
                "REQUEST_ID"
            ]
        },
        {
            "DATETIMEVAL1": [
                "DateTimeVal1"
            ]
        },
        {
            "CASETYPE": [
                "CaseType"
            ]
        },
        {
            "ASSIGNEDWORKBASKET": [
                "AssignedWorkBasket"
            ]
        },
        {
            "EDWDATAPAGE": [
                "EDWDataPage"
            ]
        }
    ]
}
</code> <br/>
In the above sample of code, DB represents the Database in which we're entering our filtered data into.<br/>
Make sure to have Table to store the data and update the table name into "Table" attribute in the template. "Action" determine whether you want to only insert into the table or update the data if exists and if not insert, followed by the Primary key determining on what conditions are we trying to UPSERT the data, atleast 1 key is required. <br/>
"Column_Name" consists of key value pair where key represents the name represented in the database, where the value(s) represents the equivalent to attributes in the data
5.)<h3>Run the Code</h3>
In Terminal
<h4>In windows</h4>
python BPADataLoad.py env

<h4>Linux</h4>
python3 BPADataLoad.py env