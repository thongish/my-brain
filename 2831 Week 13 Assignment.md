Kevin Pham
A01026954

### Use Case Diagram:

![[Drawing 3.png]]






### Fully dressed use case:

|                                            |                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Use Case Title:**                        | Submit Assignments                                                                                                                                                                                                                                                                                                                                                                 |
| **Primary Actor:**                         | Student                                                                                                                                                                                                                                                                                                                                                                            |
| **Pre-condition(s):**                      | 1. Student is logged into the LearningHub system<br>2. The assignment submission window is open<br>3. The student hast the necessary files prepared for upload                                                                                                                                                                                                                     |
| **Success Scenario:**                      | 1. Student navigates to course page<br>2. Student selects the relevant assignment from the list<br>3. The system displays the assignment submission page<br>4. Student uploads the required files<br>5. Student clicks "Submit" button<br>6. The system validates the file format and size<br>7. The system confirms successful submission with a timestamp                        |
| **Extensions or <br>Alternative Flow(s):** | **Invalid File Format/Size:**<br>1. The system displays an error message if the uploaded file does not meet the format/size criteria<br>2. The student selects a new file and retries submission<br><br>**Late Submission:**<br>1. If the deadline has passed, the system displays a warning message<br>2. The student can still submit, but the submission is flagged as late<br> |
| **Post-Conditions:**                       | 1. The assignment submission is recorded in the system with a timestamp<br>2. The student receives a confirmation notification                                                                                                                                                                                                                                                     |
### Assumptions:
- The LMS supports role-based access for Students, Instructors, and Administrators
- File uploads can have predefined acceptable formats and size limits
- A timestamp feature ensure tracking of submission times

# Resources
- Week 13 slides
- Chatgpt helped with diagram and fully dressed use case