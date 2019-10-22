# JumpCloud-Password-Hashing-Assignment
Test Plan and Test Case documents for the Password Hashing Assignment

Application URL:
http://127.0.0.1:8088/hash

Requirements:
Password Hashing Application Specification:

The following is the requirement specification that was used in building the password hashing
application. It describes what the application should do.

   ● When launched, the application should wait for http connections.
   
   ● It should answer on the PORT specified in the PORT environment variable.
   
   ● It should support three endpoints:
   
○ A POST to /hash should accept a password. It should return a job identifier
immediately. It should then wait 5 seconds and compute the password hash.
The hashing algorithm should be SHA512.

○ A GET to /hash should accept a job identifier. It should return the base64
encoded password hash for the corresponding POST request.

○ A GET to /stats should accept no data. It should return a JSON data structure
for the total hash requests since the server started and the average time of a
hash request in milliseconds.

● The software should be able to process multiple connections simultaneously.

● The software should support a graceful shutdown request. Meaning, it should allow any
in-flight password hashing to complete, reject any new requests, respond with a 200 and
shutdown.

● No additional password requests should be allowed when shutdown is pending.

Sample Curl rquests and reponses from command prompt:

To GET the stats:
    curl -X GET http://127.0.0.1:8088/stats
    
    Response: {"TotalRequests":0,"AverageTime":0}
    
 To POST data to hash end point: 
 
    curl -X POST -H "Content-Type: application/json" -d {\"password\":\"Password\"} http://127.0.0.1:8088/hash
    
    Response: 1
    
 To GET the hashed password for the id provided (1 in this example)
 
    curl -X GET http://127.0.0.1:8088/hash/1
    
    Response: 5sg7KCrrLgIoRFlXIcwAu9pHyyRTfBd5+buE8EA54Wdua6hXPliNoQUlEOOqCjKp5Vh5riKwwtYhNvwKPoX4uw==
    
    
 To shut down the application server:
 
    curl -X POST -H "Content-Type: application/json" -d shutdown http://127.0.0.1:8088/hash
    
 Execution:
 Download all the files provided in the requirements doc for either LINUX or Windows.
 
 Note: I used Windows 10 to execute and test the application.
    
