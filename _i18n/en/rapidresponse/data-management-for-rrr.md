# Nimble Data Management

Considering that time is the limiting reagent in any Rapid-Response Research
(RRR) reactions, having a data management plan ahead of time and sticking to
it should lessen confusion and inconsistency when teams are rapidly slicing
and dicing the data for their own specific needs. What follows is, first, a
conceptual way of thinking of the data, and, then, practical tips for
achieving the goals of consistency of results between the various parts of
your RRR project.

## Concepts

While gathering data and researching, collected and captured fragments of
information are typically heterogeneous and don’t really speak to each other.
You could be looking at two groups of entities that are semantically related
(rabbits and warrens) but that, nevertheless, have widely divergent lists of
properties.

The ultimate goal here is a **single source of truth (SST)**, and towards that end,
it’s useful to always have consolidation in mind when gathering data. For
example, in Volume 2 of *Torn Apart / Separados*, for the most part we had an
SST of truth that was a list of about 5,500 financial awards ICE
gave to government contractors since 2014. That is, it became clear that the
*atomic unit* was the award, and all we were doing was collecting properties
pertaining to each award.

The SST should be a table of these atomic units as rows
and properties as columns. During the research and collection phase of RRR,
this can be spreadsheet in the cloud or even a database, if your team is able
to create an interface for one quickly. But we recommend sticking, for now, to
one model only. That is, one type of entity and its myriad properties. This
challenges the object-oriented or relational-database paradigms many of us are
familiar with, but for the purposes of consistency, flattening the data like
this encourages, we believe, safety.

Finally, the goal is to get the SST **frozen** as quickly
as possible. This means, concretely, that property names are fixed as soon as
possible. As the list of properties grows (in _Torn Apart / Separados_ every
award had over 250 properties), it becomes useful to have a data
dictionary or cheatsheet that describes the properties.

The data dictionary should sit in a separate file from the SST, not in a
separate tab on the same spreadsheet. This encourages two practices. First, it
allows the RRR team to refer to the dictionary while working on the SST.
Second, it reminds researchers that they are pursuing two different ends with
each file. The SST is going to be a **machine-readable data source**. The
dictionary, on the other hand, is going to merely be an aid to researchers.

With property names (and types) frozen, it becomes possible to start thinking
of the SST as something a script can manipulate to filter the data and reshape
to help the RRR describe one (of many) aspects of the collected data. Each
narrative, or visualization, or whatever particular investigation into the
data should work off a **dynamically generated subdataset**. The aim is to remove
rows and columns that are not needed for the investigation. Yet it would also
not be difficult to add deleted properties from the SST if needed.

The dynamically generated subdataset can include properties that are not in the
SST, such as computed properties (average values of certain rows, for example,
or “pretty” versions of text strings that remove capitalization), but these
calculations should be done to the subdataset as it is generating its own data
file. The script that generates the subdataset is also where the data is
finessed into fitting the expectations the investigation has down the line.

By dynamically generating these subdatasets, it ensures that changes to the SST
are propagated throughout all the RRR investigations. Similarly, if a
researcher notices an error in the subdataset, they can return to the SST and
correct it, thereby propagating the correction as well. 

This touches on the final concept of RRR data management: **immutability**.
The SST should be, for all intents and purposes, immutable. Changes such as
decapitalization, calculations, conversions to other units, and so on, should
be done by the scripts building the subdatasets, such that, if necessarily,
the SST can be rebuilt from the original sources, should that need arise.
Another way, better to add a column at the end, `use_this_row` with a `true`
or `false` value than to delete rows from the SST. As such, work is done on
*copies* of the SST, while leaving the SST untouched.

## Practice

### Single Source of Truth (SST)

Above, we encourage creating one, single table with all of your data in it,
its possible to draw one model (awards) out of it. Sometimes (rabbits and
warrens), that will not be, in which case each specific model table can be its
own SST.

#### Unique IDs

Establish a column (or build one) that stands as the unique, unchanging ID
associated with that instance of the model. It can be an ascending number or
something more complex, but there should be one attached.

#### Get to CSV/JSON ASAP

Though there are conceptual reasons for building on one giant table, there are
practical reasons as well. Namely, getting the file to a `.csv` or `.json`
format as soon as possible exposes it to being used to generate subdatasets.
Furthermore, as plain text data formats, CSV and JSON fit into the portability
and maintainability demands of minimal computing.

#### But keep it away from Excel

Excel is far too opinionated about the data users throw at it. For
applications that don’t rely on, say, Unicode or machine parsing down the
line, that is probably sufficient. But for RRR, it introduces unpredictable
results. We therefore recommend collecting as a team on a cloud spreadsheet
and downloading to CSV as soon as the data starts taking shape.

#### Once it’s in CSV/JSON, put it under version control

Cloud spreadsheets have a reasonable, user-friendly version history. And git
provides, well, a version history. This allows the team to retrace their steps
if/when data gets corrupted or lost.

#### Fix column (property) names as soon as possible

One problem we have run into is the tendency towards waiting for the data to
be finalized before beginning to build subdatasets from them. This is a
conceptual mismatch, because the point of the SST and dynamically generated
subdatasets is that the form precedes the content. Coders writing
visualizations can fill the data in the subdatasets with dummy data. But to
make that easier, the data needs to be in a predictable format. As such, it’s
useful if the coders can expect a property called `rabbit_name` instead of
just `name`. 

Additionally, because the pace of the RRR limits the opportunities to use
certain programming paradigms like test-driven development, changing headers
(or keys) can have unintended side effects down the line. Fixing headers is
part of embracing immutability, which limits side effects.

### Atomic Units

#### Design a good model and stick to it

Sometimes, the atomic unit is obvious from the RRR data source. We are looking
at a list of rabbits, so, hence, our output will be a list of rabbits.
Ultimately, we may be interested not in the rabbits themselves, but in their
human overseers, who are named in the `overseer` property. The temptation to
imagine that the “actual” atomic unit is the overseer must be avoided. It is
far easier to build a subdataset that redefines the SST in terms of a
different property than to try to coerce that pivot during the course of data
collection.

#### But change if you need to

Anyone who has tried to use data to plan a fantasy baseball auction has come
across the problem of atomic units. Is the atomic unit the player or are there
two, hitters and pitchers? Some fantasy advice websites provide separate
datafiles for pitchers and hitters. Yet only frustration lies in trying to
maintain that distinction of two separate models in planning one’s auction. So
even though hitters and pitchers have mostly different properties (related to
their statistics hitting and pitching, respectively), it makes sense to create
a single atomic unit, a player, and simply have blank properties. 

### Data Dictionary

#### Make it clear

Ideally, the data dictionary should have granular information about the
property, such as:

* Header name (such as `total_awards_2018`, written in
[camelCase](https://en.wikipedia.org/wiki/Camel_case) or
[snake_case](https://en.wikipedia.org/wiki/Snake_case))
* Corresponding column name (“A,” “BZ,” “JW,” etc.)
* Type (string, url, date, number)
* Range (if applicable)
* Possible/expected values (if the property has a controlled vocabulary)

It is also useful to include a textual description of each property that could
include where the data was collected, by whom, when, and what the property
means.

#### But remember your audience

During the course of RRR, the data dictionary is most useful as a means by
which people collecting data and people filtering the data know that they’re
making the same assumptions about what is in the SST. As such, just the column
name and header name might be sufficient. 

Afterwards, however, especially if the data will be made public to outside
researchers (which we encourage), a more extensive data dictionary would be
more useful.

### Dynamically generated subdatasets

Building generators that create subdatasets from the SST are vital to good
data management in general but precisely in RRR situations. No matter what
language you are using for programming, there is probably an I/O module for
reading files and a CSV parser. From there, you can use your language’s
various [higher-order
functions](https://en.wikipedia.org/wiki/Higher-order_function) to generate a
new subdataset. Here are the three most common.

#### `array.filter(func)` (Ruby: `array.select &block`, Python:
`filter(func, list)`)

Your progamming language’s
[`#filter`](https://en.wikipedia.org/wiki/Filter_(higher-order_function))
function works by iterating over your SST and determining whether the row in
question passes your given predicate. In other words, `#filter` is a great way
to ignore rows in your dataset by sending it predicates like `row.name.length
> 0`, which will limit the subdataset to rows in the SST with values in the
`name` column that are not blank.

#### `array.map(func)` (Ruby: `array.map &block`, Python: `map(func,
list)`)

If `#filter` generates a subdataset that is “shorter” than the SST (fewer
rows), [`#map`](https://en.wikipedia.org/wiki/Map_(higher-order_function))
lets you change the width (number of columns) of your subdataset. It allows
you to ignore columns, calculate new ones, convert columns, and even rename
them. The function iterates over the SST and applies the same transformation
to each row, generating a new representation of that row and combining
everything into a list at the other end.

#### `array.reduce(func, initVal)` (Ruby: `array.reduce initVal,
&block`, Python: `functools.reduce(func, list, initVal)`)

Finally,
[`#reduce`](https://en.wikipedia.org/wiki/Fold_(higher-order_function)) folds
your dataset and removes one dimension from it. It can calculate sums of
columns, generate lists of unique values for columns, or produce other
metadata about the SST (or your subdataset).

These three higher-order functions provide the flexibility to immutably yet
dynamically generate subdatasets, leaving the SST intact.

### New entities

If the rabbits SST mentioned above, I noted that one column, `overseer` listed
the name of the human who was the given rabbit’s overseer. It is likely that
your RRR is more interested in the overseers than in the rabbits. Using a
combination of the higher-order functions above, it becomes possible to recast
the SST in terms of the overseers. For example, it is possible to use
`#reduce` to get the list of unique overseers. Then, using that list, you can
`#filter` the SST to get the list of rabbits the specific overseer oversees.
Then, you can use `#reduce` to collect general information about the rabbits,
like their average age or what unique warrens they live in. 

Finally, you can `#map` this newly generated data into a new list where the
atomic unit is no longer a rabbit, but, rather, the overseer. And when a new
batch of data about rabbits comes in, it becomes easy to update the subdataset
of overseers, because it is a question of simply re-generating the subdataset.

### Separate subdatasets

The SST is likely to be an immense file, weighing several megabytes. It’s bad
netiquette and counter-minimal computing to dump that kind of file on an
unsuspecting web user. The hope is that, through generating separate
subdatasets, where each pertains to a specific investigation, you end up with
a collection of smaller files that load more quickly.

### Lookup tables

Perhaps the `overseer` value in the SST is not the overseer’s name, but,
rather, their ID number with the local rabbit overseer’s guild. Having a
lookup table, a file separate from the SST, that gives the overseer’s name and
local guild ID number, can help you build subdatasets with information that is
easier for your users to understand. That information can, of course, be also
encoded into the SST (`overseer_guild_id`, `overseer_name`, etc.), and often is. But
the lookup table is also useful for customizations, especially when
“prettifying” names so that they are appropriately capitalized or uniformly
presented.

### Calculate close to the data

It’s very tempting to put off calculations or transformations of the data to
the end of the data flow. After all, `#map()` and all the other higher-order
functions can be executed in the browser in JavaScript. We believe that, for
RRR and minimal computing purposes, it is better to perform those
transformations and generations on the server-side, generating a file (CSV or
JSON) that can be quickly read by the browser and presented without a lot of
manipulation. After all, the browser is probably already busy trying to draw
visualizations or engaging in other tasks. Nevertheless, where to calculate is
a balancing act.

### Conclusion

It is our hope that this document provides both a good starting point for RRR
data management as well as a useful description of why data management is
important in general, but especially in RRR projects, where things can spin
out of control quickly. 

The underlying principles are, again, to consolidate data into a single-source
of truth that then becomes immutable. Investigations should dynamically
generate their own versions of the SST and work with those, instead of with
the SST itself. But when the SST is updated, the subdatasets must be
regenerated. 

## Appendix A: Node scripts for generating dynamic subdatasets

Writing a Node script that builds a `.csv` from a SST is rather
straightforward. In what follows

Here is a
sample script:

```javascript
const fs = require("fs");
const csv = require("csv");
const process = require("process");

// Read and parse the SST csv.
fs.readFile(process.argv[2], (err, file) => {
  if (err) throw err;
  csv.parse(file, { columns: true }, (err, SingleSourceOfTruth) => {
    if (err) throw err;

    // Build a dataset out of the SST.
    const dataset = SingleSourceOfTruth.filter(row => {
      return row.use_this_row;
    });

    // Now convert back to csv and write a new file.
    csv.stringify(dataset,
      {
        // create a header row
        header: true,
        // the list of column names for the header row. These must
        // match dataset property names.
        // You could also have:
        // columns: Object.keys(dataset[0])
        columns: ["array", "of", "column", "names"]
      },
      (err, output) => {
        if (err) throw err;
        fs.writeFile(process.argv[3], output, (err) => {
          if (err) throw err;
          process.stdout.write(`File ${process.argv[3]} successfully written.\n`);
        });
      });
  });
});
```
