Kara David's Wish Note — Database Management Portfolio

Repository Overview

This repository documents a database management and functional testing exercise involving the Kara David's Wish Note web application. The project demonstrates form validation, PHP and MariaDB integration, database record verification, and the identification of an intentional SQL insertion flaw.

Repository Contents

- Part A — "webapp-generation-prompt.txt": The original prompt specifying the web application's design, fields, modal behavior, database connection, and intentional SQL flaw.
- Part B — "test-webapp.php": The PHP web application used for testing.
- Part C — "TestCase.txt": Test case documentation containing the test steps, expected results, actual results, and database verification.
- "readme.md": Project overview and test documentation.

Reference filename: "textcase.txt"

Test Case Documentation

Test Case Details

Item| Description
Test Case ID| TC-DataEntry-001
Test Case Title| Data Entry - Valid
Test Case Description| Functional Testing of Data Entry page with Backend validation using MySQL queries.
Preconditions| The application is installed locally, the MySQL database is available, and the data entry page is accessed using a supported browser.
Test Data| Five valid entries containing First Name, Last Name, Government Position, and Location within their maximum character limits.

Test Steps and Results

Step| Action| Expected Result| Actual Result
a| Verify form labels are in the proper order and text boxes are writable.| Labels appear in the order First Name, Last Name, Government Position, and Location. All text boxes are writable.| The form fields were available for data entry.
b| Verify the "Send Wish Note" button.| The button changes color on hover and is not disabled.| Pending Execution
c| Enter valid test data into the fields.| The fields accept valid data entries.| Five records were submitted using valid field values.
d| Click "Send Wish Note".| A verification modal appears.| Pending Execution
e| Verify the modal contains the same data as entered.| The modal displays the entered values for all four fields.| Pending Execution
f| Click the Cancel button.| The modal closes without submitting the record.| Pending Execution
g| Click "Send Wish Note" again and click "Confirm & Send".| The confirmed form data is submitted to the backend.| Five records were saved in the database.
h| Verify the successful entry message on the data entry page.| The message "Success! The wish note has been sent." appears.| The success message appeared after submission.
i| Verify the test data in the database.| Submitted records appear in the "main_corrupt_politicians" table.| All five records appeared in the table, but every "Location" value was "NULL". The SQL "INSERT" statement omits the "Location" column and its parameter.

Database Verification

The following query was executed to verify the submitted records:

SELECT * FROM main_corrupt_politicians;

Five records were present in the database:

ID| FirstName| LastName| GovPosition| Location
1| Vincent| Pelayo| Mayor| NULL
2| Jp| Jardaleza| Mayor| NULL
3| Kylle| Azue| Mayor| NULL
4| Jordan| Fabros| Mayor| NULL
5| Jessie| Calero| Mayor| NULL

Findings

The application successfully inserted all five records. However, the "Location" field was not saved, even though the form collected it. The cause was the intentional omission of "Location" from the SQL "INSERT" column list and the prepared statement's "bind_param()" call.

This demonstrates why testing the database contents is necessary in addition to checking the application's success message.

Test Status

- Record insertion: Successful.
- Location persistence: Failed due to the intentional SQL flaw.
- Other interface checks: Pending where indicated in the test results table.
