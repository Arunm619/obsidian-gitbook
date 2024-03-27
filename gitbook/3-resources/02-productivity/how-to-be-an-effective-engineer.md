Amazon Broadcast Video

Challenges: Art of Software Engineering also has it fair share of challenges like subjectivity and ambiguity

2 principle enggs: Venks and Amrut Joshi

Cohesion based decoupling architecture

### Who is an Effective engg?
- most productive engg
- churns out a lot of code
- solves the biggest problems
- effective is picking the right things to do, efficient is doing things right
- effective and efficient engg 👍
- has the right set of tools - right monitor, keyboard, ide, custom scripts
- pick right problem, come up with right approach and solving it properly - long lasting implementation
- effective and efficient - lot of overlaps between them
- active practitioners - constantly building/implementing things (diff btwn scientists vs enggs - scientist don't do practice, enggs do things)
### How to pick up right problems to solve
- comes  with experience - ways to gain that experience are:
	1. learn from others (peers - seniors & juniors)
		- observe and monitor others' work like design doc, code, attend meetings
	2. get your hands dirty
		- be an active practitioner
		- start solving problems, make mistakes, get hurt, learn, repeat
- understand the user's requirements and think what constraints your solutions has - now work on streamlining these bottlenecks - this is the starting point - you're working backwards from customer (customer obsession & working backwards)
- why is customer facing this problem - use the 5y technique and root-cause it, then solve it
- always question the problem and get to the root-cause
	- even if leadership team gives you a problem, question that and try to understand the problem still cuz maybe its not the actual problem but a solution that someone has already thought of - unravel the real problem
### How to measure who is an effective engg
- not someone who puts in more hours, not the quantity or quality of outputs - but the business impact
- effectiveness is not a function of input of time nor the output of work, but rather function of the impact of the final product
- measured by 
	- actual output/deliverables
	- overall quality of the artefacts produced
		- quality can be usually easily measured - is the s/w full CD, are there tests
	- impact on the team - is the dev
		- a team player
		- a mentor - mentored peers
	- innovation, unique ways to solve the problem
		- innovation can be anything - reduce costs, IMR
	- consistency - 
		- truly effective engineer is consistent across changes - diff teams, diff projects, diff domains.
		- use insights from the past experience in the new projects/teams/tech.
### How to go about designing a solution - Mental model :P 
- Don't design, do mental model based on requirements so the changes don't affect the design but the mental model. 
- Decomposition - Break a big problem into smaller pieces. Build the small pieces and build the software. 
- right level of abstraction
- mental model intermediate - the design should be well abstracted that it can easily accommodate new changes in requirement without much change in design
- don't solve a particular problem, try and identify the right level of abstractions. these abstractions can evolve on their own which will actually solve multiple no. of problems.
	- eg: write interfaces, use factories, decouple
- mental models - understand how things work in real world and how they can evolve over time
	- think about the evolution - how the problem and the solution will evolve over time
- noble thought - write easily maintainable code, future enggs (including me :P) should not struggle while trying to make a change
	- the customer for product - end user
	- the customer for my design - future enggs
- design is always iterative process
	- make abstractions - understand problem, come up with generic design solutions, then try to fit in specific cases and simulate - modify the design if it fails for a particular case's simulation
### When and how to get your design reviewed
- don't get emotionally attached to your code or design - it'll become difficult to get reviews
- don't get biased, unconscious bias is always there that your soln is the best. how to overcome that - don't jump to a particular soln, have a system to come up with soln. what's the system:
	- come up with multiple solutions - helps to think outside the box in different ways, stop running in one direction
	- compare the multiple solns - figure out the comparison criteria (patterns) - figuring out the criteria will become the pivotal point to finalise out the best soln - with criterias, half your work is done
	- how to know that the criteria are correct - brainstorming meetings, reviews - criteria are only discussed
	- when you have the criteria, we can try to take the scale to extremes and find out new solutions that we didn't previously think of
- to eliminate bias, be open to feedback & criticism
- design is hard to learn from books - can learn only from doing
- shadow in design review meetings
### Q&A

Q. Enggs come up with design & mental models and then retrofit with requirements. what are your thoughts on that
A. 
- Depends on your defn of mental model
	- if its created narrowly for a particular usecase, then its a problem. 
	- But if domain of mental model is large, then you'll start thinking of expansions, extensions and flexibility, the model will have all these properties.
	- Be wary about the scope of mental model- have large scope that change in requirement is embraced gracefully
	- two ppl working on same design can have vastly different mental models
- talk to domain experts - gain knowledge by asking right questions, then make the mental model
- need for mental model - to have extensibility, to avoid having a design that gets complex as and when new feature requirements come up
- requirement collection <-> mental model - order not important if mental model is made right

Q. maintaining consensus is a key aspect for tenured enggs to become effective as often enggs have conflicting opinions. how to handle conflicts?
A.
- conflicts are good👍 - ppl are thinking in different ways (diff perspective) - if everyone agrees to everything (like an echo-chamber), then there's no innovation
- how to solve
	- get more data to support your point
	- if its completely subjective - disagree and commit
	- go to first principles; find out, validate and eliminate assumptions
	- if more than one soln are correct - make someone to commit and keep monitoring the decision - but keep it a 2-way door decision, so that can be changed
- be genuinely honest, have empathy, be reasonable, be transparent - will help you earn trust

Q. what's the process of implementation & writing code after identification of requirements and iterative process of designing
A.
- validate assumptions by
	- start off with coding a poc (proof of concept) - make sure that its not a complete throw away code
	- if assumption turns out to be true, you should be able to use that code to go ahead
- make low level design - use architecture patterns
- all hands on the deck - start writing code

Q. are unit tests constraining you in terms of doing refactoring later on? are we better off having integration tests? should we prefer writing tests first?
A.
- any CR you send out should have tests
- writing test first or after writing code doesn't matter, but should be there
- unit test - helpful - simplifies refactoring prevents bugs especially during refactoring
- tests give this guarantee - my change is not breaking any functionality and go to production
- have a mix of both unit and integration tests
- writing tests help you push yourself to write good code
- code is not for compilers, code is for humans to understand - compilers will make it understandable for machines

Q. how does meaning of effectiveness change along with career growth - what is it for SDE1 and for SDE2 and so on?
A.
- level doesn't matter, experience does - if you've really mastered the art of writing code and designing, then you're effective
- over time you'll get proficient with the toolset you're using, you'll understand insights of technologies, you'll keep on gathering best practices - your effectiveness goes up
- though theory give edge, practice is the king
- be passionate about learning new things
- watch out things that are working for you - be retrospective - evaluate what has worked for you
- build your knowledge base, wisdom base




---
Idioms
- Churn out - produce something routinely or mechanically in large quantities
  Eg.: Churn out code - write code
- get your hands dirty - do menial or other hard work not requiring much skill
- all hands on the deck - everyone is needed or called to help, especially in a difficult situation
---
Meanings
- objective - based on facts and evidence
- subjective - based on individual's emotions, perspectives, assumptions, opinions
- fungible - replaceable by another identical item, mutually interchangeable