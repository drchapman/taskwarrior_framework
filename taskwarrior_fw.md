# TaskWarrior Framework

## Goals
- Create and manage projects and member tasks within taskwarrior using a consistent interface
- Create and manage conceptual contexts within taskwarrior using a consistent interface
- Reduce the keystrokes and complexity needed for project and context management


## task_project

### Syntax

~~~bash
task_project 
	Show all currently defined projects

task_project -h
	Show this help message

task_project ProjID
	Show all tasks belonging to the project whose definition has taskID ProjID

task_project ProjID add [+] Task Description
	Create a new task as a member of the 
	+ Copies tags (except +definition) from the definition task

task_project ProjID mv TaskID
	Move task TaskID into project ProjID

task_project ProjID drop TaskID
	Drops task TaskID from project ProjID

task_project new Project description
	Define a new project 
~~~

## task_context

### Syntax

~~~bash
task_context 
	Show all currently defined contexts

task_context -h
	Show this help message

task_context ContextID 
	Show all tasks belonging to the context whose definition has taskID ContextID

task_context new ContextName description -f <task filter>
	Define a new context 

task_context rm ContextID 
	Removes a Context definition

~~~

## Components

Task Warrior Project Definitions Report: `ProjDefs`

~~~bash
report.ProjDef.description=Manage Projects and Project Definitions
report.ProjDef.filter=status:pending +definition
report.ProjDef.columns=id,project,description.count,tags
report.ProjDef.sort=project
~~~


Project Details Report: `ProjDetails`

~~~bash
report.ProjDetails.description=Display the constituent tasks of a project
report.ProjDetails.filter=status:pending -definition
report.ProjDetails.columns=id,entry.age,due.relative,description.count,tags
report.ProjDetails.sort=date+,urgency
~~~


Task Warrior Context Description Report: `ContextDesc`

~~~bash
report.ContextDesc.description=Show currently defined Contexts
report.ContextDesc.filter=status:pending +context
report.ContextDesc.columns=id,project,description.count
report.ContextDesc.sort=project
~~~


Context Details Report: `ContextTasks`

~~~bash
report.ContextTasks.description=Display the constituent tasks of a context
report.ContextTasks.filter=status:pending -definition
report.ContextTasks.columns=id,entry.age,due.relative,project,description.count,tags
report.ContextTasks.sort=due+,urgency
~~~
