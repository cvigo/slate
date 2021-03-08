---
title: LRA Deployment API v1.0.0
language_tabs:
  - ruby: Ruby
  - python: Python
language_clients:
  - ruby: ""
  - python: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="lra-deployment-api">LRA Deployment API v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

LRA Deployment API exposes the LRA Deployment

Base URLs:

* <a href="https://developers.bbva.com//LraDeployment/v1">https://developers.bbva.com//LraDeployment/v1</a>

Email: <a href="mailto:you@your-company.com">Support</a> 

<h1 id="lra-deployment-api-services">services</h1>

Top level (service level) CRUD functions

## Creates a new Service with its basic properties

<a id="opIdcreateService"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json'
}

result = RestClient.put 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json'
}

r = requests.put('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}', headers = headers)

print(r.json())

```

`PUT /author_geographies/{auth_geography}/services/{service_name}`

Creates a new Service with its basic properties

> Body parameter

```json
{
  "spec": {},
  "default_repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/financial_management_data_lra_serv.git"
}
```

<h3 id="creates-a-new-service-with-its-basic-properties-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|body|body|[ServiceWithVersions](#schemaservicewithversions)|false|Deployment request|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|

<h3 id="creates-a-new-service-with-its-basic-properties-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|Deployment request accepted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets the details of a Service and its Release Versions

<a id="opIdgetSercice"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/services/{service_name}`

Gets the details of a Service and its Release Versions

<h3 id="gets-the-details-of-a-service-and-its-release-versions-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|

> Example responses

> 200 Response

```json
null
```

<h3 id="gets-the-details-of-a-service-and-its-release-versions-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<h3 id="gets-the-details-of-a-service-and-its-release-versions-responseschema">Response Schema</h3>

Status Code **200**

*The Service version if in queue for build*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» name|string|false|read-only|The unique LRA Service Name.<br>It is also used as the name for the virtual host for the Service.|
|» spec|any|false|none|LRA Service properties (future use maybe?)|
|» default_repo|string|false|none|Default repository URL. Used when the release version does not specify a repository URL|
|» versions|[[Version](#schemaversion)]|false|read-only|[One Service version, that is defined by a code version and an array of configuration objects]|
|»» name|string|true|none|Semantic version name|
|»» repo|string|false|none|URL to the repo that contains the service source code.<br>It overwrites the default repo property at `Service` level|
|»» commit|string|true|none|Git commit hash that contains the source code for this Release Version|
|»» git_tag|string|false|none|Optional Git tag name. Just informative. The code will be taken from the given commit hash|
|»» git_branch|string|false|none|Optional Git branch. Just informative. The code will be taken from the given commit hash|
|»» configs|[[Config](#schemaconfig)]|false|none|Configuration Resources used by this Service|
|»»» name|string|true|none|Service Configuration Object name|
|»» timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|»» status|object|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|
|»»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»»» stages|[[StatusEvent](#schemastatusevent)]|false|none|A list that contains status details of all the deployment stages that the request has gone through|
|»»»» stage|string|false|none|The name of the stage being reported|
|»»»» description|string|false|none|The description of the stage to be updated|
|»»»» status|string|false|none|* queued: the deployment request as been accepted and queued in the deployment pipeline<br>* inProgress: the deployment request has been accepted and is being processed. Image building can take some time...<br>* scheduled: the Service artifacts are ready and the deployment will be attempted in the next batch<br>* failed: cannot build the Service Artifacts<br>* skipped: the Service has not been deployed in the last batch because one or more dependencies are not met. See "schedule.notBeforeDate" and "schedule.notBeforeServices" in the request<br>* reverted: the requested deployment caused the service not to start with the new configuration, so it has been reverted to the last known working configuration.<br>* partial: the Service has been deployed but not all the conditions have been satisfied<br>* done: Stage succeeded|
|»»»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»»»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»»»» error_reasons|[string]|false|none|Error reasons. This field usually comes when the error flag is set to true.|
|»»»» start_time|string(date-time)|false|none|Stage's start time (ISO 8601 with RFC 3339 profile)|
|»»»» end_time|string(date-time)|false|none|Stage's end time (ISO 8601 with RFC 3339 profile)|

#### Enumerated Values

|Property|Value|
|---|---|
|status|queued|
|status|inProgress|
|status|scheduled|
|status|failed|
|status|skipped|
|status|reverted|
|status|partial|
|status|done|

<aside class="success">
This operation does not require authentication
</aside>

## Deletes all the Service Release versions and their artifacts.

<a id="opIddeleteService"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.delete('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}')

print(r.json())

```

`DELETE /author_geographies/{auth_geography}/services/{service_name}`

Deletes all the Service Release versions and their artifacts.
The command fails if any of them is in use in any environment

<h3 id="deletes-all-the-service-release-versions-and-their-artifacts.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|

<h3 id="deletes-all-the-service-release-versions-and-their-artifacts.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|Request accepted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|One or more Release versions are in use|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="lra-deployment-api-release-versions">release versions</h1>

Service Release Versions CRUD functions

## Adds or modifies a Release Version for a Service. Only SNAPSHOT versions can be modified

<a id="opIdaddServiceVersion"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json'
}

result = RestClient.put 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/versions/{version}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json'
}

r = requests.put('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/versions/{version}', headers = headers)

print(r.json())

```

`PUT /author_geographies/{auth_geography}/services/{service_name}/versions/{version}`

Request to create a new Release Version for a Service, or to modify an existing one.
The service artifacts are built and stored in the Image Registry for later deployment.
Release Versions (SemVer named) are inmutable, only SNAPSHOT versions can be patched.

> Body parameter

```json
{
  "name": "1.0.0",
  "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/financial_management_data_lra_serv.git",
  "commit": "ca82a6dff817ec66f44342007202690a93763949",
  "git_tag": "v1.0.0",
  "git_branch": "feature/new_functions",
  "configs": [
    {
      "name": "config_1"
    }
  ]
}
```

<h3 id="adds-or-modifies-a-release-version-for-a-service.-only-snapshot-versions-can-be-modified-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|version|path|string|true|SemVer version name|
|body|body|[Version](#schemaversion)|false|Version details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|

<h3 id="adds-or-modifies-a-release-version-for-a-service.-only-snapshot-versions-can-be-modified-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|Request accepted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<aside class="success">
This operation does not require authentication
</aside>

## Deletes a Release Version

<a id="opIdremoveServiceVersion"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/versions/{version}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.delete('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/versions/{version}')

print(r.json())

```

`DELETE /author_geographies/{auth_geography}/services/{service_name}/versions/{version}`

Deletes a Release Versions.
The command fails if the Release Version is in use in any environment

<h3 id="deletes-a-release-version-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|version|path|string|true|SemVer version name|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|

<h3 id="deletes-a-release-version-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|Request accepted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|One or more Release versions are in use|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets the current status of a Release Version

<a id="opIdgetServiceVersion"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/versions/{version}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/versions/{version}', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/services/{service_name}/versions/{version}`

Gets the current status of a Release Version, in terms of readiness for deployment.
Can be used to know if the Release Version is eligible for deployment or the causes that make it not eligible.
Should not be used to get the current deployments of the Release Version.

<h3 id="gets-the-current-status-of-a-release-version-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|version|path|string|true|SemVer version name|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|

> Example responses

> 200 Response

```json
{
  "name": "1.0.0",
  "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/financial_management_data_lra_serv.git",
  "commit": "ca82a6dff817ec66f44342007202690a93763949",
  "git_tag": "v1.0.0",
  "git_branch": "feature/new_functions",
  "configs": [
    {
      "name": "config_1"
    }
  ],
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}
```

<h3 id="gets-the-current-status-of-a-release-version-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Version](#schemaversion)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="lra-deployment-api-deployment-requests">deployment requests</h1>

Deployments with basic traffic rules CRUD functions

## Adds the default deployment, with weight based traffic rules.

<a id="opIdaddDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests', headers = headers)

print(r.json())

```

`POST /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests`

Request to install the default deployment for a Service, with weight based traffic rules, in the given environment.
Requests are queued according to the `schedule` parameter in the request payload. They can be cancelled by issuing a DELETE call.
If two requests are scheduled for the same target time, the behavior is undetermined.
The command fails if any of the Release Versions does not exist.

> Body parameter

```json
{
  "traffic": [
    {
      "version": "1.0.0",
      "weight": 70
    },
    {
      "version": "1.0.1",
      "weight": 30
    }
  ],
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  }
}
```

<h3 id="adds-the-default-deployment,-with-weight-based-traffic-rules.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|body|body|[DeploymentRequest](#schemadeploymentrequest)|false|Default Deployment details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
{
  "id": "string"
}
```

<h3 id="adds-the-default-deployment,-with-weight-based-traffic-rules.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Id](#schemaid)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets the list of Service Deployment requests in the given environment

<a id="opIdgetDeployments"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests`

Gets the list of Service Deployment requests in the given environment.
PENDING: Filters

<h3 id="gets-the-list-of-service-deployment-requests-in-the-given-environment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|is_completed|query|boolean|false|If true, gets only the requests which status is completed (either OK or KO)|
|got_error|query|boolean|false|If true, gets only the failed requests|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
[
  {
    "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
    "traffic": [
      {
        "version": "1.0.0",
        "weight": 70
      },
      {
        "version": "1.0.1",
        "weight": 30
      }
    ],
    "schedule": {
      "not_before_date": "2020-08-29T09:12:33.001Z",
      "not_before_services": [
        {
          "service": "d-personalfinances-v1-financialmanagement",
          "version": "1.0.3"
        },
        {
          "service": "d-personalfinances-v1-userpreferences",
          "version": "1.1.3"
        }
      ]
    },
    "timestamp": "2019-08-24T14:15:22Z",
    "status": null
  }
]
```

<h3 id="gets-the-list-of-service-deployment-requests-in-the-given-environment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<h3 id="gets-the-list-of-service-deployment-requests-in-the-given-environment-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[DeploymentRequest](#schemadeploymentrequest)]|false|none|none|
|» id|string(uuid)|false|read-only|Request ID. Read Only|
|» traffic|[[Weighted_rule](#schemaweighted_rule)]|true|none|default and mandatory traffic rule, an array of service versions and % of traffic going to each one. Must sum 100%|
|»» version|string|true|none|The service version that will get the traffic matching this rule|
|»» weight|integer|true|none|Percentage of the traffic that will be sent to this service version<br>The default rules based on weights must sum 100%|
|» schedule|object|false|none|none|
|»» not_before_date|string(date-time)|false|none|The resource must not be deployed before this date-time. If left empty, It will be deployed ASAP|
|»» not_before_services|[[BeforeService](#schemabeforeservice)]|false|none|none|
|»»» service|string|true|none|LRA Service name that must be scheduled for deployment to meet the dependency|
|»»» version|string|false|none|LRA Service version that must be scheduled for deployment to meet the dependency|
|» timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|» status|object|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|
|»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»» stages|[[StatusEvent](#schemastatusevent)]|false|none|A list that contains status details of all the deployment stages that the request has gone through|
|»»» stage|string|false|none|The name of the stage being reported|
|»»» description|string|false|none|The description of the stage to be updated|
|»»» status|string|false|none|* queued: the deployment request as been accepted and queued in the deployment pipeline<br>* inProgress: the deployment request has been accepted and is being processed. Image building can take some time...<br>* scheduled: the Service artifacts are ready and the deployment will be attempted in the next batch<br>* failed: cannot build the Service Artifacts<br>* skipped: the Service has not been deployed in the last batch because one or more dependencies are not met. See "schedule.notBeforeDate" and "schedule.notBeforeServices" in the request<br>* reverted: the requested deployment caused the service not to start with the new configuration, so it has been reverted to the last known working configuration.<br>* partial: the Service has been deployed but not all the conditions have been satisfied<br>* done: Stage succeeded|
|»»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»»» error_reasons|[string]|false|none|Error reasons. This field usually comes when the error flag is set to true.|
|»»» start_time|string(date-time)|false|none|Stage's start time (ISO 8601 with RFC 3339 profile)|
|»»» end_time|string(date-time)|false|none|Stage's end time (ISO 8601 with RFC 3339 profile)|

#### Enumerated Values

|Property|Value|
|---|---|
|status|queued|
|status|inProgress|
|status|scheduled|
|status|failed|
|status|skipped|
|status|reverted|
|status|partial|
|status|done|

<aside class="success">
This operation does not require authentication
</aside>

## Changes a pending deployment request

<a id="opIdmodifyDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json'
}

result = RestClient.put 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json'
}

r = requests.put('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}', headers = headers)

print(r.json())

```

`PUT /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}`

Request to change a pending Deployment Request.
Requests are queued according to the `schedule` parameter in the request payload. They can be cancelled by issuing a DELETE call.
If two requests are scheduled for the same target time, the behavior is undetermined.
The command fails if any of the Release Versions does not exist.

> Body parameter

```json
{
  "traffic": [
    {
      "version": "1.0.0",
      "weight": 70
    },
    {
      "version": "1.0.1",
      "weight": 30
    }
  ],
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  }
}
```

<h3 id="changes-a-pending-deployment-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|
|body|body|[DeploymentRequest](#schemadeploymentrequest)|false|Default deployment details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

<h3 id="changes-a-pending-deployment-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Cancels a pending deployment request

<a id="opIddeleteDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.delete('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}')

print(r.json())

```

`DELETE /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}`

Cancels a pending Deployment Request.
The command fails if the Request has been already completed or is in progress.

<h3 id="cancels-a-pending-deployment-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

<h3 id="cancels-a-pending-deployment-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Deleted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets a deployment request

<a id="opIdgetDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}`

Gets the Details of a Deployment Request.

<h3 id="gets-a-deployment-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "traffic": [
    {
      "version": "1.0.0",
      "weight": 70
    },
    {
      "version": "1.0.1",
      "weight": 30
    }
  ],
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  },
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}
```

<h3 id="gets-a-deployment-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DeploymentRequest](#schemadeploymentrequest)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="lra-deployment-api-advanced-traffic-rule-requests">advanced traffic rule requests</h1>

Advanced traffic rules CRUD functions

## Adds a new traffic advanced rule for a Service

<a id="opIdaddTrafficRule"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/', headers = headers)

print(r.json())

```

`POST /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/`

Request to install a new traffic rule for a Service in the given environment.

> Body parameter

```json
{
  "traffic": {
    "version": "1.0.1-TEST",
    "headers": [
      {
        "header_name": "x-my-header_1",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      },
      {
        "header_name": "x-my-header_2",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      }
    ]
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  }
}
```

<h3 id="adds-a-new-traffic-advanced-rule-for-a-service-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|body|body|[AdvancedTrafficRuleRequest](#schemaadvancedtrafficrulerequest)|false|Traffic Rule details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
{
  "id": "string"
}
```

<h3 id="adds-a-new-traffic-advanced-rule-for-a-service-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Id](#schemaid)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets the list of traffic advanced rule requests in the given environment

<a id="opIdgetTrafficRules"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/`

Gets the list of advanced traffic rule requests in the given environment.
PENDING: Filters

<h3 id="gets-the-list-of-traffic-advanced-rule-requests-in-the-given-environment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|is_completed|query|boolean|false|If true, gets only the requests which status is completed (either OK or KO)|
|got_error|query|boolean|false|If true, gets only the failed requests|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
[
  {
    "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
    "traffic": {
      "version": "1.0.1-TEST",
      "headers": [
        {
          "header_name": "x-my-header_1",
          "match": {
            "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
          }
        },
        {
          "header_name": "x-my-header_2",
          "match": {
            "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
          }
        }
      ]
    },
    "schedule": {
      "not_before_date": "2020-08-29T09:12:33.001Z",
      "not_before_services": [
        {
          "service": "d-personalfinances-v1-financialmanagement",
          "version": "1.0.3"
        },
        {
          "service": "d-personalfinances-v1-userpreferences",
          "version": "1.1.3"
        }
      ]
    },
    "timestamp": "2019-08-24T14:15:22Z",
    "status": null
  }
]
```

<h3 id="gets-the-list-of-traffic-advanced-rule-requests-in-the-given-environment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<h3 id="gets-the-list-of-traffic-advanced-rule-requests-in-the-given-environment-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[AdvancedTrafficRuleRequest](#schemaadvancedtrafficrulerequest)]|false|none|none|
|» id|string(uuid)|false|read-only|Request ID. Read Only|
|» traffic|object|true|none|Client calls including the given http headers will be routed to the given Release Version of this Service|
|»» id|string(uuid)|false|read-only|ID assigned to this rule upon creation time|
|»» version|string|true|none|The service version that will get the traffic that matches this rule|
|»» headers|[[Header](#schemaheader)]|true|none|set of header matching rules that must be true for this rule to be effective|
|»»» header_name|string|false|none|The name of the http header to be used|
|»»» match|any|true|none|Header must match an exact value or a regular expression.|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»» *anonymous*|object|false|none|none|
|»»»»» exact|string|true|none|The exact value that the header must contain to match this rule|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»» *anonymous*|object|false|none|none|
|»»»»» regex|string|true|none|The regular expression that the value in the header must match to match this rule|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» schedule|object|false|none|none|
|»» not_before_date|string(date-time)|false|none|The resource must not be deployed before this date-time. If left empty, It will be deployed ASAP|
|»» not_before_services|[[BeforeService](#schemabeforeservice)]|false|none|none|
|»»» service|string|true|none|LRA Service name that must be scheduled for deployment to meet the dependency|
|»»» version|string|false|none|LRA Service version that must be scheduled for deployment to meet the dependency|
|» timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|» status|object|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|
|»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»» stages|[[StatusEvent](#schemastatusevent)]|false|none|A list that contains status details of all the deployment stages that the request has gone through|
|»»» stage|string|false|none|The name of the stage being reported|
|»»» description|string|false|none|The description of the stage to be updated|
|»»» status|string|false|none|* queued: the deployment request as been accepted and queued in the deployment pipeline<br>* inProgress: the deployment request has been accepted and is being processed. Image building can take some time...<br>* scheduled: the Service artifacts are ready and the deployment will be attempted in the next batch<br>* failed: cannot build the Service Artifacts<br>* skipped: the Service has not been deployed in the last batch because one or more dependencies are not met. See "schedule.notBeforeDate" and "schedule.notBeforeServices" in the request<br>* reverted: the requested deployment caused the service not to start with the new configuration, so it has been reverted to the last known working configuration.<br>* partial: the Service has been deployed but not all the conditions have been satisfied<br>* done: Stage succeeded|
|»»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»»» error_reasons|[string]|false|none|Error reasons. This field usually comes when the error flag is set to true.|
|»»» start_time|string(date-time)|false|none|Stage's start time (ISO 8601 with RFC 3339 profile)|
|»»» end_time|string(date-time)|false|none|Stage's end time (ISO 8601 with RFC 3339 profile)|

#### Enumerated Values

|Property|Value|
|---|---|
|status|queued|
|status|inProgress|
|status|scheduled|
|status|failed|
|status|skipped|
|status|reverted|
|status|partial|
|status|done|

<aside class="success">
This operation does not require authentication
</aside>

## Modify an existing advanced traffic rule for a Service

<a id="opIdmodifyTrafficRule"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json'
}

result = RestClient.put 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json'
}

r = requests.put('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}', headers = headers)

print(r.json())

```

`PUT /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}`

Request to modify an existing advanced traffic rule for a Service in the given environment.

> Body parameter

```json
{
  "traffic": {
    "version": "1.0.1-TEST",
    "headers": [
      {
        "header_name": "x-my-header_1",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      },
      {
        "header_name": "x-my-header_2",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      }
    ]
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  }
}
```

<h3 id="modify-an-existing-advanced-traffic-rule-for-a-service-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|
|body|body|[AdvancedTrafficRuleRequest](#schemaadvancedtrafficrulerequest)|false|Traffic Rule details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

<h3 id="modify-an-existing-advanced-traffic-rule-for-a-service-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Request accepted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Removes an advanced traffic rule of a Service from the given environment.

<a id="opIdremoveTrafficRule"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.delete('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}')

print(r.json())

```

`DELETE /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}`

Request to delete an advanced traffic rule of a Service in the given environment.

<h3 id="removes-an-advanced-traffic-rule-of-a-service-from-the-given-environment.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

<h3 id="removes-an-advanced-traffic-rule-of-a-service-from-the-given-environment.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|Request accepted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets an advanced traffic rule rule request

<a id="opIdgetTrafficRule"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/services/{service_name}/deployment_geographies/{deploy_geography}/environments/{environment}/advanced_traffic_rules_requests/{id}`

Gets the Details of a Deployment Request.

<h3 id="gets-an-advanced-traffic-rule-rule-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|service_name|path|string|true|LRA Service Name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "traffic": {
    "version": "1.0.1-TEST",
    "headers": [
      {
        "header_name": "x-my-header_1",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      },
      {
        "header_name": "x-my-header_2",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      }
    ]
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  },
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}
```

<h3 id="gets-an-advanced-traffic-rule-rule-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[AdvancedTrafficRuleRequest](#schemaadvancedtrafficrulerequest)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="lra-deployment-api-service-configs-deployment-requests">service configs deployment requests</h1>

Service Configs CRUD functions

## Request to deploy a new LRA Service Config Object. The object must be deployed in a specific environment, given in the payload

<a id="opIdaddConfigurationDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests', headers = headers)

print(r.json())

```

`POST /author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests`

Request to deploy a LRA Service Configuration in the given environment.
Requests are queued according to the `schedule` parameter in the request payload. They can be cancelled by issuing a `DELETE` call.
If two requests are scheduled for the same target time, the behavior is undetermined.

> Body parameter

```json
{
  "config": {
    "name": "config_1",
    "variables": {
      "from_repo": {
        "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
        "commit": "ca82a6dff817ec66f44342007202690a93763949",
        "git_tag": "v1.0.0"
      }
    }
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  }
}
```

<h3 id="request-to-deploy-a-new-lra-service-config-object.-the-object-must-be-deployed-in-a-specific-environment,-given-in-the-payload-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|config_name|path|string|true|LRA Service Configuration name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|body|body|[ConfigurationDeploymentRequest](#schemaconfigurationdeploymentrequest)|false|Service Configuration deployment details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
{
  "id": "string"
}
```

<h3 id="request-to-deploy-a-new-lra-service-config-object.-the-object-must-be-deployed-in-a-specific-environment,-given-in-the-payload-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Id](#schemaid)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<aside class="success">
This operation does not require authentication
</aside>

## Lists all deployment requests for a Configuration Objects in the given environment

<a id="opIdgetConfigurationDeployments"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests`

Lists all deployment requests for a Configuration Objects in the given environment
PENDING: Filters

<h3 id="lists-all-deployment-requests-for-a-configuration-objects-in-the-given-environment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|config_name|path|string|true|LRA Service Configuration name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|is_completed|query|boolean|false|If true, gets only the requests which status is completed (either OK or KO)|
|got_error|query|boolean|false|If true, gets only the failed requests|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
[
  {
    "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
    "config": {
      "name": "config_1",
      "variables": {
        "from_repo": {
          "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
          "commit": "ca82a6dff817ec66f44342007202690a93763949",
          "git_tag": "v1.0.0"
        }
      }
    },
    "schedule": {
      "not_before_date": "2020-08-29T09:12:33.001Z",
      "not_before_services": [
        {
          "service": "d-personalfinances-v1-financialmanagement",
          "version": "1.0.3"
        },
        {
          "service": "d-personalfinances-v1-userpreferences",
          "version": "1.1.3"
        }
      ]
    },
    "timestamp": "2019-08-24T14:15:22Z",
    "status": null
  }
]
```

<h3 id="lists-all-deployment-requests-for-a-configuration-objects-in-the-given-environment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|

<h3 id="lists-all-deployment-requests-for-a-configuration-objects-in-the-given-environment-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[ConfigurationDeploymentRequest](#schemaconfigurationdeploymentrequest)]|false|none|none|
|» id|string(uuid)|false|read-only|Request ID. Read Only|
|» config|object|true|none|LRA Service configuration object, made of a simple array of string key/value|
|»» name|string|false|none|The unique name of this configuration. Configuration objects have no versions|
|»» variables|any|false|none|configuration can be either taken from a repo or passed as key/value array parameter|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»» *anonymous*|object|false|none|none|
|»»»» from_repo|object|false|none|Repository and pointer to a commit that contains the configuration object|
|»»»»» repo|string|false|none|URL to the repo that contains the source files for the configuration object|
|»»»»» commit|string|false|none|Git commit hash that contains the source files for the configuration object|
|»»»»» git_tag|string|false|none|Optional Git tag name. Just informative. The code will be taken from the given commit hash|
|»»»»» git_branch|string|false|none|Optional Git branch. Just informative. The code will be taken from the given commit hash|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»» *anonymous*|object|false|none|none|
|»»»» specific|[[ConfigurationItems](#schemaconfigurationitems)]|true|none|[LRA Service Configuration variable, just a key/value pair]|
|»»»»» key|string|false|none|none|
|»»»»» value|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» schedule|object|false|none|none|
|»» not_before_date|string(date-time)|false|none|The resource must not be deployed before this date-time. If left empty, It will be deployed ASAP|
|»» not_before_services|[[BeforeService](#schemabeforeservice)]|false|none|none|
|»»» service|string|true|none|LRA Service name that must be scheduled for deployment to meet the dependency|
|»»» version|string|false|none|LRA Service version that must be scheduled for deployment to meet the dependency|
|» timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|» status|object|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|
|»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»» stages|[[StatusEvent](#schemastatusevent)]|false|none|A list that contains status details of all the deployment stages that the request has gone through|
|»»» stage|string|false|none|The name of the stage being reported|
|»»» description|string|false|none|The description of the stage to be updated|
|»»» status|string|false|none|* queued: the deployment request as been accepted and queued in the deployment pipeline<br>* inProgress: the deployment request has been accepted and is being processed. Image building can take some time...<br>* scheduled: the Service artifacts are ready and the deployment will be attempted in the next batch<br>* failed: cannot build the Service Artifacts<br>* skipped: the Service has not been deployed in the last batch because one or more dependencies are not met. See "schedule.notBeforeDate" and "schedule.notBeforeServices" in the request<br>* reverted: the requested deployment caused the service not to start with the new configuration, so it has been reverted to the last known working configuration.<br>* partial: the Service has been deployed but not all the conditions have been satisfied<br>* done: Stage succeeded|
|»»» completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|»»» error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|»»» error_reasons|[string]|false|none|Error reasons. This field usually comes when the error flag is set to true.|
|»»» start_time|string(date-time)|false|none|Stage's start time (ISO 8601 with RFC 3339 profile)|
|»»» end_time|string(date-time)|false|none|Stage's end time (ISO 8601 with RFC 3339 profile)|

#### Enumerated Values

|Property|Value|
|---|---|
|status|queued|
|status|inProgress|
|status|scheduled|
|status|failed|
|status|skipped|
|status|reverted|
|status|partial|
|status|done|

<aside class="success">
This operation does not require authentication
</aside>

## Changes a pending Configuration deployment request

<a id="opIdmodifyConfigurationDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json'
}

result = RestClient.put 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json'
}

r = requests.put('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}', headers = headers)

print(r.json())

```

`PUT /author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}`

Request to change a pending Configuration Deployment Request.
Requests are queued according to the `schedule` parameter in the request payload. They can be cancelled by issuing a `DELETE` call.
If two requests are scheduled for the same target time, the behavior is undetermined.

> Body parameter

```json
{
  "config": {
    "name": "config_1",
    "variables": {
      "from_repo": {
        "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
        "commit": "ca82a6dff817ec66f44342007202690a93763949",
        "git_tag": "v1.0.0"
      }
    }
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  }
}
```

<h3 id="changes-a-pending-configuration-deployment-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|config_name|path|string|true|LRA Service Configuration name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|
|body|body|[ConfigurationDeploymentRequest](#schemaconfigurationdeploymentrequest)|false|Default deployment details|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

<h3 id="changes-a-pending-configuration-deployment-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Cancels a pending Configuration deployment request

<a id="opIddeleteConfigurationDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.delete('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}')

print(r.json())

```

`DELETE /author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}`

Cancels a pending Configuration Deployment Request.
The command fails if the Request has been already completed or is in progress.

<h3 id="cancels-a-pending-configuration-deployment-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|config_name|path|string|true|LRA Service Configuration name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

<h3 id="cancels-a-pending-configuration-deployment-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Deleted|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Gets a Configuration deployment request

<a id="opIdgetConfigurationDeployment"></a>

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://developers.bbva.com/LraDeployment/v1/author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}', headers = headers)

print(r.json())

```

`GET /author_geographies/{auth_geography}/configurations/{config_name}/deployment_geographies/{deploy_geography}/environments/{environment}/deployment_requests/{id}`

Gets the Details of a Configuration Deployment Request.

<h3 id="gets-a-configuration-deployment-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|auth_geography|path|[Geography](#schemageography)|true|Geography where the Service is developed, typically the country code|
|config_name|path|string|true|LRA Service Configuration name|
|deploy_geography|path|[Geography](#schemageography)|true|Geography where the Service Lives, typically the country code|
|environment|path|[Environment](#schemaenvironment)|true|Logical environment, DEV, INT, AUS, etc.|
|id|path|string(uuid)|true|Request ID|

#### Enumerated Values

|Parameter|Value|
|---|---|
|auth_geography|ESP|
|auth_geography|MEX|
|auth_geography|GLO|
|auth_geography|COL|
|auth_geography|PER|
|auth_geography|ARG|
|auth_geography|USA|
|auth_geography|URY|
|auth_geography|PAR|
|auth_geography|VEN|
|deploy_geography|ESP|
|deploy_geography|MEX|
|deploy_geography|GLO|
|deploy_geography|COL|
|deploy_geography|PER|
|deploy_geography|ARG|
|deploy_geography|USA|
|deploy_geography|URY|
|deploy_geography|PAR|
|deploy_geography|VEN|
|environment|DEV|
|environment|INT|
|environment|UAT|
|environment|PRF|
|environment|PRE|
|environment|PRO|

> Example responses

> 200 Response

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "config": {
    "name": "config_1",
    "variables": {
      "from_repo": {
        "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
        "commit": "ca82a6dff817ec66f44342007202690a93763949",
        "git_tag": "v1.0.0"
      }
    }
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  },
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}
```

<h3 id="gets-a-configuration-deployment-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ConfigurationDeploymentRequest](#schemaconfigurationdeploymentrequest)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|invalid input parameters|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found.|None|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_Schedule">Schedule</h2>
<!-- backwards compatibility -->
<a id="schemaschedule"></a>
<a id="schema_Schedule"></a>
<a id="tocSschedule"></a>
<a id="tocsschedule"></a>

```json
{
  "not_before_date": "2020-08-29T09:12:33.001Z",
  "not_before_services": [
    {
      "service": "d-personalfinances-v1-financialmanagement",
      "version": "1.0.3"
    },
    {
      "service": "d-personalfinances-v1-userpreferences",
      "version": "1.1.3"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|not_before_date|string(date-time)|false|none|The resource must not be deployed before this date-time. If left empty, It will be deployed ASAP|
|not_before_services|[[BeforeService](#schemabeforeservice)]|false|none|none|

<h2 id="tocS_BeforeService">BeforeService</h2>
<!-- backwards compatibility -->
<a id="schemabeforeservice"></a>
<a id="schema_BeforeService"></a>
<a id="tocSbeforeservice"></a>
<a id="tocsbeforeservice"></a>

```json
[
  {
    "service": "d-personalfinances-v1-financialmanagement",
    "version": "1.0.3"
  },
  {
    "service": "d-personalfinances-v1-userpreferences",
    "version": "1.1.3"
  }
]

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|service|string|true|none|LRA Service name that must be scheduled for deployment to meet the dependency|
|version|string|false|none|LRA Service version that must be scheduled for deployment to meet the dependency|

<h2 id="tocS_DeploymentRequest">DeploymentRequest</h2>
<!-- backwards compatibility -->
<a id="schemadeploymentrequest"></a>
<a id="schema_DeploymentRequest"></a>
<a id="tocSdeploymentrequest"></a>
<a id="tocsdeploymentrequest"></a>

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "traffic": [
    {
      "version": "1.0.0",
      "weight": 70
    },
    {
      "version": "1.0.1",
      "weight": 30
    }
  ],
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  },
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|read-only|Request ID. Read Only|
|traffic|[Deployment](#schemadeployment)|true|none|default and mandatory traffic rule, an array of service versions and % of traffic going to each one. Must sum 100%|
|schedule|[Schedule](#schemaschedule)|false|none|none|
|timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|status|[Status](#schemastatus)|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|

<h2 id="tocS_AdvancedTrafficRuleRequest">AdvancedTrafficRuleRequest</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedtrafficrulerequest"></a>
<a id="schema_AdvancedTrafficRuleRequest"></a>
<a id="tocSadvancedtrafficrulerequest"></a>
<a id="tocsadvancedtrafficrulerequest"></a>

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "traffic": {
    "version": "1.0.1-TEST",
    "headers": [
      {
        "header_name": "x-my-header_1",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      },
      {
        "header_name": "x-my-header_2",
        "match": {
          "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
        }
      }
    ]
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  },
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|read-only|Request ID. Read Only|
|traffic|[AdvancedTrafficRule](#schemaadvancedtrafficrule)|true|none|none|
|schedule|[Schedule](#schemaschedule)|false|none|none|
|timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|status|[Status](#schemastatus)|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|

<h2 id="tocS_ServiceWithVersions">ServiceWithVersions</h2>
<!-- backwards compatibility -->
<a id="schemaservicewithversions"></a>
<a id="schema_ServiceWithVersions"></a>
<a id="tocSservicewithversions"></a>
<a id="tocsservicewithversions"></a>

```json
{
  "name": "b-personalfinances-v1-financialmanagement",
  "spec": {},
  "default_repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/financial_management_data_lra_serv.git",
  "versions": [
    {
      "name": "1.0.0",
      "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/financial_management_data_lra_serv.git",
      "commit": "ca82a6dff817ec66f44342007202690a93763949",
      "git_tag": "v1.0.0",
      "git_branch": "feature/new_functions",
      "configs": [
        {
          "name": "config_1"
        }
      ],
      "timestamp": "2019-08-24T14:15:22Z",
      "status": null
    }
  ]
}

```

LRA Service and its deployment metadata for a specific environment

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|read-only|The unique LRA Service Name.<br>It is also used as the name for the virtual host for the Service.|
|spec|[ServiceSpec](#schemaservicespec)|false|none|LRA Service properties (future use maybe?)|
|default_repo|string|false|none|Default repository URL. Used when the release version does not specify a repository URL|
|versions|[[Version](#schemaversion)]|false|read-only|[One Service version, that is defined by a code version and an array of configuration objects]|

<h2 id="tocS_ServiceSpec">ServiceSpec</h2>
<!-- backwards compatibility -->
<a id="schemaservicespec"></a>
<a id="schema_ServiceSpec"></a>
<a id="tocSservicespec"></a>
<a id="tocsservicespec"></a>

```json
{}

```

LRA Service properties (future use maybe?)

### Properties

*None*

<h2 id="tocS_Version">Version</h2>
<!-- backwards compatibility -->
<a id="schemaversion"></a>
<a id="schema_Version"></a>
<a id="tocSversion"></a>
<a id="tocsversion"></a>

```json
{
  "name": "1.0.0",
  "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/financial_management_data_lra_serv.git",
  "commit": "ca82a6dff817ec66f44342007202690a93763949",
  "git_tag": "v1.0.0",
  "git_branch": "feature/new_functions",
  "configs": [
    {
      "name": "config_1"
    }
  ],
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}

```

One Service version, that is defined by a code version and an array of configuration objects

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|Semantic version name|
|repo|string|false|none|URL to the repo that contains the service source code.<br>It overwrites the default repo property at `Service` level|
|commit|string|true|none|Git commit hash that contains the source code for this Release Version|
|git_tag|string|false|none|Optional Git tag name. Just informative. The code will be taken from the given commit hash|
|git_branch|string|false|none|Optional Git branch. Just informative. The code will be taken from the given commit hash|
|configs|[[Config](#schemaconfig)]|false|none|Configuration Resources used by this Service|
|timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|status|[Status](#schemastatus)|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|

<h2 id="tocS_Config">Config</h2>
<!-- backwards compatibility -->
<a id="schemaconfig"></a>
<a id="schema_Config"></a>
<a id="tocSconfig"></a>
<a id="tocsconfig"></a>

```json
{
  "name": "config_1"
}

```

Reference to a service configuration object

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|Service Configuration Object name|

<h2 id="tocS_Deployment">Deployment</h2>
<!-- backwards compatibility -->
<a id="schemadeployment"></a>
<a id="schema_Deployment"></a>
<a id="tocSdeployment"></a>
<a id="tocsdeployment"></a>

```json
[
  {
    "version": "1.0.0",
    "weight": 70
  },
  {
    "version": "1.0.1",
    "weight": 30
  }
]

```

default and mandatory traffic rule, an array of service versions and % of traffic going to each one. Must sum 100%

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Weighted_rule](#schemaweighted_rule)]|false|none|default and mandatory traffic rule, an array of service versions and % of traffic going to each one. Must sum 100%|

<h2 id="tocS_AdvancedTrafficRule">AdvancedTrafficRule</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedtrafficrule"></a>
<a id="schema_AdvancedTrafficRule"></a>
<a id="tocSadvancedtrafficrule"></a>
<a id="tocsadvancedtrafficrule"></a>

```json
{
  "version": "1.0.1-TEST",
  "headers": [
    {
      "header_name": "x-my-header_1",
      "match": {
        "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
      }
    },
    {
      "header_name": "x-my-header_2",
      "match": {
        "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
      }
    }
  ]
}

```

### Properties

*None*

<h2 id="tocS_Header_rule">Header_rule</h2>
<!-- backwards compatibility -->
<a id="schemaheader_rule"></a>
<a id="schema_Header_rule"></a>
<a id="tocSheader_rule"></a>
<a id="tocsheader_rule"></a>

```json
{
  "version": "1.0.1-TEST",
  "headers": [
    {
      "header_name": "x-my-header_1",
      "match": {
        "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
      }
    },
    {
      "header_name": "x-my-header_2",
      "match": {
        "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
      }
    }
  ]
}

```

Client calls including the given http headers will be routed to the given Release Version of this Service

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|read-only|ID assigned to this rule upon creation time|
|version|string|true|none|The service version that will get the traffic that matches this rule|
|headers|[[Header](#schemaheader)]|true|none|set of header matching rules that must be true for this rule to be effective|

<h2 id="tocS_Header">Header</h2>
<!-- backwards compatibility -->
<a id="schemaheader"></a>
<a id="schema_Header"></a>
<a id="tocSheader"></a>
<a id="tocsheader"></a>

```json
{
  "header_name": "x-my-header",
  "match": {
    "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|header_name|string|false|none|The name of the http header to be used|
|match|[HeaderMatch](#schemaheadermatch)|true|none|Header must match an exact value or a regular expression.|

<h2 id="tocS_HeaderMatch">HeaderMatch</h2>
<!-- backwards compatibility -->
<a id="schemaheadermatch"></a>
<a id="schema_HeaderMatch"></a>
<a id="tocSheadermatch"></a>
<a id="tocsheadermatch"></a>

```json
{
  "exact": "calls-with-this-header-will-go-to-v1.0.1-TEST"
}

```

### Properties

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» exact|string|true|none|The exact value that the header must contain to match this rule|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» regex|string|true|none|The regular expression that the value in the header must match to match this rule|

<h2 id="tocS_Weighted_rule">Weighted_rule</h2>
<!-- backwards compatibility -->
<a id="schemaweighted_rule"></a>
<a id="schema_Weighted_rule"></a>
<a id="tocSweighted_rule"></a>
<a id="tocsweighted_rule"></a>

```json
{
  "version": "1.0.0",
  "weight": 100
}

```

Standard Service routing. Weighted round-robin algorithm splits the traffic among the given versions

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|version|string|true|none|The service version that will get the traffic matching this rule|
|weight|integer|true|none|Percentage of the traffic that will be sent to this service version<br>The default rules based on weights must sum 100%|

<h2 id="tocS_Role">Role</h2>
<!-- backwards compatibility -->
<a id="schemarole"></a>
<a id="schema_Role"></a>
<a id="tocSrole"></a>
<a id="tocsrole"></a>

```json
{
  "name": "low",
  "functions": [
    "ListBalances",
    "ListMoreStuff"
  ]
}

```

Security role names and the gRPC functions allowed to each one

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|Currently supported roles are "low", "medium" and "high"|
|functions|[RoleFunctions](#schemarolefunctions)|true|none|List of functions that consumers that have this role granted can call|

#### Enumerated Values

|Property|Value|
|---|---|
|name|low|
|name|high|
|name|medium|

<h2 id="tocS_RoleFunctions">RoleFunctions</h2>
<!-- backwards compatibility -->
<a id="schemarolefunctions"></a>
<a id="schema_RoleFunctions"></a>
<a id="tocSrolefunctions"></a>
<a id="tocsrolefunctions"></a>

```json
[
  "ListBalances",
  "ListMoreStuff"
]

```

List of functions that consumers that have this role granted can call

### Properties

*None*

<h2 id="tocS_Status">Status</h2>
<!-- backwards compatibility -->
<a id="schemastatus"></a>
<a id="schema_Status"></a>
<a id="tocSstatus"></a>
<a id="tocsstatus"></a>

```json
{
  "completed": false,
  "error": false,
  "stages": [
    {
      "stage": "compiling",
      "description": "Source code is being compiled into binary artifacts",
      "status": "inProgress",
      "completed": false,
      "error": false,
      "error_reasons": [
        "Not enough quota to deploy multiple replicas for HA, Number of replicas created: 1",
        "Some other feedback..."
      ],
      "start_time": "2020-08-29T09:12:33.001Z",
      "end_time": "2020-08-29T09:12:33.001Z"
    }
  ]
}

```

The service or configuration deployment status
This data structure is used as return value in "GET" API calls

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|stages|[[StatusEvent](#schemastatusevent)]|false|none|A list that contains status details of all the deployment stages that the request has gone through|

<h2 id="tocS_StatusEvent">StatusEvent</h2>
<!-- backwards compatibility -->
<a id="schemastatusevent"></a>
<a id="schema_StatusEvent"></a>
<a id="tocSstatusevent"></a>
<a id="tocsstatusevent"></a>

```json
{
  "stage": "compiling",
  "description": "Source code is being compiled into binary artifacts",
  "status": "inProgress",
  "completed": false,
  "error": false,
  "error_reasons": [
    "Not enough quota to deploy multiple replicas for HA, Number of replicas created: 1",
    "Some other feedback..."
  ],
  "start_time": "2020-08-29T09:12:33.001Z",
  "end_time": "2020-08-29T09:12:33.001Z"
}

```

The service or configuration deployment status at each stage of the deployment pipeline
This data structure is used in the event notification at the end of each deployment stage and as array in "GET" API calls

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|stage|string|false|none|The name of the stage being reported|
|description|string|false|none|The description of the stage to be updated|
|status|string|false|none|* queued: the deployment request as been accepted and queued in the deployment pipeline<br>* inProgress: the deployment request has been accepted and is being processed. Image building can take some time...<br>* scheduled: the Service artifacts are ready and the deployment will be attempted in the next batch<br>* failed: cannot build the Service Artifacts<br>* skipped: the Service has not been deployed in the last batch because one or more dependencies are not met. See "schedule.notBeforeDate" and "schedule.notBeforeServices" in the request<br>* reverted: the requested deployment caused the service not to start with the new configuration, so it has been reverted to the last known working configuration.<br>* partial: the Service has been deployed but not all the conditions have been satisfied<br>* done: Stage succeeded|
|completed|boolean|false|none|Deployment process completion flag.<br>If true indicates that the entire Deployment process has ended, with or without errors,<br>and no further status update will be provided|
|error|boolean|false|none|Determines if an error has occurred during the Deployment process|
|error_reasons|[string]|false|none|Error reasons. This field usually comes when the error flag is set to true.|
|start_time|string(date-time)|false|none|Stage's start time (ISO 8601 with RFC 3339 profile)|
|end_time|string(date-time)|false|none|Stage's end time (ISO 8601 with RFC 3339 profile)|

#### Enumerated Values

|Property|Value|
|---|---|
|status|queued|
|status|inProgress|
|status|scheduled|
|status|failed|
|status|skipped|
|status|reverted|
|status|partial|
|status|done|

<h2 id="tocS_Geography">Geography</h2>
<!-- backwards compatibility -->
<a id="schemageography"></a>
<a id="schema_Geography"></a>
<a id="tocSgeography"></a>
<a id="tocsgeography"></a>

```json
"ESP"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|ESP|
|*anonymous*|MEX|
|*anonymous*|GLO|
|*anonymous*|COL|
|*anonymous*|PER|
|*anonymous*|ARG|
|*anonymous*|USA|
|*anonymous*|URY|
|*anonymous*|PAR|
|*anonymous*|VEN|

<h2 id="tocS_Environment">Environment</h2>
<!-- backwards compatibility -->
<a id="schemaenvironment"></a>
<a id="schema_Environment"></a>
<a id="tocSenvironment"></a>
<a id="tocsenvironment"></a>

```json
"DEV"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|DEV|
|*anonymous*|INT|
|*anonymous*|UAT|
|*anonymous*|PRF|
|*anonymous*|PRE|
|*anonymous*|PRO|

<h2 id="tocS_Runtimes">Runtimes</h2>
<!-- backwards compatibility -->
<a id="schemaruntimes"></a>
<a id="schema_Runtimes"></a>
<a id="tocSruntimes"></a>
<a id="tocsruntimes"></a>

```json
"java"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|java|
|*anonymous*|python|
|*anonymous*|golang|

<h2 id="tocS_ConfigurationDeploymentRequest">ConfigurationDeploymentRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationdeploymentrequest"></a>
<a id="schema_ConfigurationDeploymentRequest"></a>
<a id="tocSconfigurationdeploymentrequest"></a>
<a id="tocsconfigurationdeploymentrequest"></a>

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "config": {
    "name": "config_1",
    "variables": {
      "from_repo": {
        "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
        "commit": "ca82a6dff817ec66f44342007202690a93763949",
        "git_tag": "v1.0.0"
      }
    }
  },
  "schedule": {
    "not_before_date": "2020-08-29T09:12:33.001Z",
    "not_before_services": [
      {
        "service": "d-personalfinances-v1-financialmanagement",
        "version": "1.0.3"
      },
      {
        "service": "d-personalfinances-v1-userpreferences",
        "version": "1.1.3"
      }
    ]
  },
  "timestamp": "2019-08-24T14:15:22Z",
  "status": null
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|read-only|Request ID. Read Only|
|config|[Configuration](#schemaconfiguration)|true|none|LRA Service configuration object, made of a simple array of string key/value|
|schedule|[Schedule](#schemaschedule)|false|none|none|
|timestamp|string(date-time)|false|read-only|Date and time of the request creation or last modification|
|status|[Status](#schemastatus)|false|read-only|The service or configuration deployment status<br>This data structure is used as return value in "GET" API calls|

<h2 id="tocS_Configuration">Configuration</h2>
<!-- backwards compatibility -->
<a id="schemaconfiguration"></a>
<a id="schema_Configuration"></a>
<a id="tocSconfiguration"></a>
<a id="tocsconfiguration"></a>

```json
{
  "name": "config_1",
  "variables": {
    "from_repo": {
      "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
      "commit": "ca82a6dff817ec66f44342007202690a93763949",
      "git_tag": "v1.0.0"
    }
  }
}

```

LRA Service configuration object, made of a simple array of string key/value

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|The unique name of this configuration. Configuration objects have no versions|
|variables|[ConfigVariables](#schemaconfigvariables)|false|none|configuration can be either taken from a repo or passed as key/value array parameter|

<h2 id="tocS_ConfigVariables">ConfigVariables</h2>
<!-- backwards compatibility -->
<a id="schemaconfigvariables"></a>
<a id="schema_ConfigVariables"></a>
<a id="tocSconfigvariables"></a>
<a id="tocsconfigvariables"></a>

```json
{
  "from_repo": {
    "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
    "commit": "ca82a6dff817ec66f44342007202690a93763949",
    "git_tag": "v1.0.0",
    "git_branch": "feature/new_functions"
  }
}

```

### Properties

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» from_repo|[ConfigFromRepo](#schemaconfigfromrepo)|false|none|Repository and pointer to a commit that contains the configuration object|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» specific|[[ConfigurationItems](#schemaconfigurationitems)]|true|none|[LRA Service Configuration variable, just a key/value pair]|

<h2 id="tocS_ConfigFromRepo">ConfigFromRepo</h2>
<!-- backwards compatibility -->
<a id="schemaconfigfromrepo"></a>
<a id="schema_ConfigFromRepo"></a>
<a id="tocSconfigfromrepo"></a>
<a id="tocsconfigfromrepo"></a>

```json
{
  "repo": "https://globaldevtools.bbva.com/bitbucket/scm/gluon/configuration.git",
  "commit": "ca82a6dff817ec66f44342007202690a93763949",
  "git_tag": "v1.0.0",
  "git_branch": "feature/new_functions"
}

```

Repository and pointer to a commit that contains the configuration object

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|repo|string|false|none|URL to the repo that contains the source files for the configuration object|
|commit|string|false|none|Git commit hash that contains the source files for the configuration object|
|git_tag|string|false|none|Optional Git tag name. Just informative. The code will be taken from the given commit hash|
|git_branch|string|false|none|Optional Git branch. Just informative. The code will be taken from the given commit hash|

<h2 id="tocS_ConfigurationItems">ConfigurationItems</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationitems"></a>
<a id="schema_ConfigurationItems"></a>
<a id="tocSconfigurationitems"></a>
<a id="tocsconfigurationitems"></a>

```json
{
  "key": "variable_1",
  "value": "value_for_variable_1"
}

```

LRA Service Configuration variable, just a key/value pair

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|key|string|false|none|none|
|value|string|false|none|none|

<h2 id="tocS_Id">Id</h2>
<!-- backwards compatibility -->
<a id="schemaid"></a>
<a id="schema_Id"></a>
<a id="tocSid"></a>
<a id="tocsid"></a>

```json
{
  "id": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Request Id. Use it to modify or cancel|

