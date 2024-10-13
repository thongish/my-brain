# Script

Slide 1:
- In this section of the presentation we'll be going over a brief description of each implementation methodology, why we don't recommend certain methodologies, and why we recommend Phased implementation

Slide 2:
- The 4 implementation methodologies we'll be discussing are direct cutover, pilot implementation, parallel operation, and phased implementation
- Direct Cutover is where the old system is made unavailable and users start using the new system immediately

Slide 3:
- Pilot implementation is where a small group of users adopt the new system before the rest of the user base

Slide 4:
- Parallel operation is where both the old and new systems are used simultaneously for as long as the new system is being tested

Slide 5:
- Phased implementation is where features of the new system are slowly introduced into the old system, replacing the old features, if any

Slide 6:
- So why didn't we choose parallel operation or pilot implementation?
- Well, parallel operation is quite expensive since you need to run both systems at the same time
- In our opinion, we don't have enough proposed changes to justify the cost of running two systems at the same time
	- if it were an entire system overhaul, it would make more sense
- We also think using a parallel operation would be counterproductive to our non-functional requirements
- D2L would have to split resources to run both systems which inherently goes against our non-functional requirements due to the fact that running two systems at once is more complex and resource exhaustive which could affect reliability and performance

Slide 7:
- Pilot implementation on the other hand is pretty straight forward
- Our non-functional reliability and performance requirements can't feasibly be piloted because they require the full user base for testing

Slide 10:
- So why didn't we choose direct cutover?
- It's very high risk
- Given the variety of our proposed changes being both functional and non-functional
- Any unanticipated issues arising could impact the reliability and performance of the system
	- If our proposed changes were purely functional, the risk would be significantly less
- There is also no way to measure the benefits of each proposed change until after they've the old and new systems have been swapped
	- This is an issue because how does D2L know if any of these changes have any benefit to their platform at all? They can't know until spending the time and resources into making all the changes first
- And lastly, too many features at once can be overwhelming for both the user base and the development team
- For the development team, integrating 15 different changes at once can become complicated
- For the users, 15 features being introduced at the same time can lead to features being unseen or disregarded by users

Slide 11:
- That leaves us with Phased implementation
- We recommend phased implementation because it solves all the issues with using direct cutover
- First issue being that there is less risk involved due to being able to handle the variety of proposed changes, whether functional or non-functional
	- For example, improving the uptime of the system can be implemented in phases
	- This is less risky because troubleshooting a small change is much more manageable than troubleshooting a whole system 
- secondly, D2L can measure the benefits of each feature as they roll out
	- This is great for D2L because they can gauge whether the changes are adding any benefit to their platform early on ,and use that information to make decisions on whether to move forward with the rest of the changes or not
- And lastly, features can be adopted by users one at a time
- This leads to a higher likelihood of the users using and testing the feature being introduced

Now i'll hand it off to Ray to discuss implementation tasks







# REMOVE
Slide 8:
- We're now left with Direct Cutover and Phased implementation
- To help drive our point, I'd like to make the comparison between the systems development life cycle vs the agile and iterative development methodologies
- SDLC, often called waterfall methodology requires that the entire project be completed before being implemented
- The key point here is that this methodology is not flexible in that changes to the requirements aren't allowed once the process starts and the SDLC is similar to direct cutover
- The D2L development team would have to complete all proposed changes before being able to deliver them to the users if they used Direct Cutover

Slide 9:
- Agile methodology on the other hand, focuses it's efforts in making incremental changes
- This means that each feature or improvement is developed  in small increments while a working product is maintained throughout the whole process
- The key point here is that this methodology is flexible because if requirements need to be changed, the development team can start a new iteration on it
- And agile is similar to phased implementation
- Each proposed change can be introduced slowly in small increments
