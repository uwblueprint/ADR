# Blueprint Architectural Design Reviews

## Rationale

This repository contains all of UW Blueprint's architectural design reviews (since the creation
of the system in W2020).  Prior to W2020, the responsibility of system design rested solely upon 
Project Leads (PLs).  While this was a fast process, this system didn't benefit from Blueprint
members' diversity of experience.  This lack of feedback sometimes resulted in suboptimal design
decisions which cost time to undo further down the road.  Due to this need for a more collaborative 
approach to system design, the practice of Architectural Design Reviews (ADRs) was implemented at 
Blueprint.

## Process

ADRs will be performed for every new project that Blueprint takes on.  After scoping (and by extension, 
the Statement of Work) is complete, Project Leads and their team should work on creating a design
document for their project.  This system design work should involve the entire team as it's a valuable
learning opportunity for both junior and senior developers.  Once created, the PL should open a PR adding
the design doc to the appropriate term directory (if the directory hasn't been created, it should be 
added).  This doc should follow the naming pattern {project-name}-adr.md (a Markdown file).

Once the PR has been created, the PL should request review from their entire team, the VPP, and the other
PLs.  Furthermore, the PR link should be shared in the #project-team-{term} channel on Slack asking for
review.  The doc should also be shared with any senior developers who have expertise with the specific
language, framework, technologies, etc.  The doc will be considered approved once the VPP and another
PL approve.

## Design Doc Template

The design doc template can be found in the root directory of this repository.

## Review

Given the short timeline of the Blueprint project cycle, it is imperative that design docs are reviewed
as fast as possible (i.e. within a week).  If reviews are needed on your design doc, mercilessly @channel
the project team Slack channel and/or DM people directly asking for reviews.

To conduct a review, Github's PR commenting feature should be used.  This will allow us to have a centralized
store of review feedback.  Given the open-ended nature of system design and balancing of tradeoffs, review 
comments should be worded as suggestions.

## Amendments

While the goal of ADRs is to flesh out all the details prior to commencing work, there's a very real 
possibility that an amendment to the original design is required.  Make sure to document these changes
by updating the design doc using a new PR.  These amendments don't require approval by VPP or another PL.
