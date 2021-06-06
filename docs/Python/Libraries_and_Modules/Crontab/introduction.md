# Python-Crontab

![Crontab](images/Crontab_logo.svg){: .center}

1. [pip page](https://pypi.org/project/python-crontab/)
2. [Gitlab](https://gitlab.com/doctormo/python-crontab)

##Description

Crontab module for reading and create cronotab files and accessing the sytem cron with and easy API

> The special character "W", "L", "#", and "?"" is not supported. 

| Field Name | Mandatory | Allowed Values | Special Characters | Extra Values |
|:-----------|:---------:|:---------------|:------------------:|:------------:|
|Minutes	 | Yes	     | 0-59	          | * / , -	           | < >          |
|Hours		 | Yes		 | 0-23			  | * / , -	           | < >          |
|Day of month| Yes	     | 1-31	          | * / , -	           | < >          |
|Month	     | Yes	     | 1-12 or JAN-DEC| * / , -	           | < >          |
|Day of week | Yes       | 0-6 or SUN-SAT | * / , -	           | < >          |

## Installation
```
pip install python-crontab
```
## Crontab Syntax

The specific syntax to define the schedule consist of five field

```
Minute Hours Day Month Day_of_the_Week
```

as mentioned about the fields can have the following values
```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23) 
│ │ ┌───────────── day of month (1 - 31)
│ │ │ ┌───────────── month (1 - 12)
│ │ │ │ ┌───────────── day of week (0 - 6) (Sunday to Saturday;
│ │ │ │ │                                       7 is also Sunday on some systems)
│ │ │ │ │
│ │ │ │ │
* * * * *  command to execute
```

We can make more complex configuration if we make use of special characters 

| Character   | Meaning                        |
|:------------|:-------------------------------|
|Comma		  | To separate multiple values    |
|Hyphen		  | To indicate a range of values  |
|Asterisk	  | To indicate all possible values|
|Forward slash|	To indicate EVERY              |

> For example: 
`0 16 1,10,22 * *` tells cron to run a task at 4 PM (which is the 16th hour) on the 1st, 10th and 22nd day of every month.  

## Access to Crontab

There are 5 ways to access, there are 3 that work just in Linux and the other two will work in windows 

**Linux**
1.
```Python
from crontab import CronTab

cron = CronTab(user='username')
```
2.
```python
from crontab import CronTab

cron = CronTab()
```
3.
```python
from crontab import CronTab

cron = CronTab(user=True)
```

**Windows and other systems**  
4. 
```python
from crontab import CronTab

cron = CronTab(tabfile='filename.tab')
```
where `filename.tab` is a file containing the task.  

5.
```python
from crontab import CronTab

cron = CronTab(tab=""" * * * * * command""")
```

## Create A new Job

We can create this jobs in different ways, two main are, with the commands and with commands plus comments

```python
cron.new(command='my command')
```
now with a comment
```python
cron.new(command='my command',
		comment='my comment')
```

so a complete example will be 

```python
from crontab import CronTab

cron = CronTab(user='username')
job = cron.new(command='python test.py')
job.minute.every(1)
cron.write()
```
and the test file
```python
from datetime import datetime

my_file = open('append.txt', 'a')
my_file.write(f'append {datetime.now()}')
```

## Setting restrictions

| Restriction                     | Description                   |
|:--------------------------------|:------------------------------|
| `job.minute.every(<minutes>)`   | Set minutes `<minutes>` (0-59)|
| `job.hour.every(<hours>)`       | Set hours `<hours>` (0-23)    |
| `job.dow.on(<day_of_the_week>)`, `job.dow.on(<day_of_the_week>,<day_of_the_week>)`  | Set day of the week `<day_of_the_week>` ('MON','SAT', etc)|
| `job.month.during(<month>)`,`job.month.during(<month>,<month>)`| Set month `<month>` ('JAN', 'FEB', etc)|

Every time we set a time restriction we cancel the previous one thus

```python
job.hour.every(1)
job.hour.every(15)
```	

the value set will be 15 instead of 1
in order to add restriction to a previous one 

```python
job.hour.every(1)
job.hour.also.on(15)
```

In some case we want to set up one filed and make the other field to 0, we can do something like:

```python
job.every(15).hours()
```
This will set the schedule to `0 */4 * * *`. 
> Similarly for the 'day of the month', 'month' and 'day of the week' fields.  

## Set job to work every reboot

```python
job.every_reboot()
```

## Clean the restrictions

```python
job.clear()
```

## Enable and disable jobs

To enable the job
```python 
job.enable()
```

To disable the job
```python
job.enable(False)
```

To check if the task is enable

```python
job.is_enable()
```

## Checking validity

```python
job.is_valid()
```

## Finding a job

Finding by the command name
```python
cron.find_command("command name")
```

Finding by the comments
```python
cron.find_comment("comment")
```

Finding according the time
```python
cron.find_time(time schedule)
```

## Remove the jobs

```python
cron.remove(job)
```

remove base in the comment 

```python
cron.remove_all(comment='my comment')
```

or remove all
```python
cron.remove_all()
```

## Environment Variable 

We can define environment variables 

```python
job.env['VARIABLE_NAME'] = 'Value'
```

to get the variables

```python 
job.env
```



























