> ![warning](../../images/warning.png) This document describes an alpha release of calicoctl
>
> See note at top of [calicoctl guide](../../README.md) main page.

# Calico resources
This guide describes the set of valid resource types that can be managed
through `calicoctl`.

## Overview of resource YAML file structure
The calicoctl commands for resource management (create, delete, replace, get)
all take YAML files as input.  The YAML file may contain a single resource type
(e.g. a tier resource), or a list of multiple resource types (e.g. a tier and two
policy resources).

### A single resource
The general structure of a single resource is as follows:

```
apiVersion: v1
kind: <type of resource>
metadata:
  name: <name of resource>
  ... other identifiers required to uniquely identify the resource
  ... labels (when appropriate for the resource type)
spec:
  ... configuration for the resource
```



### Definitions
| name     | description                                               | requirements                                                                     | schema |
|----------|-----------------------------------------------------------|----------------------------------------------------------------------------------|--------|
| apiVersion     | Indicates the version of the API that the data corresponds to.                           | Currently only `v1` is accepted. | string |
| kind    | Specifies the type of resource described by the YAML document. | Can be [`bgppeer`](bgppeer.md), [`hostendpoint`](hostendpoint.md), [`policy`](policy.md), [`pool`](pool.md), [`profile`](profile.md), [`tier`](tier.md), or [`workloadendpoint`](workloadendpoint.md) | string |
| metadata | Contains sub-fields which are used identify the particular instance of the resource. | | YAML |
| spec | contains the resource specification, i.e. the configuration for the resource. | | YAML |

### Multiple resources in a single file
A file may contain multiple resource documents specified in a YAML list format. For example, the following is the contents of a file containing two `tier` resources:
```
- apiVersion: v1
  kind: tier
  metadata:
    name: tier1
  spec:
    order: 10
- apiVersion: v1
  kind: tier
  metadata:
    name: tier2
  spec:
    order: 20
```

[![Analytics](https://calico-ga-beacon.appspot.com/UA-52125893-3/libcalico-go/docs/calicoctl/resources/README.md?pixel)](https://github.com/igrigorik/ga-beacon)
