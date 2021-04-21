# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. PDF report generator which converts telemetrics in csv to pdf format.
3. List of receipients to send email notification.
4. Breach limit information
5. Record trend measurement limit.
6. Real time clock measurement.

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|------------------------------------------------------
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | YEs           | CSV has been succesfully converted to pdf
Counting the breaches       | YES           | Track everytime breach occurs using a global counter
Detecting trends            | YES           | Time stamp information for detected trend
Notification utility        | YES           | Email notification is triggered when breach occurs.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Test to track the breaches.
4. Test for email notification for all recipients only when breach occurs.
5. Time stamp added is in sync with system time.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | PDF file     | Email alert                 | Fake the sending of emails
Report inaccessible server |Access to server| email alert               | Fake the sending of emails
Find minimum and maximum   | csv file       | min and max values        |  None - it's a pure function
Detect trend               | time limit to detect trend | time stamp for trend detected| None - it's a pure function
Write to PDF               | csv file    | pdf file                    | csv to pdf convertor
