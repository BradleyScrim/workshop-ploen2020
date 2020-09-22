# OpenRefine Workshop Plön

## Examples for messy data

### Format
- 23.5
- "23.5 %"
- "23,5 %"
- "23.5%"
- "23.5 %"
- "http://inkscape.org"
- "inkscape.org"

### Seperator
- item1, item2, item3
- item1; item2; item3
- item1; item2, item3
- item1;item2;item3
- item1|item2|item3

### Abbreviation etc.
- Germany
- germany
- Deutschland
- D
- GER
- Allemagne
- BRD
- Bundesrepublik Deutschland

## Links
- [Workshop Resources](https://github.com/BradleyScrim/workshop-ploen2020/tree/master/openrefine)
- Documentation
  - [OpenRefine homepage](https://openrefine.org/)
  - [OpenRefine documentation](https://openrefine.org/documentation.html) (and online courses)
  - [GREL Functions overview](https://github.com/OpenRefine/OpenRefine/wiki/GREL-Functions)

## Install/Run
- required
  - Java JRE/JDK
  - OS: Linux, Windows, MaxOS
- [unpack and run locally](https://openrefine.org/download.html)
- OR run as docker container with
  - `docker run -p 3333:3333 vimagick/openrefine`
  - then open http://0.0.0.0:3333/

## Data to fiddle with

### Sabio-export-glucose-liver
- Origin http://sabio.villa-bosch.de/newSearch/index
  - XLS file `20200219sabio-export-glucose-liver.xls`
- feel free to try out openRefine with this data set
- Exercises
  1. create a new project by importing the data
  1. select subset
     - create a text-facet for `ECNumber`
     - sort Enums by count
     - get all entries with the `ECNumber`="1.1.1.47"
  1. combine facets
     - create a numeric facet for `Temperature`
     - you may need to transform the column to numbers (*Edit Cells → Common transformations*)
     - configure a min/max for `Temperature`
     - now all rows include data matching all of your facets
  1. play around
     - create a *excluding facet*
     - *invert* the selection
  1. find out about log scale
     - create a numeric facet for `parameter.startValue` → linear scale doesn't fit here
     - click *change* in the facet
     - change value to `log(value)`
     - now you have a log scale


### So much candy data, seriously
- Origin https://www.scq.ubc.ca/so-much-candy-data-seriously/
  - CSV file `candyhierarchy2017.csv`
- Exercises
  1. Start to *Cluster* the column `Q4: COUNTRY` - try to harmonise all people from USA, usa, u.s.a,…
  1. After clustering the `Q4: COUNTRY`, you can start *Reconcile* with *WikiData* to  in your data. [Documentation](https://github.com/OpenRefine/OpenRefine/wiki/Reconciliation)
    - with *reconciling* you bring meaning to your data by finding matching links. In this example for countries.
  1. Split the `Click Coordinates (x,y)` into two columns `click x` and `click y`.
     - Hint: There are several ways to do so. For example:
       - multiple step: first *Transform* the cells to get rid of the braces `value.replace("(","").replace(")","")`; then *Split into several columns* by `,`
       - generate columns by regex: *Add column based on this column* with regex like `value.match(/\((\d+),\s*(\d+)\)/)[0]` and `value.match(/\((\d+),\s*(\d+)\)/)[1]`
     - after spliting, look at the *scatterplot* for this two columns - you can also use this visualisation to select records
       - compare with [these results](https://github.com/riinuots/candihierarchy)
