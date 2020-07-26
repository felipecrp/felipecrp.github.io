---
layout: post
title:  "Getting started to GitHub GraphQL API"
comments: true
excerpt_separator: <!--more-->
---

The GitHub GraphQL API (aka GitHub API v4) is a significant improvement on its API and enables researchers to interact with GitHub more efficiently. Although similar results can be achieved with the old API, depending on the required data, researchers need to make the first query and then make subqueries to fetch corresponding data, leading to problems with the API rate limits.

The great advantage of using the new API is that GraphQL enables one to specify the returning data, sparing the need for subqueries to fetch corresponding data.

In this post, I will explain how to search for repositories and retrieve its name, description, URL, and the number of commits. Since the last information is a bit trickery, I will start with the formers.

<!--more-->

The next frame shows the query skeleton. It merely tells GitHub that it will query information (instead of creating, updating, or deleting).

```
query {
    your query here
}
```

The query has two parts: the search and the result part. The below frame shows the search. It will search for the first ten repositories with `releasy` in its content.

```
search(
    first: 10
    type: REPOSITORY,
    query: "releasy",
)
```

The next frame shows the result part. It retrieves the resulting nodes, parses them as Repository objects, and extract its name and description.

```
{
    nodes {
        ... on Repository {
            nameWithOwner
            description
            url
        }
    }
}
```

The the next frame shows the full query, which is the concatenation of the search and result part inside the skeleton previous showed:

```
query {
    search(
        first: 10
        type: REPOSITORY,
        query: "releasy",
    ) {
        nodes {
            ... on Repository {
                nameWithOwner
                description
                url
            }
        }
    }
}
```

To execute, you must POST the query to [https://api.github.com/graphql](). Since the API requires authentication, before POST, you need to generate an authentication token, which you create inside the [Personal access token](https://github.com/settings/tokens) tab inside the GitHub Developer Settings.

In our example, we are using public data, so the token does not need any privilege. It is just clicking on "Generate new token", leave all fields blank, and click again "Generate token". However, be aware that the token itself must be kept private.

With the query and the access token ready, I created the following python code to execute the query.

```python
import requests
import json

query = '''
    query {
        search(
            first: 10
            type: REPOSITORY,
            query: "releasy",
        ) {
            nodes {
                ... on Repository {
                    nameWithOwner
                    description
                    url
                }
            }
        }
    }
'''

headers = {'Authorization': f'Bearer {your token here}'}

response = requests.post('https://api.github.com/graphql', headers=headers, json={
    'query': query
})

if response.ok:
    data = json.loads(response.content)
    print(json.dumps(data, indent=2))
```

The result is the following JSON, already parsed by our code.

```json
{
  "data": {
    "search": {
      "nodes": [
        {
          "nameWithOwner": "gosu/releasy",
          "description": "A rake task generator to help with building/packaging/deploying Ruby applications (\u26a0\ufe0f unmaintained)",
          "url": "https://github.com/gosu/releasy"
        },
        {
          "nameWithOwner": "releasy/react-releasy",
          "description": "Relay with zero-configuration. SSR, caching, testing and more.",
          "url": "https://github.com/releasy/react-releasy"
        },
        {
          "nameWithOwner": "vtex/releasy",
          "description": "CLI tool to release node applications with tag and auto semver bump",
          "url": "https://github.com/vtex/releasy"
        },
        {
          "nameWithOwner": "design-all-the-things/releasy",
          "description": "Web app to follow release workflow, from ticket creation to production",
          "url": "https://github.com/design-all-the-things/releasy"
        },
        {
          "nameWithOwner": "Acidmanic/releasy",
          "description": "Release Easy! This is a java command-line application, aimed to automatically detect any package manager used for a given project (current directory) and set version onto responsible files. it finally commits and tags the changes due the version.",
          "url": "https://github.com/Acidmanic/releasy"
        },
        {
          "nameWithOwner": "releasy/releasy-examples",
          "description": null,
          "url": "https://github.com/releasy/releasy-examples"
        },
        {
          "nameWithOwner": "gems-uff/releasy",
          "description": null,
          "url": "https://github.com/gems-uff/releasy"
        },
        {
          "nameWithOwner": "Daio-io/releasy",
          "description": null,
          "url": "https://github.com/Daio-io/releasy"
        },
        {
          "nameWithOwner": "joefiorini/releasy",
          "description": null,
          "url": "https://github.com/joefiorini/releasy"
        },
        {
          "nameWithOwner": "ch-egli/releasy",
          "description": null,
          "url": "https://github.com/ch-egli/releasy"
        }
      ]
    }
  }
}
```

Which, of course, I will highlight our research project. :)

```json
{
    "nameWithOwner": "gems-uff/releasy",
    "description": null,
    "url": "https://github.com/gems-uff/releasy"
},
```

Now, I will complete the query, including the number of commits. We need to get the repository HEAD, parse the result as commits, fetch its history, and count. 

```
object(expression: "HEAD") {
    ... on Commit { 
        history{ totalCount }
    }
}
```

The next frame shows the complete query:

```
query {
    search(
        first: 10
        type: REPOSITORY,
        query: "releasy",
    ) {
        nodes {
            ... on Repository {
                nameWithOwner
                description
                url
                object(expression: "HEAD") {
                    ... on Commit { 
                        history{ totalCount }
                    }
                }
            }
        }
    }
}
```

And a subtract of the result:

```json
{
  "data": {
    "search": {
      "nodes": [
        (...)
        {
          "nameWithOwner": "gems-uff/releasy",
          "description": null,
          "url": "https://github.com/gems-uff/releasy",
          "object": {
            "history": {
              "totalCount": 176
            }
          }
        },
        (...)
      ]
    }
  }
}
```

This post teaches how to create and execute GraphQL queries on GitHub. It helps to retrieve information without running multiple queries and avoid become stuck with the API rate limits. In the future, I will write another post explaining advanced queries. 

Please, write your comments below. 

