# Sharing Data

## Motivation

- Make meta-data about scientific articles publicly available
- pdf documents are the dominant data format for scientific articles
- pdf documents (found in the wild) do not semantic meta-data about authors, sections, references,
  etc. but only layout and textual information.
- automated extraction of semantic meta-data from pdf document is a highly challenging task that
  involves multiple steps
- We can not solve this alone. The EXCITE project (as well as many others) are aiming to improve the
  full citation extraction and publication pipeline. We can't solve all of that well. We have to
  re-use the work of others.

## Goals

- Establish a set of identifiers that can be used to link meta-data to pdf documents

- Establish meta-data exchange formats

- Curate lists of publicly available data-sets that conform to these ID-schemes and formats

## Successful examples of data sharing

- Git & GitHub are great examples for a successful data sharing infrastructure
  - Hash (sha1) based file and linking and addressing. There are no git ID's, only SHA-1 hashes to
    refer to files, commits, etc. Mutable meta-data points to nodes of Merkle trees.
  - De-centralization. Git is de-central by design. There is no central git server. All git checkouts are equal.
  - Separate Hosting Service and Data Sharing. GitHub is the dominant platform for hosting and
    viewing git repositories. But it's by no means the only one. Everyone can install open source
    UIs like GitLab, or use alternative providers like BitBucket.
  - Plan for change. Codebases are under constant change by a variety of people. The very purpose of
    git is to manage changes in the code-base in a repository.

- Hosting Data Sets
  - Central Services
    - FigShare
    - GitHub
    - Arxiv.org
  - De-centralized Approaches
    - [IPFS](https://ipfs.io) -- A peer-to-peer hypermedia protocol to make the web faster, safer, and more open.
    - [BitTorrent](http://www.bittorrent.com) -- Download large files with the easy-to-use BitTorrent client

- Global Indices / Browsers / Aggregators
  - Google
  - Goolge Scholar

## Content

- [Public Datasets](datasets.yaml)

## Usage

* `make validate` validate the dataset.yaml file
