---
title: Kanban for Infrastructure Teams
description: Overcoming common barriers and adapting agile practices for IT operations.
date: 2023-07-25
# lastmod: 2025-03-26
author: 'Felipe Curty'
# draft = true
---

When I started leading an IT infrastructure team and introduced Kanban to the
team, I realized that adopting agile methods would be far from trivial. I faced
challenges and discovered a few tweaks that helped me align the team goals and
streamline our process.

I figure out some problems unique to infrastructure teams. Unlike development
teams, which generally follow a development process, an infrastructure team
typically deals with a diverse range of tasks and technologies. For instance, I
managed a team in which one collaborator was responsible for the old mainframe
infrastructure, and the other was responsible for a modern Linux server farm.
How can we run an engaging and relevant daily for both of them? Moreover, how
can team members with entirely different skill sets support each other?

Furthermore, there is a lack of literature focused on infrastructure teams. Most
books and blogs I read discuss Kanban in the context of development teams, i.e.,
teams that work toward developing new features and bug fixes for software
projects. Unfortunately, infrastructure teams work entirely differently. Thus,
it was difficult to find relevant examples suitable for my team. 

Another challenge is the variety of task sizes within infrastructure work. There
are many incidents to handle. Some incidents took a few minutes, while others
took days to resolve. Also, we need to track space in the schedule to manage
project tasks. Moreover, my team supervises and advises on many tasks executed
by contractors. Gathering all these tasks into the board without exploding the
work in progress (WIP) was a challenge.

I categorized the tasks into three groups to start addressing these challenges:
Incidents - small tasks requested by our clients that take less than one day to
complete; Internal Tasks - all tasks executed by the team, such as configuring a
server or developing automation, and incidents that span over a day; and
Contractor Tasks - tasks executed by contractors that require supervision.

Then, I started to manage the incidents. I found [this post][small-task] from
_Joakim Sundén_, author of the book _Kanban in Action_ that inspired my
solution. The idea is to track the incidents in a dedicated column on the Kanban
board. In the incident column, we write the list of incidents opened and
assigned to our team. We write only the incident number and the owner. Once the
incident is resolved, we simply cross it out.

[small-task]:
    https://joakimsunden.com/one-way-of-handling-small-tasks-on-a-kanban-board

This column helps us handle many small tasks. Our goal is to represent the
assigned work and work done. In the daily meeting, we do not discuss each
incident. But, we can quickly identify whether the number of incidents is under
control. When an incident demands more attention, its owner can speak about it,
and we evaluate promoting the incident to an internal task.

Next, I started to manage the internal tasks.


---








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
represent the tasks of infrastructure teams. Thus, I suggest generalizing the
board to the following columns:

  - **Doing** the work, such as configuring infrastructure, assessing its
    quality and compliance, developing automation, and writing contracts;
  - **Reviewing** the work to assure its quality;
  - **Deploying** the work to satisfy all the change and delivery management
    compliance.

As in any Kanban board, the card will be moved through these three columns until
ready. Since different types of tasks are managed on the same board, it would be
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

The third barrier I found is handling epic tasks that may stay fixed in the same
board column for weeks. It is a common problem in agile methods, and the
solution is to split the epic task into smaller tasks. The issue is that it may
be difficult to split the task into meaningful small tasks. For instance,
depending on the number of servers, applying a security patch may take a while
to reach all the production servers. A reasonable solution is to split the
servers into waves and track each on a separate card. Thereby, we can create a
task to update the application server and another to update the database
servers. 
