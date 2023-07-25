---
layout: post
title:  "Kanban for infrastructure and DevOps teams?"
comments: true
excerpt_separator: <!--more-->
---

I have worked with infrastructure teams for over a decade, and I discovered that
adopting agile methods with these teams is far from trivial because some
barriers muddle the use of such methods in those teams. In this post, I will
share some thoughts about those barriers and discuss how teams could bypass
them.

<!--more-->

The first barrier I found deploying Kanban in an infrastructure team is the lack
of literature discussing and explaining the subject regarding those teams'
processes. Most books and blog posts explain Kanban in the context of a
development process, where the team works toward developing new features and bug
fixes for a software product or project. That is not how infrastructure teams
manage their work. Although agile concepts apply to any team, it is difficult
for the infrastructure teams to find examples they identify with.

I suggest starting by adapting the Kanban board from development to
infrastructure. A common Kanban board created for developers generally comprises
three major action columns: developing, testing, and deploying. This board is
adequate for teams that develop and deliver new features but does not fully
represent the work of infrastructure teams. Thus, I suggest generalizing the
board to the following columns:

  - **Doing** the work, such as configuring infrastructure, assessing its
    quality and compliance, developing automation, and writing contracts;
  - **Reviewing** the work to assure its quality;
  - **Deploying** the work to satisfy all the change and delivery management
    compliance.

As in any Kanban board, the card will be moved through these three columns until
ready. Since different types of work are managed on the same board, it would be
helpful to state a _definition of done_ to each type in each column. For
instance, a configuring task, such as applying security patches, could be
considered done on the _doing_ column once applied and documented on the
development systems. It would be considered done on the _reviewing_ column once
tested by other team members. It would be considered done on the _deploying_
column once the change was applied in the quality assurance and production
systems.

The _reviewing_ column could be challenging because infrastructure teams may
comprise members with very different skills, in which case, the test of some
configuration could be unfeasible to be done by other team members. I will not
discuss it in this post because it is a problem regarding knowledge, training,
and team management.

The second barrier I found is managing incidents and service requests. Complex
tasks may be tracked among other cards. But generally, these activities comprise
several small tasks that are individually simple but may consume much time when
added together. The problem is that tracking small activities (e.g., an incident
or access request that may take one hour to be solved) will fill the board with
small cards, which may be unfeasible to manage and will reduce the board's
effectiveness in tracking the important tasks. Also, it will not be possible to
control the _work in progress_ when mixing tasks with such a different size.

I struggled to solve this problem until I found [this post][small-task] from
_Joakim Sundén_, author of the book _Kanban in Action_. The idea is to track
small tasks in a different column, where the team writes the _ticket_ number_ to
represent that it needs to be done and cross it out once done. This way, the
board can track the effort of the small tasks without mixing them with the other
tasks.

[small-task]: https://joakimsunden.com/one-way-of-handling-small-tasks-on-a-kanban-board

The third barrier I found 

The task goes to doing when the development start. After the development,
someone responsible for testing the new feature would pull the card to testing
and check the quality. Finally, after all, the developer deploys the code to
Quality or Production System and the card is finished.

The second difficulty is that it seems more difficult to split infrastructure
task into a coarse size that worth track on the board. For instance, small
incidents would just include overhead to the board if they are managed as a
card. Huge tasks, like infrastructure epics, could lay forever on the board,
which is not the idea of agile.

The third is the lack of product vision. In fact, the product owner is a common
role in development teams but it is a misunderstood role for infrastructure
teams. I would argue that the main product of infrastructure teams is the
infrastructure itself. 

The forth is the lack of business client vision. The infrastructure team is
generally far away from the company client. Hence, they lack the vision of
urgency and importance that may enable the correct prioritization of the tasks.


Also, infrastructure teams generally manage contracts, which naturally increase
the WIP. Some of the project activities are done by the contractors and the
infrastructure team just need to track the status and check for quality issues.

I would categorize infrastructure into three categories:

  - General tasks - it represents the tasks that the team need to acomplish in
    order to success.
  - Incidents and service requests - it represents small and usually urgent
    tasks that might interrupt the team.
  - Tracking tasks - it represent General tasks that are handler by other
    individual contributors, generally contractors.


The developers work many times are more interchangeable. It means that developer
team may be working on different features, but the developers are generally
sharing at least the development stack, frameworks and programming language. Of
course there are a lot of complex activities that can be impossible to onboard
to inexperienced developers, but by the end of the day, it will be all about
complexity and business logic. It is rare to find a developer team that manage
several different technologies to develop a system. 

In infrastructure it is quite different. Instead of managing to use a common
language or framework, infrastructure teams tend to manage different products
that could be completely different on to the other. I'm not yelling that
infrastructure work is more complex, but just that the nature of the work
demands to be much more heterogeneous than developers team. 

For instance, I'm currently leading the SAP infrastructure team. They are four
awesome guys that need to handle about one hundred server online with the most
different technologies. From the Netweaver application server to the Oracle
database. There are also other hibrid tools, such as IDM and TDMS. The point is
that those tools works completely different, which make 


using agile 

I have been working on security, infrastructure, DevOps teams for a long to know
that some unplanned tasks may easily break a well-crafted board. Hence, I would
like to share some insights about how to create a kanban board.

Most of the literature I have read describes boards geared towards development
teams. These boards generally comprise columns related to code, test and deploy
activites. Sometimes, these boards also include a colum related to planning
activities, where the team intends to break large generic histories (i.e.,
epics) into smaller detailed histories.

While these boards can work pretty well for developer teams, they generally do
not fit at all for security, infrastructure, and devops teams, because tha type
of work is very different. First, developer teams tend to focus on delivery
features of product. 





