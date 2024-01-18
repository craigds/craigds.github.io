# Koordinates - 2018 - Platform Merging project (“ID Migration”)

## Background

In 2018, Koordinates merged web apps running on three separate customer sites into one multi-tenanted platform. A notable and fiddly subproject was merging the identifier namespaces into one, dubbed “the ID migration.” I spearheaded the R&D effort for this project.

## Strategy

### 1. Catalogue identifiers

Firstly it involved cataloguing the current values and growth rates of all the identifiers in Koordinates’ several large databases, as well as all places those identifiers were used in disk and cloud storage, and all places the identifiers were exposed in URLs.

### 2. Assign ranges
The next phase was to assign all overlapping identifiers a new range in the merged site.

For example, User `123` on a particular site would become User `500123` on the new merged site. Each type of table/resource had its own range assigned, so that even with an expected 6 months worth of growth between range assignment and project completion, the assigned ranges for each resource on each site would not overlap.

### 3. Redirect old URLs
3. After all the ranges were assigned, I built a backward-compatibility layer for all resources that had been exposed to customers or the public. Old URLs redirected to different new URLs based on which customer domain being accessed. We managed to do this efficiently and transparently without any database access.

### 4. Merge sites

The final step was to actually merge the databases and storage. Scripting this merge of multiple large databases and many terabytes of storage was an intricate procedure and needed to be well tested.

I built a new staging environment specifically for testing the process, and we ran it repeatedly to ensure we weren’t going to break customer data or have an embarrassing long-lived outage.

## Outcomes

In the end we scheduled several hours of downtime across all the sites, during which we migrated all the customer data to the new instance without any issues. The old URLs still redirect to this day, and it has been a smooth experience for customers.
