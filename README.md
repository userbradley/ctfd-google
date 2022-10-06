# CTFD on Google Cloud

This is a weekend project to get [cftd.io](https://ctfd.io) working and deployed in to Google cloud.

## Options for installing

* GKE
* Cloud run

Both options rely on an SQL database, however GKE will rely on a redis Database too

## Why?

I want to use it at work, and the helm charts for this currently seem out of date, so it makes sens to create my own one,
that is specific to GKE (As that's my cloud of choice)