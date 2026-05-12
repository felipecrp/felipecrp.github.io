---
title: 'Keeping Knowledge in the Room: Three Practices for Infrastructure Teams'
description: Why infrastructure teams struggle to share knowledge, and what has helped my teams keep it in the room.
date: 2026-05-11
author: 'Felipe Curty'
tags:
- Knowledge Management
- Infrastructure
- DevOps
cover:
  image: headline.png
  alt: Cover illustration for the post
  relative: true
---

I have been leading infrastructure and security teams for over a decade, and one
problem keeps coming back: knowledge does not spread on its own. Unlike a
development team where everyone shares a stack, an infrastructure team is a
collection of specialists, each owning a different product. When that specialist
takes a vacation -- or leaves -- their knowledge often walks out with them. In
this post I share what I have learned about why knowledge management is harder in
infrastructure teams and the practices that have helped my teams keep knowledge
in the room.

First, consider development teams. On a development team, engineers
are largely interchangeable. They may work on different features, but they
generally share the same stack: programming language, frameworks, build system.
Onboarding still takes time because the stack can be complex, and business logic
and codebase history do not transfer overnight. But once a developer understands
the basics of the stack and the business logic, they can usually step into a
teammate's work without much friction.

Infrastructure teams are quite different. Instead of converging on a single
stack, an infrastructure team manages a portfolio of products that often have
nothing in common with each other. I am not claiming the work is harder than
development -- only that it is structurally more heterogeneous, and that
heterogeneity is what makes knowledge so hard to share.

For instance, I once worked on a team that had to support both Linux and
mainframe operating systems -- two completely different worlds, demanding
completely different engineer profiles. A Linux specialist and a mainframe
operator could sit next to each other every day and never be able to cover for
one another. I saw the same pattern leading an SAP infrastructure team. The
stack spanned database administrators, NetWeaver experts, BASIS specialists,
integration engineers (PI/PO), and identity management administrators -- five
specialties under one team, with almost no overlap between them. IDM in
particular runs on a weird workflow engine -- even a senior SAP BASIS engineer
needs weeks of ramp-up before they can touch it.

So how to fight that? There is no silver bullet, but three practices have made a
difference on my teams: encouraging documentation, rotating engineers through
incident handling, and automating whatever can be automated. None of them
eliminates the heterogeneity -- they just keep knowledge flowing in the room.

First, pick one documentation tool and stick with it. A Git repository is often
enough, but a SharePoint site, Confluence, or any other wiki works too. When you
migrate content from old tools, take the opportunity to update what is outdated
along the way. If a document is not worth updating right now, link to it from
the new tool and mark it for future review. The engineer must document -- it
does not need to be perfect, but they need to take responsibility for writing.

Within documentation, separate playbooks (high-level tutorials) from runbooks
(very detailed scripts) and technical reports. Within each type, categorize by
technology or subject, so engineers can quickly find what they need. The
playbook explains what to do. The runbook explains how to do it. Generally, a
runbook can be reused in multiple playbooks. Finally, use technical reports to
gather context or to write more complex settings that engineers need to
understand the infrastructure.

Next, rotate engineers through incident handling. Incident handling is a natural
opportunity for engineers to run simple tasks, test their access, and become
familiar with the playbooks and runbooks of another specialty. A BASIS
specialist, for instance, can learn to free disk space on a Linux server -- or
know which team to escalate to -- without changing their day-to-day role.
Incidents also force engineers to talk across specialties to resolve the problem
-- and because incidents are shorter and more contained than projects, that
communication often happens and stays focused.

Finally, automate! Prefer tools like Ansible that describe each task
declaratively, so the playbook itself becomes runnable documentation. Moreover,
engineers can extend and reuse those automations, which spreads both the work
and the knowledge across the team. Once a procedure lives in code, it stops
walking out the door with the engineer who knew it.

Together, these practices make the team less fragile. Documentation captures
what people know; rotation gives them chances to learn from each other;
automation lets the system remember, so engineers do not have to.
