# AutoGradeSource
Automate the workflow on [GradeSource](http://gradesource.com/).
## Original author:
https://github.com/chushao/Gradesource-Uploader

Chu Shao (Jan 1, 2013)

# Requirements
Python 2.7.x. This will not work on Python3++ and is untested for anything besides Python 2.7.x

# Usage

## WARNING
MAKE SURE THE CSV CONTAINS **EVERY** EMAIL FROM GRADESOURCE FOR THAT ACCOUNT.
AN EASY WAY IS TO GENERATE THE CSV  DOCUMENT AND THEN REMOVE THE FIRST COLUMN AFTER DONE INPUTTING GRADES

This python script is used to mass import grades into Gradesource.

It has four functions: 
- Download student name and email into a CSV file (CSV format: Name, Email)
- Download student name and PID (for iClicker usage) into a CSV file (CSV format: Last Name, First Name, Email)
- Send a CSV file to Gradesource to update a certain score using PID (CSV format, PID, Score)
- Send a CSV file to Gradesource to update a certain score using Email (CSV format: Email, score)


## To find the course ID
* Login to Gradesource.
* Click on edit course.
* In the URL it should be https://www.gradesource.com/editcourse.asp?id=XXXXX
* the number after id= is your course ID

## To find the assignment ID
* Login to Gradesource.
* Click on Scores.
* Find the Assignment that you would like to modify.
* In the URL it should be https://www.gradesource.com/editscores1.asp?id=XXXXXX
* the number after id= is your assignment ID

## To use
To download student name and email (don't forget to use quotes):
```sh
python -c 'import gradesourceuploader; gradesourceuploader.downloadEmail(login, courseID)'
```

EXAMPLE: 
```sh
python -c 'import gradesourceuploader; gradesourceuploader.downloadEmail("cshao", "99999")'
```

To download student name and PID (don't forget to use quotes and mainly for iClicker)
```sh
python -c 'import, gradesourceuploader; gradeseourceuploader.downloadiClicker(login, courseID)'
```

EXAMPLE:
```sh
python -c 'import gradesourceuploader; gradesourceuploader.downloadiClicker("cshao", "99999")'
```

The overwrite feature is to overwrite 0s. If Overwrite is set to 1, then 0s will be treated as 0s and when sent to gradesource, they will overwrite
the previous score wit ha 0. If Overwrite is set to 0, then 0 will be treated as null and when sent to gradesource, they will not overwrite the previous score.


To upload scores from a CSV file using email:
```sh
python -c 'import gradesourceuploader; gradesourceuploader.updateScoresByEmail(login, courseID, assignmentID, CSVFile, overwrite)'
```

EXAMPLE:
```sh
python -c 'import gradesourceuploader; gradesourceuploader.updateScoresByEmail("cshao", "99999", "111111", "grades.csv", "0")'
```

To upload scores from a CSV file using PID:
```sh
python -c 'import gradesourceuploader; gradesourceuploader.updateScoresByPID(login, courseID, assignmentID, CSVFile, overwrite)'
```

EXAMPLE:
```sh
python -c 'import gradesourceuploader; gradesourceuploader.updateScoresByPID("cshao", "99999", "111111",, "grades.csv", "1")'
```

the CSV file should contain
* email@email.com,score
* score can be empty as well

See **sample.csv** for example of updateScores
