---
kind: article
title: Code is the Best Documentation
created_at: 20101110T143816
---
Early in my career, we considered it a Best Practice to produce reams of documentation along with the software we created. It was part
of the [waterfall process model](http://en.wikipedia.org/wiki/Waterfall_model). The first step is that all the stake holders fight it out to determine what the requirements of a
product should be. Next, we developers, or at least the ones who were chosen to participate in the design process would draw out [UML Diagrams](http://en.wikipedia.org/wiki/Unified_Modeling_Language)
to flesh out the major subsystems and components. Then those pieces, once their connections and interfaces were defined, would get
farmed out to different developers who would write each component, and part of the deliverable were sets of design documentation
that detailed interfaces, contracts and implementation details.

If it sounds like a painful and inefficient way to produce software that is late, over-complicated, bloated and doesn't do what the end
user wants, you're right. Almost nobody does waterfall anymore. Most new projects run with some form of [agile](http://en.wikipedia.org/wiki/Agile_software_development)
process, whether it be [Scrum](http://en.wikipedia.org/wiki/Scrum_%28development%29), [Extreme Programming](http://en.wikipedia.org/wiki/Extreme_Programming)
or some other hybrid approach.

One unintended consequence of this switch is the focus away from documentation that is not part of the software itself. I used to be an
avid commenter - when I wrote a module or piece of software, I would write all the comments first and then go in and add the code between
the statements. Now, for better or worse, I consider excessive commenting to be a code smell. If you need to write a novel about why you
did something some way, maybe that's a sign that it's too complicated or the wrong approach. Sometimes comments are necessary and good:
for any published API, the best way to document it is by commenting the public API methods and using an automated tool to generate
documentation. I also don't want to malign [Literate Programming](http://en.wikipedia.org/wiki/Literate_programming) too much - some
incredible software has been produced with it, and it may be the right tool for pedagogical applications.

Where the shift has been incredibly good and useful is that documentation is starting to take the form of executable code that
defines the specification of a program in human-readable language and can be run be an automated tool to verify that the program
actually adheres to that specification. My favorite tool for doing that is called [Cucumber](http://cukes.info/). What is nice about
this tool is it provides a way to communicate requirements that stakeholders can understand, but it can be executed whenever the
application is changed to verify that the product really does meet those requirements.

This is a simple example of a cucumber feature
<code>
	Feature: Adding numbers
		Because I am really bad at math, I need a computer program to add two numbers together
		Scenario: Simple addition
			Given a calculator
			And I press 1
			And I press +
			And I press 1
			And I press =
			Then I should see 2
</code>

Behind the scenes, you implement 'definitions' for all the steps, and even if you're not a programmer, you know what this means. The other
thing that is nice, is if the implementation becomes out of sync with the specifications, then you know, and you can fix one or the other.