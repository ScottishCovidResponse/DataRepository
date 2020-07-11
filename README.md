# DataRepository

This is a git repository to store

## Data Product format

The expected format of the components of data product in the pipeline is described in [this file][format-url] on SCRC Teams. Briefly, for toml files, there are currently three types of information that can be stored in one:

1. A simple point estimate of a parameter
```
[latency-period]
type = "point-estimate"
value = 123.12
```

2. The distribution of a parameter 
```
[latency-period]
type = "distribution" 
distribution = "gamma" 
shape = 1
scale = 2 
```
 
 3. Samples drawn from the distribution of a parameters (possibly posterior samples from a Bayesian model)
```
[latency-period] 
type = "samples" 
samples = [1.0, 2.0, 3.0, 4.0, 5.0]
```

In the examples above, each file had a single component called `latency-period` in the data product. If there's only one component in a data product, then we suggest giving it the same name as the last part of the data product's name in the namespace, so for `human/infection/SARS-CoV-2/latency-period`, this would be `latency-period`. This will be the default if no component name is given in a funtion call. You can have multiple components in a single data product. Component names in toml should use bare keys - these may only contain ASCII letters, ASCII digits, underscores, and dashes (A-Za-z0-9_-).

For example:

```
[latency-period]
type = "point-estimate"
value = 123.12

[asymptomatic-period] 
type = "point-estimate" 
value = 200.1
```

The only further constraint is that all of the component names (here `latency-period` and `asymptomatic-period`) are different.

## Data Product location and file naming convention

Data Products stored in this repository should be stored in folders according to their namespace, data product name and version number. So the `human/infection/SARS-CoV-2/latency-period` Data Product version `v0.0.1` in the `SCRC` namespace should be found in `SCRC/human/infection/SARS-CoV-2/latency-period` and called [`v0.0.1.toml`](SCRC/human/infection/SARS-CoV-2/latency-period/v0.0.1.toml). Using this convention will make it easy to browse the repository.

[format-url]: https://teams.microsoft.com/l/file/03AF05F8-DF00-417B-BA73-B152606C0CCA?tenantId=6e725c29-763a-4f50-81f2-2e254f0133c8&fileType=docx&objectUrl=https%3A%2F%2Fgla.sharepoint.com%2Fsites%2FScottishCOVID-19ResearchConsortium%2FShared%20Documents%2FGeneral%2FCollaboration%2Fdata%20pipeline%20API%2F3.%20Standardised%20data%20type%20API.docx&baseUrl=https%3A%2F%2Fgla.sharepoint.com%2Fsites%2FScottishCOVID-19ResearchConsortium&serviceName=teams&threadId=19:283c5ea4551344249cc76dd0ecaa4f74@thread.tacv2&groupId=669b45e2-a9a6-4060-ba8a-9ebd3713e367
