[How to effectively "Spike" a complex technical project Aditya Bansal at LeadDev London 2023 - YouTube](https://www.youtube.com/watch?v=z-ML5JYkmZ0&ab_channel=LeadDev)


Aditya Bansal 
Founding engineer, Cortex

[Cortex | Internal Developer Portal](https://www.cortex.io/)
Cortex is the internal developer portal that cuts noise for developers with paved paths to production. Catalog, score, and drive action to improve software.


2 big questions:
1. took longer than expected to finish a project?
2. requirements different from original expectations after long time?


Move fast and break things!

industry is divided into
YOLO(You Only Live Once) ..... BDUF (Big design up front)

yolo: 
dont design, write code, directly jump into code.. and oops mistakes!


BDUF:
iron out all details  and write code.
Big design up front (BDUF) is a software development approach in which the program's design is to be completed and perfected before that program's implementation is started.


Technical Spike: middle of both extremes:

1. most important details : key
2. remove distraction: just enough design and answer enough questions
3. time box


Effective Spiking:
- ~~Product~~  Problem : help solve problems for customers.
- Technical
	- Known unknowns : apis needed
	- Unknown unknowns : side effects, teams need to work with.

what not to do:
- Write production ready code 
	- Assume throw away code
	- assume it will not get merged
- solve for everything
	- dont try to limit the number of unknowns to 0. just reduce it down for increasing chance of success.
- take all the time in the world
	- starting point of project, not the project itself.
	- 1or 2 weeks based on the complexity

Branch called : `project/playground`

----

**Running an effective spike: Known unknowns**
List of greenfield changes: 
- Interfaces, Classes, Modules, Tables. 
- high level details
- talk to customers/stakeholders, solidify the understanding

**Running an effective spike: unknown unknowns**
- tag your explorations
	- Add annotations to document them, create own annotations @domainspike
- what will break? 
- what is the ripple effect?

Writing it down 
- what's new?
	- text spec - dump down data
- what's being modified?
	- different teams, get buy in?
- what do we need to discuss?
	- tech discussion with the team?


The above is specific to *New project on an already existing codebase.*

Put it in your own context and solve it.

**Those who have knowledge, don't predict. Those who predict, don't have knowledge.**
- Lao Tzu






---

malign - evil in nature
iron out - solve/settle problems
reminisce - indulge in enjoyable recollection of past events
caveat - warning or caution
