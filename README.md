# Characterizing the System Evolution That is Proposed After a Software Incident

This replication package consists of two guides and three sets of data.

## Guides

`void-data-selection-guide.md` provides an overview of how incidents from the VOID data base were selected and filtered with automated and manual techniques. It also provides a list of which incident reports were manually excluded and why.

`extracting-and-coding-guide.md` provides an explanation of how we consistently labeled codes across the extracted data and answers to common questions we had while doing our extraction and coding.

## Data

`data/*.yaml` Each incident report has a corresponding YAML file which includes the data we extracted from the incident report. The incident report itself is not included as part of this data set (we do not own this information), and so a URL is provided at the top of each YAML file to access the data. Each YAML file contains the three properties we extracted from the incident report (and context) and our applied categorizations and codes.

`data/void_incidents.csv` A complete list of incidents within the VOID data set at the point of extraction, without any filtering performed.

`data/void_incidents_fitting_inclusion_criteria.csv` A list of incident reports which satisfy the automated filtering criteria. Saturation was reached at incident 75, and so we did not proceed further with analyzing incidents further than this.
