---
layout: post
title:  "Why is it difficult to use Kanban for infrastructure and DevOps teams?"
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

