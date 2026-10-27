# Architecting artificial systems

An Agent Skill for architecting artificial systems, whether software, organizations or mixtures of the two, under one shared governance. It looks at a system at two layers: a metaphysical layer, what the system is in its own terms (the things it deals in and how they relate, what happens to them, who acts and answers for what, how work is handed down and coordinated across), and a physical layer, whatever carries that out, from programs and machines to people and organizations, each working by its own field's principles, which the Skill does not contain. Of anything a system keeps that matters it asks how it comes to be and who may change it. It describes the activities around a system, from formulating what is required to evolving what already runs, and it reads sixteen real systems in this way, among them Kubernetes controllers, Google's Borg, US joint command, the FAA's air traffic organization, VistA consults, Estonia's X-Road and the 737 MAX's MCAS. It is written as inquiry rather than as a formal system, with each field's own words kept where they serve, and its heuristics are ways of understanding, each with what it is good for and where it stops, not rules.

## Who it is for

Anyone, person or AI agent, who designs, reviews, diagnoses or changes a software system, an organization or a system that mixes the two: deciding what should exist, how the things that matter come to be and who may change them, where a decision, boundary or layer belongs, how units delegate, request services and share resources, why a difficulty keeps returning, or how to change a system that is already running. It is written first for frontier language models, in narrative prose, and serves people who brief them, or who want one way of thinking about structure across software and organizations.

## Installing

The repository is the Skill directory itself, so cloning it into a skills directory installs it:

```
git clone https://github.com/Wanli-Wylie/architecting-artificial-systems.git ~/.claude/skills/architecting-artificial-systems
```

That makes it available in every project. To share it with everyone who works in one repository, clone it to `.claude/skills/architecting-artificial-systems` at that repository's root instead. The directory name matches the `name` in the frontmatter of `SKILL.md`. To update, pull in that directory.

Other environments that follow the Agent Skills specification can load the directory as it is: `SKILL.md` with YAML frontmatter and Markdown instructions, and a `references/` directory of Markdown files read only when needed. There are no scripts, assets or dependencies.

## How it is used

Claude Code reads the name and description from the frontmatter of `SKILL.md` and loads the Skill when a task matches; it can also be invoked by name, as `/architecting-artificial-systems`. `SKILL.md` carries the whole in brief: the scope, the two layers, the model in brief, the activities, a pointer to each case, and when to read further. The references are opened only when a question needs their depth: `references/model.md` for questions of structure, `references/activities.md` for questions about the work, and a case when a situation resembles it. The closing section of `SKILL.md` says how the Skill is revised when experience shows it wrong.

## Layout

```
architecting-artificial-systems/
  SKILL.md                         the entry: scope, the two layers, the model in brief, activities, cases, revising
  README.md                        this file
  CHANGES.md                       the change record, newest first
  LICENSE                          MIT
  references/
    model.md                       the model in ten parts
    activities.md                  formulating, architecting, realizing, operating and observing,
                                   diagnosing and reformulating, evolving, describing a design,
                                   organizing the work
    cases/
      palantir-ontology.md         Palantir Foundry Ontology
      sap-universal-journal.md     SAP ERP and the S/4HANA Universal Journal
      x-road-estonia.md            an X-Road instance and its governing authority
      mission-command.md           US Army mission command
      gccs-j.md                    GCCS-J and the common operational picture
      joint-command-support.md     US joint command and support relationships
      faa-air-traffic.md           the FAA's air traffic organization
      vista-consults.md            VistA consults in the Veterans Health Administration
      grid-balancing.md            a balancing authority's balancing system
      kubernetes-controllers.md    Kubernetes controllers
      borg.md                      Borg at Google
      multics-unix.md              Multics to Unix, and the kernel boundary
      end-to-end.md                the end-to-end argument
      toyota-andon.md              Toyota andon
      sre-slos.md                  service level objectives in Google SRE
      boeing-737-max-mcas.md       Boeing 737 MAX and MCAS
```

## License

MIT; see [LICENSE](LICENSE). The Skill may be copied, adapted and redistributed with the copyright notice kept.
