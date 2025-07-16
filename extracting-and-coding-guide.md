# Incident Report Extraction and Coding

This guide documents our process for extracting and analyzing the action items (AIs) from incident reports (IRs). The input for the analysis is an incident report, and the output is a YAML file (one YAML file per incident report) that has an entry for each AI in the IR and includes the summary or "coding" properties described below. Note that values `UNCLEAR` or `UNKOWN` are used when the IR is not sufficiently clear or the IR authors themselves didn't know. A full list of possible values for codes (though obviously not the summary properties).

## Motivation for the AI

These YAML properties capture aspects of the incident that influenced the AI. We will use the IR-54 as a running example. 

* `experience:` A summary of the incident experience(s) that influenced the AI. For example: *Service became overloaded during a traffic spike.*

* `lifecycle:` During what stage of the incident did the experience occur in? At the top level, these are the failure and the response, with a sub-category after the slash. For example: *Failure / Inception.*

* `iso:` The ISO 25010 characteristics the experience relates to. For example: *Capacity.*

* `tags:` A number of non-mutually exclusive properties. These can be seen as themes that help explain the experience in terms of the *behavior* and/or the *scenario* experienced. For example: *high load (spike, overloaded service).*


## Evolution proposed by the AI

These YAML properties capture details about the proposed evolution and its intended effects. 

* `action:` For example: *Make auto-scaling more aggressive.*

* `change-type:` Inspired by Buckley and Mens' work, but we have modified it to better capture the AI instance in our dataset. We suppose it is natural that some change types may not be relevant to their work (on tools for modifying source code) and our more broad focus on AIs to socio-technical systems. 

change-type: evo / alter
action: Make auto-scaling more aggressive
target: Service auto-scaling infrastructure (feature enablement service)
sts: 
   - Tech / Core
intended-effect: 
   - Flexibility / Scalability (behavior at scale)

intention:
goal: Better handle traffic spikes
google-ai: prevent
coding:
   - Handle repeat event (within some range)
   - Extend range (rate of spike)

other:
modification: Tune auto-scaling behavior (more aggressive)
activity: reconfigure
level: component
temporal: new



This guide documents the process of converting the VOID Dataset CSV to YAML files with the correct set of extracted and coded AIs. This process is as follows:

1. IR report is read and included if it satisfies the inclusion criteria.
2. A YAML file is generated from the IR that lists each AI described by key properties and appropriate codes
3. Using grounded theory, we perform an on-going analysis of each AI and add and refine the codes


### Extracting

#### 1. Read public IR linked at top of YAML file
If it does not match the inclusion criteria (e.g., not an incident report, url does not work), then take the last incident report and rename it to be that incident, and then update in `incidents_included.csv`. Note your name in `extractedBy`. Immediately commit and push the name change to reserve the incident report

#### 2. Begin the extraction process

Extract:
   1. IR description comment
   2. For each AI,
      1. Summaries: `action`, `target`, `goal`
      2. Mandatory codes: `sts`, `google-ai`
      3. Optional Codes: `change-type`, `iso25010`, `temporal`, `themes`
      4. Memos
   3. IR-level memos, including concepts like `ordering` and things which are not covered by other fields but which we might want to start extracting later
   4. IR-level patterns

We have included a description of each property below that you can use to guide extraction. When you have finished extracting an incident report, add to the comments at top `[TODO] Needs review`

Notes:
   - Do NOT extract actions performed during the mitigation unless explicitly marked as "Action Item"
   - Extract only as you are able. Annotate with these when unsure:
      - `UNCLEAR`: IR does not provide this information or sufficient information. Only make reasonable inference.
      - `UNKNOWN`: Authors of the IR (not the researchers) did not know something and say so
      - `(VAGUE)` the IR is not specific about something (i.e. an action)
      - `[TODO]` note of issues, notes for reviewers, notes of reviewers, or undone things
   - If you need to commit (e.g. to save partial progress) then add a `[TODO]` at the top in comments which says extraction incomplete and finish at a later time.

### Description of IR YAML Properties

- `patterns`: No prescription for format, but include interesting ideas, which we will refine through later use of grounded theory.

- `memos`: No prescription for format, but include interesting notes. For example, :
    - `ordering` (memo): If there is an ordering suggested in the IR about what order to do AIs, then make note of that in the memos for the IR (not the AI). Inspired by Buckley and Mens. The reason we are interested in this is because we could ask why they want to do them in a certain order. Is it because of dependencies, is it faster then better, etc.

### Description of AI YAML Properties

Both top level categorizations use categories that come from existing work (with some important adaptations) though our work is the first time these categorizations have been applied to FDSE (or similar) as far as we know. These are relatively coarse-grained and organize the data around two simple dimensions. 

* What part(s) of the system are effected by the proposed action (see sts below), and
* Why is the action being proposed (see google-ai below).

Some of our other coding is inductive, that is we collaboratively defined them ourselves as we examined the data and sought to understand in more detail the nature of the changes being made to systems. These are relatively find-grained and each relates to one or more of the dimensions mentioned above.

#### STS

Previous work on socio-technical system theory, resilience engineering, (or what ever you call this area) has shown the importance of considering the broader socio-technical system when trying to understand a system failure--but here we are using it to better understand the changes being proposed. Our interest in this branch of research came from our preliminary analysis, which showed that proposed changes target more than just the core system [MO2RE 2024].

We have categorized all of our AIs along two main (and broad) dimensions or aspects. The first is based on *the part of the socio-technical system* that the AI will affect or change. The categories we are using come from previous work and includes the following [Davis 2014]:

`sts`: The part of the socio-technical system that the action will be affected by the change.
- `Culture`: The culture, norms and values that underpin the work of an organization and the interactions between people.
- `Goals`: The plans and objectives of an organization, some of which may be captured in roadmaps or other planning documents.
- `People`: The staff employed by an organization, along with the roles they fulfill and how they are organized.
- `Process` and procedure: Formal and informal processes and procedures an organization uses to do its work. 
- Buildings and `infrastructure`: The buildings and other physical assets used of the organization in the creation and operation of systems.
- `Tech` (referring to software/application)

The majority of the AIs in our dataset affect the technical aspects of systems, suggesting a more fine-grained categorization might be helpful for understanding our dataset. So, looking further at these AIs we have identified several subcategories of technology that capture important variation in our dataset:

- `Tech / Core`: The core technical system that provides the primary business and user value. 
- `Tech / Support`: Software systems that existing to support core systems and to support people in operating and managing the core systems.
- `Tech / Infrastructure`: Low level technical infrastructure. [TODO] JS: Looking at the coded data AIs I'm not sure if we need Tech / Infrastructure.

Note this quote from the Davis paper:

> A work system will usually have a set of goals and metrics, involve people (with varying attitudes and skills), using a range of technologies and tools, working within a physical infrastructure, operating with a set of cultural assumptions, and using sets of processes and working practices.

From that quote we assume that what Davis means by "Technology and tools" is actually really the "Technical / Support" category we have defined above. 


#### Google-ai

The second top-level dimension captures a high-level notion of *why the change is being made*, specifically as it relates to the incident that just occurred. The categories we are using come from previous work [Lunney 2017] and includes the following:

`google-ai`:
   - `investigate` this incident: what happened to cause this incident and why? Determining the root causes is your ultimate goal. Examples: logs analysis, diagramming the request path, reviewing heapdumps
   - `mitigate this` incident: what immediate actions can we take to resolve and manage this specific event? Examples: rolling back, cherry-picking, pushing configs, communicating with affected users 
   - `repair` damage from this incident: how can we resolve immediate or collateral damage from this incident? Examples: restoring data, fixing machines, removing traffic re-routes 
   - `detect future` incidents: how can we decrease the time to accurately detect a similar failure? Examples: monitoring, alerting, plausibility checks on input/ output 
   - `mitigate future` incidents: how can we decrease the severity and/or duration of future incidents like this? How can we reduce the percent of users affected by this class of failure the next time it happens? Examples: graceful degradation; dropping non-critical results; failing open; augmenting current practices with dashboards, playbooks, incident management protocols, and/or war rooms 
   - `prevent future` incidents: how can we prevent a recurrence of this sort of failure? Examples: stability improvements in the code base, more thorough unit tests, input validation and robustness to error conditions, provisioning changes

Note that given how we are extracting AIs, we expect that the first three categories will rarely appear in our coded data.

#### Coding block level

In addition to the top level coding just described, under `coding` we are considering a set of five codes. The following is an overview, but note that when one of these is not applicable, we just leave it out.

**Change type.** Our notion of `change-type` is inspired by Buckley and Mens' work. We have modified it to better capture the AI instance in our dataset. We suppose it is natural that some change types may not be relevant to their work (on tools for modifying source code) and our more broad focus on AIs to socio-technical systems. 

  - `evo / add`: Add something not formerly present in the system
  - `evo / subtract` Remove something that was formerly present in the system
  - `evo / alter` Modifying something present (e.g., by adding and removing). Examples: Replacement, renaming, redesigning
  - `evo / UNCLEAR`: Change the system, but not sure if that change is by addition, subtraction, or alteration
  - `formative` Does not change the system. Examples: preparative actions like investigation, identifying and prioritizing actions like reprioritize existing work)
  
**Temporal.** We are capturing a simple `temporal` dimension for the AI, that was initially inspired by the observation that some AIs refer to work that was already planned. So far we have seen the following cases:

  - `new` the work is newly planned during the post-incident analysis,
  - `previously started` the work predated the post-incident analysis, or
  - `backlog` the work was in the backlog but had not yet been started.

**Modification.** Captures the change being made to the system (or at least proposed). That is, once the action item is complete, *what will be different about the system?* Eventually this will likely be around 12 categories (identified by the first word in the code value) but for concreteness here are some current examples:

  - `Formalize maintenance process`,
  - `Automate status update operation`, and
  - `Reduce query frequency`.

**iso25010.** What do we want to be different about the system so that it accomplishes some goal? It is important to note that the coding related to constraints is relevant here (as constraints are a type of nonfunctional requirement for systems).

Use the potential values found in the [ISO 25010 specification](./iso250102023.md).

