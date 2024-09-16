#BUSINESS/W1 
# Information systems development

## Programming

- The process of creating a set of logical instructions for a digital device to follow using a programming language

## Systems development life cycle

- Very structured and risk averse, designed to manage large projects that include multiple programmers and systems that have a large impact on the organization 
- Requires clear, upfront understand of what the software is supposed to do and is not amenable to design changes
- Sometimes referred to as **waterfall methodology
	- Only when one step is done may the next begin
	- Criticized for being rigid
		- Changes to requirements are not allowed once process has begun
		- No software available until after programming phase

			![[Pasted image 20240911161500.png]]

- ### Common phases:
	1. **Preliminary analysis**
		- Ask important questions such as:
			- What is the problem to be solved?
			- Is creating a solution possible?
			- What alternatives exist?
			- Is this project a good fit for the company?
		- After answering questions, a **feasibility study** is launched
			- Technical feasibility
			- Economic feasibility
			- Legal feasibility
	2. **System analysis**
		- System analysts work with different stakeholder groups to determine specific requirements for the new system
		- Procedures documented, key players/users interviewed, data requirements developed
			- All done to get an overall impression of exactly what the system is supposed to do
		- Result of this phase is a **system requirements document** that may be done by a Systems Analyst
	3. **System design**
		- Designer takes the system requirements document and develops the specific technical details required for the system
		- Design for the UI, database, data inputs and outputs, and reporting are developed here
		- Result of this phase is a **system design document**
			- Has everything a programmer needs to create the system
			- May be done by Systems Analyst, Developer, or Systems Architect based on scale of project
	4. **Programming**
		- Using system design document as a guide, programmers develop the software
		- Result is an initial working software that meets requirements from system analysis and system design phase
		- May be done by Developer, Software Engineer, Programmer, or Coder
	5. **Testing**
		- Software program developed in programming phase is put through a series of structured tests
			- Unit test
			- System test
				- Ensure different components work together
			- User acceptance test
				- For those who will be using the software to see if system meets their standards
		- Any bugs, errors, or problems found in this phase are resolved and then tested again
		- May be done by Tester, Testing Analyst, or Quality Assurance
	6. **Implementation**
		- Includes training the users, providing documentation, and data conversion from the previous system to the new system
	7. **Maintenance**
		- In this phase the system has a support structure in place
		- Reported bugs are fixed and requests for new features are evaluated and implemented
		- System updates and backups are made for each new version of the program

# Rapid application development

- Focuses on quickly building a working model of the software, getting feedback from users, and then updating working model based on feedback
	- After several iterations, a final version is developed and implemented
- Focus is on user participation and iteration
- Better suited for smaller projects than SDLC
		![[Pasted image 20240911163340.png]]
### RAD methodology 4 phases
1. **Requirements planning**
	- Overall requirements for system are defined, a team is identified, and feasibility is determined
1. **User Design**
	- Representatives of the users work with system analysts, designers, and programmers to interactively create the design of the system
	- Sometimes **Joint Application Development** (JAD) used to facilitate working with various stakeholders
		- JAD session brings all stakeholders for a structured discussion about the design of the system
		- Application developers also participate and observe to understand essence of the requirements
1. **Construction**
	- Application developers and users work together build the next version of the system through an interactive process
	- Changes can be made as developers work on the program
	- This step is executed in parallel with User Design phase in an iterative fashion, making modifications until an acceptable version of the product is developed
1. **Cutover**
	- Switching from the old system to the new software
	- Timing is crucial and usually done when there is low activity
		- i.e. School systems undergo many changes and upgrades during summer and not during the rest of the year
	- Approaches to migration vary between organizations
		- Just do it
		- Implement one module at a time
		- Run both old and new systems in parallel

# Agile methodologies

- Group of methodologies that utilize incremental changes with a focus on quality and attention to detail
- Each increment is released in a specific period of time (time box), creating a regular release schedule with very specific objectives
- Based on the "Agile Manifesto" first released in 2001
- Goal is to provide flexibility of an iterative approach while ensuring quality product

![[Pasted image 20240911163445.png]]
## Agile and iterative development

**Characteristics of agile methodology**:
- Small cross-functional teams that include development team and users
- Daily status meetings to discuss current state of project
- Short time-frame increments (days to 1 or 2 weeks) for each change to be completed
- Working project at the end of each iteration which demonstrates progress to stakeholders

# Lean methodology

- Focuses on taking an initial idea and developing a **Minimum Viable Product** (MVP)
	- A working software application with just enough functionality to demonstrate the idea behind the project
- Once MVP is developed, development team gives it to potential users for review
- Feedback on the MVP is generated in two forms:
	1. Direct observation and discussion with the users
	2. Usage statistics gathered from software itself
		- Using these forms of feedback, team determines whether they should continue in the same direction or rethink the core idea behind the product, change the functions, and create a new MVP
			- This change in strategy is called a **pivot**
- Several iterations of MVP are developed, with new functions added each time based on feedback until a final product is completed
- Lean methodology works best in entrepreneurial environment where a company is interested in determining if their idea is worth developing

- Big difference between iterative and non-iterative methodologies is that the full set of requirements for the system are not known when the project is launched


# Flash cards

What is programming?::The process of creating a set of logical instructions for a digital device to follow using a programming language.

What is the Systems Development Life Cycle (SDLC)?::A structured and risk-averse methodology designed to manage large projects with multiple programmers and significant organizational impact, often referred to as the waterfall methodology.

What is the waterfall methodology?::A structured approach where each phase must be completed before the next begins, criticized for being rigid and not allowing changes once the process has started.

What are the common phases of the Systems Development Life Cycle (SDLC)?::1. Preliminary analysis, 2. System analysis, 3. System design, 4. Programming, 5. Testing, 6. Implementation, 7. Maintenance.

What occurs during the preliminary analysis phase of Systems Development Life Cycle (SDLC)?::Important questions are asked to assess the problem, feasibility, and project fit, leading to a feasibility study covering technical, economic, and legal aspects.

What happens in the system analysis phase of Systems Development Life Cycle (SDLC)?::System analysts determine specific requirements by documenting procedures, interviewing key users, and developing data requirements, resulting in a system requirements document.

What is produced during the system design phase of Systems Development Life Cycle (SDLC)?::A system design document that includes technical details required for the system, such as UI, database design, data inputs/outputs, and reporting.

What is the programming phase in Systems Development Life Cycle (SDLC)?::Programmers develop the software using the system design document as a guide, resulting in an initial working software that meets the requirements.

What is the purpose of the testing phase in Systems Development Life Cycle (SDLC)?::To put the software through structured tests like unit tests, system tests, and user acceptance tests to identify and resolve bugs and issues.

What occurs during the implementation phase of Systems Development Life Cycle (SDLC)?::Training users, providing documentation, and converting data from the previous system to the new system.

What is involved in the maintenance phase of Systems Development Life Cycle (SDLC)?::Providing support, fixing bugs, evaluating and implementing new feature requests, and making system updates and backups.

What is Rapid Application Development (RAD)?::A methodology that focuses on quickly building a working model, getting user feedback, and iterating on the model to develop a final version.

What are the four phases of RAD methodology?::1. Requirements planning, 2. User Design, 3. Construction, 4. Cutover.

What is the cutover phase in RAD?::Switching from the old system to the new software, with migration approaches varying between organizations, such as immediate switch or running both systems in parallel.

What are Agile methodologies?::A group of methodologies that utilize incremental changes with a focus on quality, with each increment released in a specific time period, based on the Agile Manifesto.

What are characteristics of agile methodology?::Small cross-functional teams, daily status meetings, short time-frame increments, and a working project at the end of each iteration.

What is Lean methodology?::A focus on developing a Minimum Viable Product (MVP) to demonstrate the core idea, gathering feedback, and iterating based on that feedback, with potential pivots in strategy.

What is a Minimum Viable Product (MVP)?::A working software application with just enough functionality to demonstrate the idea behind the project.

What is a pivot in Lean methodology?::A change in strategy based on feedback, which may involve rethinking the core idea or altering functions to create a new MVP.

What is a key difference between iterative and non-iterative methodologies?::In iterative methodologies, the full set of requirements is not known at the project launch, while non-iterative methodologies require complete requirements upfront.