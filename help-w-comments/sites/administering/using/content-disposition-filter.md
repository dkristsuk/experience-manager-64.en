---
title: Content Disposition Filter
seo-title: Content Disposition Filter
description: null
seo-description: null
uuid: 8f4b48ea-7141-442e-9429-d424ece1e728
contentOwner: trushton
discoiquuid: 1826fd68-e456-47cb-bc40-7d3eb4f373af
index: y
internal: n
snippet: y
---

# Content Disposition Filter{#content-disposition-filter}

Content disposition filter is a security feature against XSS attacks on SVG files.

Once installed, the filter blocks access to all assets. For example, you could not view a pfd online. This section describes how to configure the filter to your needs.

## Configure Content Disposition Filter {#configure-content-disposition-filter}

You can view the [Apache Sling Content Disposition Filter in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

The Content Disposition Filter options provide the following functionality:

* Content Disposition Paths: a list of paths where the filter will be applied followed by a list of mime-types to exclude on that path.This path must be an absolute path and may contain a wildcard ('&#42;') at the end, to match every resource path with the given path prefix. For example: /content/&#42;:image/jpeg,image/svg+xml " will apply the filter to every node in /content except jpg and svg images

* Excluded Resource Paths: a list fo excluded resources, each resource path must be given as absolute and fully qualified path. Prefix matching/wildcards are not supported.

* Enable For All Resource Paths: this flag controls whether to enable this filter for all paths, except for the excluded paths defined by Excluded Resource Paths. Setting this to 'true' leads to ignoring Content Disposition Paths. Independent of the configuration only resource paths are covered which contain a property named 'jcr:data' or 'jcr:content jcr:data'.
