---
title: Kanban for Infrastructure Teams
description: Overcoming common barriers and adapting agile practices for IT operations.
date: 2023-07-25
lastmod: 2026-05-13
author: 'Felipe Curty'
tags:
- Agile
- DevOps
cover:
  image: headline.png
  alt: A kanban board with three columns, sticky notes moving between them, and faded server racks in the background
  relative: true
---

When I started leading an IT infrastructure team and introduced Kanban, I
quickly realized that adopting agile methods would be far from trivial. Most
Kanban guidance assumes a development team shipping features, but
infrastructure work is heterogeneous, interrupt-driven, and partly executed by
contractors -- a mix that a standard board does not accommodate without adaptation.
I faced several challenges and, over time, found a few adjustments that helped
the team align around shared goals and keep work moving.

I ran into several problems that were unique to infrastructure teams. The first
is **heterogeneity**. A development team usually shares a stack (language,
framework, process, etc.), so its members can pair, review each other's work,
and rotate through tasks. In contrast, an infrastructure team is responsible
for a diverse range of tasks and technologies. The team I led, for example,
had one member responsible for an old mainframe and others responsible for a
modern Linux server farm. The work is not inherently more complex, but it is
far more varied, and that makes it harder to run a daily stand-up that feels
relevant to everyone or to have team members support each other across skill
sets.

Furthermore, there is a **lack of literature focused on infrastructure
teams**. Most books and blog posts discuss Kanban in the context of
development teams shipping features and bug fixes. The agile concepts
themselves apply to any team, but the examples rarely do -- and without
examples that match the work, it is hard to know where to start adapting
them.

Another challenge is the **variety of task sizes** within infrastructure
work. It mixes incidents and service requests that take minutes, such as a
password reset or a quick access grant, with project tasks that stretch over
days or weeks. Moreover, my team supervised and advised on many tasks
executed by contractors. Representing all of these on a single board was a
challenge: the tasks varied widely in importance and duration, and without
care the work in progress (WIP) would quickly get out of hand.

To handle this mix, I split the work into three groups, each managed
differently on the board:

  - **Small requests**: incidents and services requested by our clients
    that take less than one day to complete;
  - **Project tasks**: work executed by the team itself, such as
    configuring a server or developing automation, plus any incident that
    runs longer than a day;
  - **Contractor tasks**: work executed by contractors that the team
    supervises.

I started with the **small requests**. I struggled to solve this problem until I
found [this post][small-task] from _Joakim Sundén_, author of _Kanban in
Action_. The idea is to track them in a dedicated column: the team writes
the request number and the owner, and crosses each one out once it is
resolved. This way, the board represents the effort of the small requests
without mixing them with the larger tasks. Later, we stopped writing those
numbers by hand and instead displayed a live report from our ITSM that
listed the requests in progress.

[small-task]:
    https://joakimsunden.com/one-way-of-handling-small-tasks-on-a-kanban-board

In the daily meeting, we did not discuss each request; we just glanced at
the column to see whether the count was under control. When one of them demanded
more attention, its owner brought it up, and we evaluated promoting it
to a project task.

Next, I turned to the **project tasks**. These were the bulk of the team's
work and the category where a developer-style board fits best. A typical
Kanban board for developers has three action columns -- developing, testing,
and deploying -- which works well for shipping features. Project tasks in
infrastructure follow a similar shape, but the columns need to be
generalized to cover work that isn't always _developing_ or _testing_ in
the dev sense:

  - **Doing** the work, such as configuring infrastructure, assessing its
    quality and compliance, developing automation, and writing contracts;
  - **Reviewing** the work to assure its quality;
  - **Deploying** the work to satisfy change and delivery management
    compliance.

Cards move through these three columns until done. Since different project
tasks share the same board, it helped to define _done_ for each project
task in each column. For instance, applying a security patch was done in the
_doing_ column once it had been applied and documented on the development
systems; done in the _reviewing_ column once tested by other team members;
and done in the _deploying_ column once it reached the quality assurance
and production systems.

The _reviewing_ column was the hardest to operate, and in practice we
skipped it for most tasks. The team combined very different skill sets --
the mainframe person could not credibly review the Linux work, and vice
versa -- so peer review was rarely feasible, and reviewing simply did not
apply to much of the workload. I will not solve that here because it is a
broader problem of knowledge, training, and team management, but it is
worth noting that an infrastructure board may often run with the
reviewing column effectively bypassed.

One challenge that remained was **epic tasks** -- long-running work that
could stay parked in the same column for weeks. This is a common problem in
agile methods, and the standard answer is to split the epic into smaller
pieces. The hard part for infrastructure is finding splits that actually
carry meaning. Applying a security patch across hundreds of production
servers, for example, could take weeks; chopping it into "patch 50 servers"
cards is artificial and adds little visibility. A more practical split is
to group the servers by role or by deployment wave and give each group its
own card -- one for the application servers, another for the database
servers, another for the next wave of edge nodes.

Next, I turned to the **contractor tasks**. Infrastructure teams generally
manage several contracts in parallel, and a single team member can handle
a couple of contractor engagements with different collaborators at once.
These tasks behaved differently from the other two: the team did not
execute the work; it supervised it. That meant the cards on our board
represented attention rather than hands-on effort -- tracking status,
reviewing deliverables, raising quality issues, and signing off when work
was complete. Mixing those cards into the project-tasks columns would
have inflated the WIP without reflecting capacity: supervising five
contractor work streams is not the same as doing five internal projects.

I tracked contractor work on a dedicated swim lane on the board, separate
from the project-tasks columns. Each ongoing engagement got its own card,
listing the contractor, the deliverable, and the next checkpoint. The
card stayed visible for as long as the team had any responsibility for
the work -- through delivery, review, and acceptance -- which made
supervision visible to the rest of the team without competing with the
project-tasks WIP limits.

None of these adjustments are radical departures from Kanban -- they are
local adaptations to make the method fit a team that does not look like a
development team. The board became useful not because it solved every
problem, but because it represented the work as it actually was: a mix of
small requests, longer projects, and supervised work done by others.
