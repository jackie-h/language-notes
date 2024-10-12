# Calculation environment

## Desirable properties

The calculation should be very easy to read. 
- Model driven
- Keep the separation of concerns, no runtime information in the calc, no infra tweaks
- Should be able to run on live or historical with same code
- Types not data frames
- Specifications that can execute lazily
- No for loops, use functional programming - map, project
- interfaces for require attributes

Inputs
- Consistent snapshot
- Timeseries
- Composable
- Must have primary keys and time on the input 
- Batch inputs, 
- Should be structured by rate of change, i.e. separate static data that doesn't change much from dynamic
- will inflate from historical (S3?) or live
- Multi-dated bitemporal for things that are valid for many days?
- DAG
- Trusted append only data source with milestoning

Why a graph?
Need to know that you are always using the same value & same equation, so if the scenario is interest rate goes up, need to make sure you invalidate that everywhere

## Calc types
Unitary - takes a single input key and produces an output
takes multiple input keys, different time series
Aggregates - take in many inputs and produce a higher level summarizing output
"unit of work" - can calc be row based, i.e. per trade or does it need to work on an aggregate
Expensive monte carlo type calcs


## Stresses or adjustments - apply delta's across the calc
"Diddlescope concept"

User hypotheticals - what-if this changed

Adjustments
- can be fed in at lower levels ?

## SDLC ? 
mono-repo vs versioned ?
pluggable versioned calcs - incremental


## Display layer
- Keep strings out of calc layer, use for display later
- Keep human readable conversions out of calc layer - i.e. boolean are 0/1


## Calculation Implementation Options

1 - Object oriented 
- Graph with the ability to batch lazy fetch nodes. Similar to UFO but more advanced

2 - signals - functions with defined inputs

Specify a calc and derive a plan from it

What keys/object-oriented gives us, is the ability to consistently understand the primary key of a "thing"


## Maintainability

- Inputs should be derived from the calc, so that the function is not loading more data than it needs

- 

## Debug-ability
 - Inspect graphs
 - Easy restarts
 - Lineage
 - Inspect intermediate results


## Versioned - everywhere


## Cost/Operational Constraint solving

- memory + cpu time
- latency

- load only what is needed in memory
- use very efficient data structures
- reuse appropriately
- memory sharing across processes - 


## What is reasonable on a single machine ?

10 million rows, 20 columns
double - 8 bytes
int - 2 or 4 bytes
char - 1 byte

Assume worst case every field is 8 bytes
10,000,000 * 20 * 8 / 1024 / 1024 / 1024 = 1.5Gb

1,000,000 * 100 * 8 / 1024 / 1024 / 1024 = 0.75Gb
Other techniques - dictionary encoding etc.

On a desktop - "Excel limit"
1,048,576 rows by 16,384 columns


## Finding data/dataplane
Data as URL's

Data broker provisioning - 

Lifecycle - you specify at start-up what inputs you need, and latency/live?


## Scheduling/data dependencies

Push vs pull based calcs

Based on available compute & cost of calculation you can decide if it needs to be computed
If dependencies change
Can also check variances - did we already calculate this and it hasn't changed?

Budgeted compute per calc

Scheduler - big vs small workloads
Important snapshots - EOD  rate

Required runs - EOD x 
Schedule - QE,ME
Needs a holiday calendar

No such thing as EOD really - different global regions etc. 
Accuracy is just how long we keep adjusting/updating numbers

Regulator requirements - must provide ex. 

Pre-checks - do we have everything data wise and is it good ?


## Locality



## Error handling
If one item fails, must be able to bisect and try again.

## Advanced incremental calcs

Advanced delta calcs - what changed since the last time we calculated this ?
Only recalculate what changed

SIMD ? GPU ? - how much can be vectorized

Auto differentiation techniques


Can we turn UFO into interfaces to allow bulk vectorized ?


## OKR

Data platform - Quality & latency of available data into calc

Latency - i.e. from when an event occurred to when we can give an answer



Cost per input matrix for performance - i.e. GPU more expensive vs CPU
Driving key for calc - lowest level 
Instrument type

Failure rate of calc. 












