# Nimble Data Management

Rapid Response Research (RRR), as “quickly deployed scholarly interventions,”
especially rely on toolkits and nascent scholarways that aim to reduce
obstacles in our paths or corners around which we have to slow to turn. The
introduction to RRR describes it from many different perspectives, including
team management, makeup, scope, and the like. Here, instead, we offer some
more narrower thoughts regarding specifically the role data management.

Given the centrality of data acquisition and analysis to RRR, rapidly
developing a data management plan in order to lessen confusion and
inconsistency when teams race to manipulate adjust the data for their own
specific needs becomes paramount, especially early in the RRR lifecycle. In
recognition of this, we offer, in lieu of a bullet list of best practices,
ruminations on what appear to be the two core concepts to RRR data management,
which likely extend, when possible, to data management in general:
immutability and centrality.

## Immutability

As data storage becomes cheaper, the service of treating data as immutable
becomes more and more realizable.

Having immutable data does not mean that the RRR team is not allowed to
manipulate or analyze data they acquire. Instead, it merely recommends that
all changes be made to ephemeral *copies* of the data. One similar process is
[nondestructive
editing](https://helpx.adobe.com/photoshop/using/nondestructive-editing.html)
in an image or audio editing program, where all of the filters, crops, and
changes occur such that the original photo or recording remains untouched.
Similarly, a software solution like
[Datomic](https://docs.datomic.com/on-prem/architecture.html) attaches
immutability to a database architecture, where immutable facts are stored over
time. Even Git, with its model of chained commits, comes close to representing
immutability.

At the cost of increased data storage, what these examples share is the
ability to revert backward, to provide an “infinite undo” as part of the very
architecture. So one instant win for the RRR team is that if a mistake gets
fed into the data analysis point, Humpty Dumpty of the dataset *can* be put
back together again.  Of course, “infinite undo” is a feature in, say, Google
Sheets, which suggests that it alone is not enough reason to think manage data
with immutability at the center.

More important to the RRR team are the gains in accountability,
reproducibility, and multiplicity provided by having an immutable data store.

### Accountability

In a RRR situation, the team will probably be collecting, harvesting,
capturing, or in some other way extending control over data that has been
prepared by others. Under ideal circumstances, the collection process is
downloading a mere table or scraping a single website. Nevertheless, even at
that point, accountability is important. Where, when, by whom, and how data was
acquired should be recorded alongside the actual data itself. Furthermore, the
more automated the process of acquisition is (through scrapers, scripts), the
better. Though relying on someone else’s data is always risky, as they can
change the format, API, or whatever at any given moment, the window of RRR
should provide accountability and transparency in acquisition.

Once the data is acquired, of course, by treating it as immutable, the RRR
team maintains that strong link to accountability. They can always return to
the “original” version of the data and provide it to other members of the team
or outside scholars.

### Reproducibility

In the same vein as accountability, reproducibility limits the possibilities
for error to creep into the data, thereby keeping the RRR team accountable.
This is why, if possible, automation is preferred for all tasks. The data
should be acquired automatically. Then it should be refined automatically.
Then parsed and filtered and remapped automatically. 

Here, the relationship between data immutability and functional programming
becomes clearest. [Functional
programming](https://medium.freecodecamp.org/write-safer-and-cleaner-code-by-leveraging-the-power-of-immutability-7862df04b7b6)
relies on the ideas of removing side effects and having reproducible actions
that, given the same inputs will always return the same outputs. The result is
code that more clearly reveals its implementation to third parties. 

That is, if work is automated and only done on ephemeral copies of the
original data, the various sorts, filters, calculations, and capitalizations
we associate with “cleaning” or “refining” data become clearer, more
predictable, undoable, and, of course, fixable. If at first we limit our
dataset of rabbits to those that live in fields and later decide we also want
to track rabbits who live in hills, we simply have to adjust the
implementation at the filter stage.

### Multiplicity

Having an immutable datastore where analysis is done on ephemeral copies of
the data using filters and other functions also lends itself to constructing
multiple pictures of the same dataset. For example, perhaps one RRR data
narrative focuses on the ages of rabbits, while another focuses on the colors
of their fur. When the decision is made to include hill rabbits in addition to
field rabbits, both data narratives instantly incorporate the new rabbits
added to the analysis. However, to ensure the most utility from multiplicity
requires returning to the second key concept in RRR data management,
centrality.

## Centrality

While gathering data and researching, collected and captured fragments of
information are typically heterogeneous and don’t really speak to each other.
You could be looking at two groups of entities that are semantically related
(rabbits and warrens) but that, nevertheless, have widely divergent lists of
properties.

The ultimate goal of centrality is a **single source of truth (SST)**, and
towards that end, it’s useful to always have consolidation in mind when
gathering data. Under ideal circumstances, a single, atomic unit emerges that
provides the data context of the RRR project. This unit might not be the
central point of interest of the project or of certain narratives, but it
still ends up being what ties the data together.

For example, perhaps you are tracking environmental change on hills and
fields. But your data is on specific rabbits. Rabbits are the atomic unit, but
it will become later to abstract out data (average age, fur color) about the
rabbits from the frame of reference of hills and fields.

The SST should be a table of these atomic units as rows and properties as
columns. We recommend sticking, for now, to one model only. That is, one type
of entity and its myriad properties. This challenges the object-oriented or
relational-database paradigms many of us are familiar with, but for the
purposes of consistency, flattening the data like this encourages, we believe,
thinking about the data in immutable terms.

Centrality and immutability reinforce each other, because generating ephemeral
copies of the SST encourages that the SST remains accountable, reproducible,
and fertile enough for generating even more subdatasets. Hence, these mutually
informing concepts should help guide people engaging in RRR so that they can
remain maximally transparent, minimally error-prone, and, most important, free
to confidently take their data and use it to tell the stories it can.
