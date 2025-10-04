{% version "3.x" %}
# 3.7.2
Release date: February 10, 2020
## Summary
A small release that adds additional aliases and default values to some options.
Highlights from this release
1.  If no domain argument is provided, all domains in the instance will be exported.
2.  If no start or end date are provided, a default of yesterday and today will be used respectively.
## New Feature
[AM3-12478](https://dtools.ipsoft.com/browse/AM3-12478) - If no domain argument is given, default to all domains
# 3.7.1
Release date: August 29, 2019
## Summary
This release only includes one bug fix that will ensure Eddie replay tests can be generated from exported conversations.
## Bugs Fixed
AM3-10810 - This change fixes an issue that did not account for domain switching in conversations and thus could not create an Eddie replay with the proper domain information. This has now been corrected and the Eddie tests should be created with the proper domain codes.
# Download
https://dtools.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/ameliav3x-metrics-export/3.7.1/ameliav3x-metrics-export-3.7.1-all.jar
{% /version %}
