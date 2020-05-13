# DigitalRisksTest

Contraints:
Environment - I do not have an environment that allows me to pull data from an API and parse it using what I think would be the best tool, spark. I have had to therefore split the test into what I could get done  in a couple of hours. 

DigitalRisksAPI.py - This is a local API get script that connects to the event store and pulls the json data for each of the events. A file is created locally for each event.

Manual work - Due to the constaints with environments as stated above, I then moved the files to S3 where I could access them using my spark environment. 

DigitalRisks.py - This is an unfinished script, due to time contraints. It parses the json data into a dataframe which I then select the relevant column and write to a table. The simple table structures that I went with are below. 

CREATE TABLE quote (quoteId string)
CREATE TABLE quote_item (quoteId string, productname string, status string)

Issues - I took too long to decide to do the manual move of the files I created. This left me with any time to pull the data into the tables and perform some queries on them. I also ran into an issue with the number of nodes in the JSON object and not being able to return the value of the status. I solved it eventually with explode, but I do not think this is the most elegant solution. 

Happy path - If I had the environmnet and I had no time constraints, I would like to use spark. I enjoy using databricks as an environment as it is built on spark. I would pull the data directly into S3 using spark (firewall issues forbade this) and then use sparks read.json functionality to its fullist and parsing the data into tables for querying. 

Queries - The main data tables would contain all the data on the quotes, but queried to only return the active products. Window functions would be used to get the latest status for each product and quote so as to have the most up to date data. 

Further demographic analytics could be done on the data as it contains locations, jobs, ages and salaries etc. 

Who will be consuming this data? I have a question on GDPR compliance and PII data being available to everyone, as this increases the risk of data leakage. With the type of data available this would need to be an issue solved as a priority. If the data is siloed then its less of a risk, but if self service is intended then that would pose a greater risk.
