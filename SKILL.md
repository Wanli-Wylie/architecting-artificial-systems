---
name: architecting-artificial-systems
description: Architect artificial systems, whether software, organizations or a mix of the two. Use when a question turns on the structure of a system, service, data model, process, team or organization: what should exist, who owns a fact, decision or component, where a boundary, layer or source of truth belongs, how units delegate, request services, share resources and coordinate, which requirements and measures bind, why a difficulty keeps returning, or how to change a running system without losing what it must keep doing. It covers a system under one shared governance and its dealings with outside organizations as clients and suppliers. Also use for writing or reviewing a design document or brief, for organizing design work among people and AI agents, and for questions like "how should we structure this", "who should own this", "should this be its own service", "is this over-engineered", "why does this keep breaking" or "is this the right problem", even when the word architecture never comes up.
license: MIT
---

# Architecting artificial systems

An artificial system is constructed, organized, or maintained in relation to purposes that cannot be derived from its mechanisms alone. Kant's notion of *Zweck* (purpose) provides a philosophical orientation: the purpose of an artificial system cannot be inferred from its mechanisms alone. This distinction need not be incorporated into the engineering model itself. A balancing authority's control of its part of a power grid, a hospital's consult workflow, an operating system, an army, a national air traffic control service and a national data exchange are artificial systems in this sense, and so is the team that designs any of them.

This Skill is about architecting a system under one shared governance: a common order, carried by law, charters, directives, adopted standards and contracts and by the bodies that maintain them, under which roles carry authority and responsibility and what actors cannot settle among themselves has somewhere to go. Within it, actors hold distributed information, capabilities and decisions, and they often organize in two ways at once. Vertically, an actor turns one of its actions into tasks for other actors, who may delegate in turn, so that a system of complete actors can act as one actor of a larger one. Horizontally, actors request and provide services, draw on shared resources under allocation, share information and support one another. The two structures need not be isomorphic, since a unit carrying out a delegated task typically also deals with actors elsewhere in the delegation structure, and none of this implies central control or a global planner. Many systems show only one of the two, or neither, and a good reading says so.

Designing the order among several independent authorities is a different subject, which this Skill does not treat; the independent organizations a system serves, buys from or depends on appear in its design as clients, suppliers or environment. This states the Skill's scope, not a test a system has to pass, and where governance is partial or contested the model is used as far as it helps.

The engineering model takes purposes up in their operational form, as what stakeholders require of a system and how it meets those requirements, and it sees one system from three perspectives. The logical perspective describes the objects, relations, states and actions the system recognizes and what each action means; the actor perspective, who holds which roles and tasks, with what authority and observation, and how actors decide, delegate and coordinate; the implementation perspective, the programs, devices, physical processes, people following procedures and external services that make actions happen. Systems are also layered by abstraction, by assembly, by distributed execution and by control over physical dynamics. An actor usually contains mechanisms that are not actors, and decomposition stops at a trusted boundary where a unit is taken as given.

Architecture works to make the perspectives correspond: important requirements have actors able to meet them, decisions have the information and authority they need, actions have a way to happen and to be seen to have happened, and constraints across actors have a place where they take effect. It also gives each structure a reason, such as a requirement met, a boundary spanned, a decision informed, a failure contained, a load spread or a change made independent. Structure costs building, consistency and operation, so designs tend to stay capable when what can be derived is derived, each fact has one source of truth however many copies carry it, and a premise is revised once a family of mechanisms has grown around it.

Use this Skill to design, review, diagnose or change such a system. It offers a model and its vocabulary, the activities around a system, and sixteen cases of real systems read in that vocabulary. The model and its heuristics are ways of understanding with uses and limits, and a design can satisfy every correspondence in the model and still be the wrong design.

## The model in brief

[references/model.md](references/model.md) develops the model in nine parts, grounded in the cases or marked as judgment.

Requirements reach a design in stakeholders' words, with a scope and a bound, and kept apart from the means that meet them, they let those means change. A measure binds where someone relies on it, and otherwise indicates something it captures in part and is revised when it drifts ([grid](references/cases/grid-balancing.md)). A requirement can come from beyond the governance boundary ([grid](references/cases/grid-balancing.md)) and can be served without being enforced ([X-Road](references/cases/x-road-estonia.md)).

Among the perspectives, the logical world directs and the implementation constrains. Delegation and horizontal coordination need not share a shape: joint doctrine runs operational command and administrative control side by side ([joint command](references/cases/joint-command-support.md)), the FAA's Command Center directs traffic management through units inside facilities that answer to their own line ([FAA](references/cases/faa-air-traffic.md)), and Borg's priority bands rank kinds of work, not teams, while its quota rules apply to every team alike ([Borg](references/cases/borg.md)).

A fact's source of truth sits with whoever has authority over it, not wherever it is stored, and what can be derived is usually derived, as SAP dropped stored totals and their reconciliation once in-memory columns removed their reason ([SAP](references/cases/sap-universal-journal.md)). A concept need not exist at runtime unless the running system does something with it, though a system may reify part of its logical world on purpose, at a price ([Palantir](references/cases/palantir-ontology.md)).

Authority given to whoever holds the information works when a response stands behind it, as an andon pull needs a team leader who comes ([andon](references/cases/toyota-andon.md)). Decisions generally go where information and the ability to change the outcome meet, centralized where consistency, fairness or scale outweigh local knowledge, and asking who decides often removes an agreement protocol ([Kubernetes](references/cases/kubernetes-controllers.md)).

Feedback loops run at tempos that overlap. Intent, acceptance, progress and outcome are distinct observations, as a VHA consult moves from Pending to Active to Complete ([VistA consults](references/cases/vista-consults.md)), and an unknown outcome is usually kept unknown until observed.

Layers have many reasons, each repaying the interface, failure mode and latency a layer costs; the end-to-end argument places a function where the requirement and the knowledge to check it coincide ([end-to-end](references/cases/end-to-end.md)). Delegation carries latitude, authority and a composition rule, as mission command's intent "describes what constitutes success" ([mission command](references/cases/mission-command.md)), and its recursive form fits parts of one kind that are nearly independent. Where layers act on one thing, each usually needs to know what the other may do ([MCAS](references/cases/boeing-737-max-mcas.md)).

Horizontal coordination runs through requests under contracts, allocation under an enforced rule, shared records that carry a process's meaning, support relationships a common superior sets up in joint doctrine, and agreements among units. The governance usually gives what actors cannot settle a place to go, and a join between separately owned parts works when it has a meaning and an owner of its own.

A designer first asks what the world already carries, as a balancing authority builds on its generators' inertia and governors. Structure that makes a property true usually costs less than a check, as Unix's rule against links to directories protects programs that walk the tree ([Multics and Unix](references/cases/multics-unix.md)), and checks earn their place where separately owned or trusted parts meet.

A design is read from its requirements down, through the correspondences, and from its structure up, by asking what each part is for. A premise that a family of mechanisms serves is best revised as one: on the 737 MAX one untested premise, that crews would retrim within seconds, served the hazard classification, the simulator method, the single sensor and the manuals at once.

## Vocabulary

One word per meaning, mostly words engineers already use; a source's own term stays the source's.

**Artificial system.** A system constructed, organized or maintained in relation to purposes its mechanisms alone do not give.

**Governance.** The shared order a system is architected under, which gives roles their authority and responsibility, admits the actors who fill them and settles what they cannot settle themselves; one order can carry several vertical structures. The **governance boundary** is where it ends.

**Stakeholder.** Whoever uses, relies on, is affected by or holds authority over the system, best named by what it would notice if the behaviour changed. Whoever uses an interface is its **client**.

**Requirement.** What stakeholders need of the system, in their terms, with a scope and a bound that can be a ceiling as well as a minimum. It may be a function or a quality, such as latency or availability, and qualities often decide an architecture.

**Interface** and **contract.** An interface is how a part is used, and its contract is what the part commits to its clients and requires of them, failure and "not yet known" among its outcomes. A contract may promise little where its clients need little, as datagram delivery does, and a requirement allocated to a part becomes part of its contract.

**Measure.** A quantity by which the system or a part is judged: a requirement that binds construction, or an **indicator** of something it captures in part, kept tied to what it indicates so that it does not take the place of what a task is for.

**Perspective.** One of three descriptions of one system, logical, actor and implementation, refined against each other rather than stacked.

**Logical world.** What the logical perspective describes: objects, relations, states, and actions with their intent, preconditions, effect, completion condition and reported result. Mechanisms carry it without being it.

**Actor.** A unit that holds a task and carries it out by observing, deciding and acting within its authority: a person, an organization, or a program that chooses among what its task leaves open, such as an AI agent. It is a description used where it helps, and a fixed law from inputs to outputs is a mechanism. A **complete actor** has its own decision, observation and execution and an interface through which another actor can use it, as a unit acts as one actor for the command above it.

**Role.** A position defined by tasks, authority and responsibility, which an actor fills. Roles come from a system's own design or from norms, standards, laws, doctrine, contracts and existing interfaces, and the governance decides how each acquires authority.

**Task.** What an actor is responsible for, a goal to reach or a condition to maintain, with constraints, resources, timing and the result it reports; it may be delegated, assigned to a role, stated as desired state or taken on by accepting a request. Its **latitude** is what it leaves to the actor's choice, best written into its definition, as a commander's intent is, rather than granted separately.

**Authority** and **capability.** What an actor may decide and invoke, and what it can actually bring about, which designs align by specification or through training. In control engineering a function's authority is the range of effect it may command.

**Policy.** A rule that settles choices a mechanism or task leaves open, kept apart from the mechanism so either can change. Sources also say "policy" for a whole written rule set.

**Feedback loop** and **controller.** A feedback loop runs from decision through execution and observation back to decision, at a tempo matched to what it acts on. A controller runs one by a set law, as a governor does by its droop setting; a Kubernetes controller, choosing how to reach a desired state, is also usefully called an actor.

**Observation.** Information a decision can use, with its scope, time and certainty. A **state estimate** is an observation with a source and an uncertainty, read by choices and kept apart from commitments.

**Mechanism.** A real means by which an action happens or a constraint takes effect: a program, a device, a physical process, a person following a procedure, an external service.

**Layer.** One step in a hierarchy of realization, whose interface is the specification that what lies beneath realizes. Delegation is one form of layering, and a source's "level", "tier" or "echelon" stays the source's.

**Delegation.** The vertical structure among actors: an actor turns one of its actions into tasks for others, with latitude, inherited authority, constraints and an expected result, and reads what returns by a composition rule. A source's wider "delegate", such as airspace passed between FAA facilities, stays the source's.

**Service**, **request** and **allocation.** A service is a capability an actor offers others under a contract, and a request asks for it; the provider decides how to meet it, its responsibility coming from its own acceptance rather than a task handed down. Allocation divides a shared resource by quota, priority, schedule, admission or price under a rule an allocator enforces. Other horizontal relations, such as shared records and support (which joint and Army doctrine define differently), keep their sources' names.

**Composition rule.** How results from parts establish a result of the whole, which asks more than every subtask having ended, as a Kubernetes Deployment is complete when its replicas are updated and available. Where a design rests on an assumption instead, or a source states none, naming the gap is the term's use.

**Boundary.** Where ownership, execution, trust or lifetime changes. Interfaces, stored state, protocols and checks most often earn their cost there.

**Trusted boundary.** Where a design stops decomposing and takes a unit as behaving by its contract, outcomes such as failure, partial results and "not yet known" included. Those outcomes are the design's real assumption about the unit.

**Owner** and **source of truth.** An owner is the actor responsible for a part or a body of state and authorized to change it. A source of truth is where a fact's authoritative value lives, a matter of authority rather than storage; what creates work is a redundant one, two places authoritative for one fact with no rule between them.

**Correspondence.** One of the links that make the perspectives one system: requirement to the actor who meets it, decision to its information and authority, action to its execution path, claimed result to its observational basis, constraint across actors to its place of enforcement.

**Draft design.** A concrete arrangement a reader can argue with (actors with tasks, messages with fields, states with transitions), held as the reference that questions are asked of rather than as a verdict.

**Invariant.** A property meant to hold in every reachable state and through every revision, written with the failure it prevents.

**Reformulation.** A change in what is asked or how it is represented: a re-rendering asks the same question more cheaply, a replacement answers a different question in the original's service, and a change of what is asked answers to the stakeholders who rely on it, so each is tested differently.

## Activities

The activities interleave and are not stages, and a session goes better when it says which activity it is in and, on switching, why. [references/activities.md](references/activities.md) describes what good work in each looks like.

Formulating what is required names stakeholders, requirements, measures and the objects and actions that matter, starting from the governance the system is under. What is asked is a representation and can be wrong, and a need stated in the shape of a mechanism is separated from the restriction it implies.

Architecting decides roles, what is delegated and what is coordinated horizontally, layers, boundaries and sources of truth, working from a draft design. Each structure gets its own reasons rather than being read off another's shape, and saying which structures a design has, and which it lacks, is part of the design.

Realizing builds, procures and reuses, and reads construction as evidence, since a field added to keep a concept alive can mean unfinished code or a design asking for what need not exist. A reused part is asked again about its new environment.

Operating and observing runs the loops at tempos matched to what they act on and keeps each indicator beside what it indicates, so that a measure does not take a goal's place (Merton's goal displacement).

Diagnosing and reformulating reads a difficulty three ways before repairing it: a capability the system lacks, a design demanding what need not exist, or a formulation producing the difficulty.

Evolving changes a running system at its premises rather than trimming mechanisms one by one, says what each removal leaves holding and what now carries it, and keeps compatibility as a contract with clients who cannot change in step.

Describing a design marks which statements bind and which explain, states each thing once where it is owned, and says where the design stops.

Organizing the work treats the design effort as an artificial system of its own, with people and AI agents as its actors, briefs as delegation, one shared working document as its logical world, and only questions of meaning sent up to whoever holds the meaning.

## Cases

Each case reads one real system or design from public sources and says where the vocabulary strains or adds nothing. The Skill teaches through cases because, as Naur argued, the theory behind a design cannot be fully recovered from its artifacts.

- [Palantir Foundry Ontology](references/cases/palantir-ontology.md): a logical world reified for people and programs to act on, and "done" as a configuration choice.
- [SAP Universal Journal](references/cases/sap-universal-journal.md): stored totals removed as one family when a premise about cost changed, with compatibility views as a thin contract.
- [An X-Road instance](references/cases/x-road-estonia.md): members admitted into a standard's roles, registries that stay their own sources of truth, and an exchange with its own owner.
- [Mission command](references/cases/mission-command.md): delegation by intent, with intent as the composition rule, and doctrine on when tighter control fits.
- [GCCS-J](references/cases/gccs-j.md): a shared picture operated and secured along separate lines, with "fusion" where a composition rule would be.
- [US joint command and support relationships](references/cases/joint-command-support.md): graded command authority, and support set up by a common superior between commanders who do not command each other.
- [The FAA's air traffic organization](references/cases/faa-air-traffic.md): two vertical structures, handoffs and letters of agreement between facilities, and an order that defines its verbs.
- [VistA consults](references/cases/vista-consults.md): services requesting and accepting work through a record whose statuses separate intent, acceptance, progress and outcome.
- [A balancing authority](references/cases/grid-balancing.md): physical processes, controllers and dispatchers at overlapping tempos, under requirements from beyond the governance boundary.
- [Kubernetes controllers](references/cases/kubernetes-controllers.md): delegation as desired state and observed status, and field managers as owners.
- [Borg](references/cases/borg.md): allocation by priority, quota, admission and placement, priced outside the system that enforces it.
- [Multics to Unix](references/cases/multics-unix.md): a layer by interface, ownership deciding where a function went, and a change of what was asked, with its cost.
- [The end-to-end argument](references/cases/end-to-end.md): a function placed where it can be completed and checked, a thin contract, and fate-sharing.
- [Toyota andon](references/cases/toyota-andon.md): authority to signal an abnormality, made usable by a team leader who answers and a fixed-position stop.
- [Google SRE's service level objectives](references/cases/sre-slos.md): a measure as a binding requirement, and an error budget that settles release pace.
- [Boeing 737 MAX MCAS](references/cases/boeing-737-max-mcas.md): the one failure case, an automated layer whose authority grew while the crew's knowledge stayed behind.

## Going deeper

Open [references/model.md](references/model.md) when a question turns on structure: where a fact or a decision belongs, what a layer is for, how delegation composes. Open [references/activities.md](references/activities.md) when it turns on the work: stating requirements, diagnosing a difficulty that returns, changing a live system, writing a design down. Open a case when a situation resembles it, or to see how a term applies and where it strains.

## Revising this Skill

The Skill is itself a representation, drawn from sixteen cases, and fitting them does not show that it fits the next system. It is meant to change when applying it produces a worse design or misses a decision that mattered, and the reason can be stated generally; one surprise is a case to record, a pattern across cases a reason to revise. Revise it as it revises a design: change a premise rather than add a special case, say what a removed passage protected and what protects it now, and watch for its return under another name. Rewrite the affected text whole, with no history inside it, add the case to `references/cases/` where public sources can carry it, and add a row to [CHANGES.md](CHANGES.md).
