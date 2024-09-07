# PURE / Legend Retrospective

## History

In 2014 I was one of the early developers on a project a Goldman Sachs to build an environment 
that made it easy to model and share data
The lead of the project was Pierre De Belen. Pierre had been working on the project on his own and now had the buy-in 
to turn it into a fully-fledged platform that he called Pure.
I had been working on a project to share domain models across Finance and the Risk divisions that used a previous version 
of the concept (MOJO), Pure was his next generation version of that to do this across the bank

It is one of the most fun, ambitious and challenging projects I have worked on and whilst I don't think we got everything right, 
there are many principles and benefits that are extremely powerful and I still look for today and miss at other firms

In 2020 it was open-sourced under the name [Legend](https://legend.finos.org/) [Legend GitHub](https://github.com/finos/legend)


Conceptually, what are we trying to do in Finance ? Model the world - the concepts, the relationships and how they interact
A simple equity gives rise to more complex instruments, with underliers that are 

## The key concepts

- Define a model of the key logical concepts in a way that is precise and extensible and correct.
- Separate the logical model from the physical execution engine to allow those to change at different rates. You should not have to rewrite your business logic just because a faster DB came along
- Execute your business logic against the logical model. The model must execute to prove it is correct. It should not just be a paper UML model/diagram

Definitions
- A single precise definition of what something is across the whole bank

### Correctness
Pure was based on formal meta-modelling with proper concepts for M1-M4 see https://en.wikipedia.org/wiki/Meta-Object_Facility.
It included its own programming language - functional programming with classes and inheritance and gives compile time feedback on errors
- Cardinality can be specified precisely as part of the type system
- Constraints and validation part of the model
Changes can't break others
- Compiled so if you rename a property that some depends on and don't rename them you won't be able to commit
- SQL and mappings also compiled, no strings floating around in Python code where a typo can cause failure
Point-in-time query correctness built in (temporal/bitemporal milestoning)

Testing built-in, able to define tests and those run on each commit

Documentation built-in
Uniqueness - 

### Easy for Developers - fast time to market
- Interactive web based IDE to define and commit models, no set-up required
- Every query function was instantly a REST service once committed
- Data entitlements baked in at the store level, kerberos delegation all the way through, or for DB. 
- Discoverable - all models are in the environment, can easily find and use them
- Queries can execute in the IDE, giving real results from the database/store

### Extensible
- Associations are separate entities
- Separate universes to allow developers to work independently
- Projections of models to allow consumers to easily query each others data

### Maintainable
- Projections defining what you use, can see what consumers are using
- Runtime statistics
- Refactoring
- Lineage

### Business User (non-developer) friendly
- Data browser with interactive queries against the models
- Curated universes to provide a reduced guided set of relevant concepts/attributes for users
- Plugins to QlikView and other BI tools

## The business case

After the financial crisis, much more focus on liquidity, capital and other traditionally back office functions.
A single definition across the whole bank
Reduces reconciliations and streamlines communications
Instead of having to ask a team what does this mean, what is this, can consume a model

Shifting from a data river concept - everything flows downstream to a data lake concept, we all contribute

Executable specifications, no wasting time with documents that define things and are out of date, our definitions are in code and execute

## An example

Model

Store

Mapping

Function



## Lifecycle and sharing (SDLC)

### Phase 1 - Monorepo's are great!

Started as a monorepo for all models & mappings. I'll avoid discussing the pro's and con's of monorepo's here, but Goldman Sachs has a very 
successful monorepo for SecDB, so choosing a monorepo approach at the beginning was something that had a lot of backing,
it also made sure you can get compile time feedback across the whole platform.

Categories of models
"Enterprise" vs "Datamart" areas
Enterprise - "blessed" core models to be used by everyone for critical concepts that everyone needs, 
such as reference data (Entity, Account) and key financial products
Datamart - one per sub-org, Operations, Finance, FICC, Equities
This was a less "governed" area where BU's could have their own models
It also allowed for the possibility of private models spaces, for example for HCM/HR where perhaps the model itself should not be public
Consumer queries (functions) were in the 

Groups of model reviewers per domain/folder structure enforced this mapping
Contribution - anyone could propose a change

In general developers outside the core platform team worked with the enterprise models and their organizations datamart 
open in the IDE

If a model needed to be shared across Org's, it had to be promoted into the "enterprise" space.
Dependencies not allowed between datamarts.

To avoid everyone needing a shared database, each BU could map the enterprise logical model to a different store.
We partnered with Data Lake/warehouse teams so that each team could provision an OLAP (initially Sybase IQ) database with the schema


Versioning
In general the idea was to keep everyone on the same model and do a mono-repo style push (i)

Once a model gained a lot of dependencies, with many teams depending on it and code in codebases outside consuming the data, this didn't scale.
Solved for the ISDA/Derivatives model (largest model) by introducing logical versions for anything that was a breaking change
This was a full copy of the model, and multiple versions coexisted

v1::cdm::....
v2::cdm::

Tooling was added to make this easy, to create the initial copy

#### Phase 2 - Federated SDLC - Goodbye monorepo

*This change was made after I had left the team, but I was a user of it and maintained close relations with Pierre

Mono-repo's are controversial, spend endless time debating them with teams
Practically, compile times can't keep up as models and dependencies grow. Easier with non-compiled languages
Pressure to fit into "standard SDLC tooling" - git doesn't scale passed a certain size, no appetite to use Mercurial/other bespoke solutions from big tech
Open-sourced the platform so also wanted to collaborate in future with other financial institutions
Difficult to convince all dependent teams to go-live with a change at the same time

How:
Split the repo up into sub-domains and introduced versioning tied to git commit
Namespacing
model.account.
model.legalentity.
model.cdm. 

Different namespace for external models from outside, versioned to match those (CDM)

Each in a separate git repo & workspace. Automated set-up of these repo's


How?
Now when a developer starts to model.
Developer goes to online portal and creates a "WORKSPACE", select from a drop-down of other model universes you want to include, 
can include enterprise models
WORKSPACE has entitlements, can add developers, reviewers to the workspace, keep it public/private
Auto-upgrades for backwards compatible changes?
Developer controls when to consume a new version of the model
Build system automatically builds and runs tests for your downstream dependencies (?)

Human side - organization (aka Governance)
Need to decide who is the custodian/owner of a specific enterprise domain, easier if your org is clear, 
single market data team, 


## Execution platform

Milestoning propagation for consistent snapshots through joins.

Cross-store joins



How did it scale?

Streaming from the cursor straight through.

Bottleneck/overhead ?
We measured this, and found that for query results because we streamed results from the cursor on the database and 
serialized to JSON as we streamed the bottleneck was always the IO on the database. 
We were primarily dealing with OLAP db's such as Sybase IQ, so results are returned in seconds to minutes, not ms.

For Mifid trade reporting we created a faster version with DB2 that could do sub-second

Isn't this an ORM? THose are terrible and generally don't scale ?

Functional programming, TDS protocol, not just objects, can have quite a disparate mapping between an optimized store and a model

What about the generated SQL, doesn't it create monstrous joins that the DB can't handle?

## Challenges 

### Correctness of models
"All models are wrong some models are useful"

Developers are in general not very good at proper domain modelling, tend to think in databases
A good model is highly normalized, uses true business concepts with full names
Need to understand OO concepts of when to use associations vs inheritance
Trained reviewers are essential

We ended up with lots of bad models and duplication. Solved by building up a few teams that owned key models that are required by everyone, for reference data
Used CDM model for derivatives (mostly), already defined and has a process to evolve

Some vendors provide ok models - descriptions/data dictionaries that we can import, such as Bloomberg
This was imperfect as it tends to also be specific to how they transport files/API's

Just like code, it takes education and effort and curation to keep things clean and managable

"I will never get my large org to agree on a model"
This can be painful, and take time, but that is the valuable part, getting parts of the org to agree on a definition
The act of modelling and discussion is valuable, building consensus
This can be avoided/streamlined by taking an existing industry model, such as CDM for derivatives


### Retro-fitting into an existing environment
SecDb already had all the key models for pricing (UFO's - Unified Financial Objects), with it's own language Slang.
We were never going to be able to move that out
Our models ended up being from the extract of SecDb down
 

### Developer buy-in to proprietary tech
Developers want to use the programming languages they are used to - "Why learn your proprietary language, why can't I just use Java/Python/..."
This is partly because they are mindful of their career prospects and want transferable skills.
They especially don't want to learn your language when the tooling is not as polished and the error messages not always easy to understand
Standards for language tooling have increased and investment in mainstream languages far outstrips what you can do
Goldman Sachs has always had proprietary languages (Slang in SecDb) and has always maintained that you hire smart people, 
they learn fast, but developers no longer look for a job for the long term, so the investment is not something they are as bought into.

Tooling - building tooling for the language - refactoring, syntax highlighting, debugging etc.etc. is expensive
Has become easier, language server protocol.
A financial firm is not going to commit $$$$ to a huge language teams.

Pierre/our team always maintained that we didn't want to own a language. We just couldn't find an existing one with the properties we needed.
We looked for a language that does all these things, functional and OO, with reflection/meta-modelling capabilites
We haven't found one yet.

To some extent Pierre has now solved this, with everything being (JSON) models. You can use the language, or you can use JSON definitions/services


### Scaling SDLC
The sections above that describe evolutions of the SDLC/development lifecycle
This was challenging and difficult to do fast enough
The environment became slow and unmanageable for some time
This is similar to all programming languages where if you don't modularize, remove dead code, and improve compile times, things grind to a halt.
Collaboration at scale is hard, and versioning, but with the modular SDLC I think this can work


### Time-to-market for execution platforms
There will always be new DB's teams want to use and new execution platforms.
This has exploded in recent years with many new contenders from Cloud providers to vendors like Snowflake
Onboarding a DB requires
1 - understanding the SQL dialect
2 - building an entitlements model
3 - getting a test environment and drivers
For an easy DB with mostly standard SQL this can take a couple of weeks, but keeping up with these is a lag and a burden
This is not unique to Pure/Legend. Other platforms that support connectors to multiple DB's encounter this
Solutions such as Calcite and IBIS/Substrate are emerging to help other data solutions abstract that

### Data entitlements to databases
We wanted to make it easy and the data secure, so instead of having entitlements in the service layer (app layer),
we insisted on having them at the database layer itself.
This means the database needs to know who people are and allow individuals to have access to it
For some types of data it needs a mechanism to enforce row-level entitlements
We didn't want to store passwords due to the security concerns, so we also need SSO through the database
Some databases support Kerberos entitlement with propagation of credentials, but not all
Newer platforms support OAuth
We had systems to retro-fit these kind of entitlements to other databases called SecureConnect, using control tables and views with joins for row level

### Scaling the language
Compile times, compiling with type inference is complicated. The language supported inheritance and generics.
C3 linearization for type coercion/resolution.

Incremental compilation is essential, to only recompile what has changed, this requires invalidating a graph. Doing this accurately is hard. 
In the mapping grammar we tend to invalidate too much, as that is cleaner/safer (no bad state), but this means incremental compilation on large mappings takes along time

Inheritance is expensive, supported multiple inheritance initially, not as supported now

### Market data and more real time use cases
We always had ambitions to include market data and live-streaming/ticking. 
The level of engineering required is higher, and latency requirements. 
We never executed on this vision, but the concepts and the platform are set-up so that this could happen.

## Differences & Similarities
Isn't this similar GraphQL ?

What about writing data, this looks like read-only queries ?

Why not just use SQL ?
- cannot express behaviour
- SQL Standard is weak, can't use it as an abstraction across different databases as each one is different
- Wanted to support things like Spark, not just databases

What about Spark? 

What about Domain Driven Design and bounded contexts ?
Isn't it ok for everyone to have different models if useful for them ? Yes, until it hurts your business - 
The financial domain is a bounded context, I believe we can/should be consistent within that

These ideas aren't new - what about Microsoft's OData - https://www.odata.org/


## Conclusion - Would I build it again ?

The compile time feedback is amazing. Much better than XML or YAML. Avoiding typo's in SQL

The model is valuable, I find this is required and SQL is not enough. You want to see the descriptions and human read-able names and express constraints

Associations/relationships as separate first class elements is a big differentiator and allows modularization/extensibility

Timestamp propagation/consistent snapshots of joined data is hard, having a framework to do this is for you is valuable

Having your own programming language is expensive, I would try very hard to avoid, but a functional/constrained language is essential here

UI's are difficult and expensive to do well, none of our model editing UI's really ended up being where they need to be
I'd stick with text and visualizations or plugging into other UI's

The mapping grammar was never intuitive, I'd change that, developers tend to prefer mapping from the store

## Other notes

Incentives - how to produce a win-win, if you model the data, you also get this
DSF? framework in Slang where if you named things correctly you would automatically get joins




