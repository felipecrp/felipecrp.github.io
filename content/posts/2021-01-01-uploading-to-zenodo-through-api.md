---
layout: post
title:  "Uploading to Zenodo through API"
date: 2021-01-01
author: Felipe Curty
tags:
- open science
---

Zenodo is a free repository to share scientific data. It enables researchers to upload an almost unlimited amount of data and suits pretty well to share research datasets. In this article, I explain how to use the Zenodo API to share a dataset. 

We need to create a deposit to upload data to Zenodo. The deposit is the publication itself. It contains title, date, authors, DOI, description, and much other optional metadata. Once created, we can upload files to the deposit.

We are going to use curl to access the Zenodo API. It is available at <https://zenodo.org/api/> and requires authentication through an access token. The access token is generated in [Zenodo Settings > Applications > Personal access tokens](https://zenodo.org/account/settings/applications/tokens/new/). We need the "deposit:write" scope to create deposits and upload files. After defining a name and selecting the scope, the site will generate a key, i.e., a random string that we will use to authenticate with the API. It is essential to keep the key private because it would enable other users to upload files on your behalf.

First, we will call the root API URL to test. It is public and don't need authentication.

```bash
curl --request GET 'https://zenodo.org/api/'
```
```json
{
    "links": {
        "communities": "https://zenodo.org/api/communities/",
        "deposits": "https://zenodo.org/api/deposit/depositions",
        "files": "https://zenodo.org/api/files",
        "funders": "https://zenodo.org/api/funders/",
        "grants": "https://zenodo.org/api/grants/",
        "licenses": "https://zenodo.org/api/licenses/",
        "records": "https://zenodo.org/api/records/"
    }
}
```

The API response list the other API URLs. We will send a POST request to <https://zenodo.org/api/deposit/depositions> with an empty JSON to create a new deposit. Since we started using the private API, we need to provide the previously generated key in each request.

```bash
curl --request POST 'https://zenodo.org/api/deposit/depositions?access_token=<KEY>' \
     --header 'Content-Type: application/json'  \
     --data-raw '{}'
```
```json
{
    "conceptrecid": "4409229",
    "created": "2021-01-01T17:16:33.583624+00:00",
    "files": [],
    "id": 4409230,
    "links": {
        "bucket": "https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5",
        "discard": "https://zenodo.org/api/deposit/depositions/4409230/actions/discard",
        "edit": "https://zenodo.org/api/deposit/depositions/4409230/actions/edit",
        "files": "https://zenodo.org/api/deposit/depositions/4409230/files",
        "html": "https://zenodo.org/deposit/4409230",
        "latest_draft": "https://zenodo.org/api/deposit/depositions/4409230",
        "latest_draft_html": "https://zenodo.org/deposit/4409230",
        "publish": "https://zenodo.org/api/deposit/depositions/4409230/actions/publish",
        "self": "https://zenodo.org/api/deposit/depositions/4409230"
    },
    "metadata": {
        "prereserve_doi": {
            "doi": "10.5281/zenodo.4409230",
            "recid": 4409230
        }
    },
    "modified": "2021-01-01T17:16:33.583637+00:00",
    "owner": 183492,
    "record_id": 4409230,
    "state": "unsubmitted",
    "submitted": false,
    "title": ""
}
```

The response comprises a JSON with the deposit id, more API links, and additional metadata. We are interested in the bucket link, which we will use to upload files to the deposit. We will send a PUT request to the bucket link, appending the filename to the URL and its content in the body of the request. In the following example, we will upload our `readme.md` file.

```bash
curl --upload-file readme.md --request PUT 'https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5/readme.md?access_token=<KEY>'
```
```json
{
    "mimetype": "application/octet-stream",
    "updated": "2021-01-01T17:45:08.089242+00:00",
    "links": {
        "self": "https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5/readme.md",
        "version": "https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5/readme.md?versionId=b504c605-f417-436e-afd8-b3111f8d6258",
        "uploads": "https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5/readme.md?uploads"
    },
    "is_head": true,
    "created": "2021-01-01T17:45:08.081857+00:00",
    "checksum": "md5:97268f1eedc1877573f0a01f3ded263f",
    "version_id": "b504c605-f417-436e-afd8-b3111f8d6258",
    "delete_marker": false,
    "key": "readme.md",
    "size": 24
}
```

If we check the Zenodo website, we can find the readme under our deposit files.

![zenodo]

[zenodo]: /assets/figs/2021-01-01-zenodo.png
{:style="display: block; margin-left: auto; margin-right: auto;"}

## Uploading large files

Generally, we need to upload a large tarball file to Zenodo containing our dataset. Since the upload can take a while to conclude, it may help use a progress bar to mark the upload progress. The curl command provides this option.

```bash
curl --progress-bar \
     --upload-file dataset.tgz \
     --request PUT 'https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5/dataset.tfz?access_token=<KEY>' |
     cat
```

Since curl hides its output by default, it is important to include the pipe to the `cat` command to visualize the progress bar.

## Using already created deposits

If we already created a deposit, we can use the API to find its bucket URL and upload files. We need to call the deposit API to list all the created deposits.

```bash
curl --request GET 'https://zenodo.org/api/deposit/depositions?access_token=<KEY>
```
```json
[{
    "conceptrecid": "4409229",
    "created": "2021-01-01T17:16:33.583624",
    "id": 4409230,
    "links": {
        "discard": "https://zenodo.org/api/deposit/depositions/4409230/actions/discard",
        "edit": "https://zenodo.org/api/deposit/depositions/4409230/actions/edit",
        "files": "https://zenodo.org/api/deposit/depositions/4409230/files",
        "html": "https://zenodo.org/deposit/4409230",
        "publish": "https://zenodo.org/api/deposit/depositions/4409230/actions/publish",
        "self": "https://zenodo.org/api/deposit/depositions/4409230"
    },
    "metadata": {
        "prereserve_doi": {
            "doi": "10.5281/zenodo.4409230",
            "recid": 4409230
        }
    },
    "modified": "2021-01-01T17:16:33.583637",
    "owner": 183492,
    "record_id": 4409230,
    "state": "unsubmitted",
    "submitted": false,
    "title": ""
}]
```

The response JSON comprises the list of available deposits. We need to find the deposit we want to upload the files. The API URL is available on the `link > self` of the response JSON.

```bash
curl --request GET 'https://zenodo.org/api/deposit/depositions/4409230?access_token=<KEY>'
```
```json
{
    "conceptrecid": "4409229",
    "created": "2021-01-01T17:16:33.583624+00:00",
    "files": [
        {
            "checksum": "97268f1eedc1877573f0a01f3ded263f",
            "filename": "readme.md",
            "filesize": 24,
            "id": "7d6784d5-2e9f-44f3-8196-45a9f62ca941",
            "links": {
                "download": "https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5/readme.md",
                "self": "https://zenodo.org/api/deposit/depositions/4409230/files/7d6784d5-2e9f-44f3-8196-45a9f62ca941"
            }
        }
    ],
    "id": 4409230,
    "links": {
        "bucket": "https://zenodo.org/api/files/50b47f75-c97d-47c6-af11-caa6e967c1d5",
        "discard": "https://zenodo.org/api/deposit/depositions/4409230/actions/discard",
        "edit": "https://zenodo.org/api/deposit/depositions/4409230/actions/edit",
        "files": "https://zenodo.org/api/deposit/depositions/4409230/files",
        "html": "https://zenodo.org/deposit/4409230",
        "latest_draft": "https://zenodo.org/api/deposit/depositions/4409230",
        "latest_draft_html": "https://zenodo.org/deposit/4409230",
        "newversion": "https://zenodo.org/api/deposit/depositions/4409230/actions/newversion",
        "publish": "https://zenodo.org/api/deposit/depositions/4409230/actions/publish",
        "registerconceptdoi": "https://zenodo.org/api/deposit/depositions/4409230/actions/registerconceptdoi",
        "self": "https://zenodo.org/api/deposit/depositions/4409230"
    },
    "metadata": {
        "prereserve_doi": {
            "doi": "10.5281/zenodo.4409230",
            "recid": 4409230
        }
    },
    "modified": "2021-01-01T17:16:33.583637+00:00",
    "owner": 183492,
    "record_id": 4409230,
    "state": "unsubmitted",
    "submitted": false,
    "title": ""
}
```

The deposit upload URL is available on the `links > bucket` in the response JSON.
