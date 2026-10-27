# internal-source-and-method-precedence

An agent skill that sets the order in which an AI assistant consults data
sources and methodology skills:

1. Internal data sources first (a primary source, then a secondary one), then
   public or built-in databases.
2. Custom organization-defined skills before built-in skills.
3. Explore what each internal resource can actually do before planning, and
   sweep all resources against remaining gaps before answering.

It adds no retrieval or analysis capability of its own; it only decides which
source or skill is called first.

## Use

1. Copy `SKILL.md` into your skills directory (or create a skill from it in
   your assistant's skill manager).
2. Replace `PRIMARY_SOURCE` and `SECONDARY_SOURCE` with the names of your own
   internal data sources.
