# Sharing Data

## Goals

- Identifiers :: Establish a set of identifiers that can be used to link meta-data to pdf documents across different corpora

- Data Format :: Establish meta-data exchange formats

- Data Sets :: Curate lists of publicly available data-sets that conform to these ID-schemes and formats

## Identifiers

- Use _hashing_ to create universal identifiers for pdf documents

- Hashes can be generated from the pdf document itself

- No central authority is needed to give out IDs

- Common hashing methods include: md5, sha1, sha256

- md5 and sh1 are not/no longer cryptographically secure. This means, it's possible that an attacker
  produces two different pdfs that have the same hash key.

- Multiple different versions of the "same" document might be circulating in the wild

- MacOS/Preview re-writes the pdf on save, and changes it's binary representation. This is a
  particularly subtle way to generate duplicates.
  
- Finger Printing. Create a hash algorithm that is tolerant to invisible changes. Utopia Docs has a
  finger printing mechanism.

- Ids can be generated for use inside the service (e.g. auto-increment fields in the DB) but they
  shall not be used to link data.

- Problem :: Books have no sha1 key
  - We only consider digital documents?? So it get's an ID only if we have a full scan

## Data Formats

- BibJSON http://okfnlabs.org/bibjson/

## Data Sets

- [Public Datasets as YAML](datasets.yaml)

### Usage

* `make validate` validate the dataset.yaml file

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

- Share intermediate results. We don't need to run CERMINE on all arXiv pdf over and over. Do it
  once and share it with the world.

- Make it easy for researches in ML/DataMining to run their models on data-sets and share the
  outcomes with the community.

## Successful examples of data sharing

- Git & GitHub are great examples for a successful data sharing infrastructure
  - Use sha1-hashes (Merkle trees) for addressing files, trees and commits. Mutable meta-data
    (branches, tags) pointt to nodes of the tree.
  - De-centralization. Git is de-central by design. There is no central git server. All git checkouts are equal.
  - Separate Hosting Service and Data Sharing. GitHub is the dominant platform for hosting and
    viewing git repositories, but it's by no means the only one. Everyone can install open source
    UIs like GitLab, or use alternative providers like BitBucket.
  - Plan for change. Codebases are under constant change by a variety of people. The very purpose of
    git is to manage changes in the code-base in a repository.
  - Q :: Can we not just use git to manage&share data?
    - For small gold standard data-sets: Yes!
    - For csv tables with a few 100K rows: Yes!
    - For millions of pdfs: No.
    - What are the precise scaling limits of git?
    - ... of GitHub

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

## In the ideal world

* ... I should be able to clone data sets from public libraries like GESIS or arXiv with a single command (`git clone ...`)

* ... I should be able to update a cloned data-set with a single command `git pull`

* ... I should be able to revert a data set to any point the past and compare the versions `git checkout/git diff`

* ... ML/DataMining Researchers should run their methods on large corpora and publish their results

* ... Researches should not be responsible for hosting the datasets (Use managed services e.g. GitHub, NPM, )

* ... User facing services (related-work.net) should be able to pull in meta-data from different data-providers

* ... Researches should be able to see the results of their methods quickly

## Further Remarks

- Application vs. Service.
  - UtopiaDocuments is an Applications that is run by the user.  Applications can consume APIs on an
    per-paper basis.  The user is only ever going to view a hand full of pdfs in the same minute,
    it's feasible to make multiple individual API requests for each pdf in questions.
  - RelatedWork.net is a Service that is run by an institution. Part of it is a very limited HTML/JS
    application that runs on the machine of the user, and communicates with the RW HTTP API.
    Services maintain information about millions of documents. It's not feasible to make individual
    API requests to resolve additional data about each document. Services share data in bulk.
