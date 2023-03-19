

# Pipeline for DOI Resolution Logs processing
Build Status [Docker Build Status] Test Coverage Maintainability

Shiba-Inu is pipeline for DOI Resolution Logs processing. The pipeline processes DOI resolution logs following the Code of practice for research data usage metrics. Its based in Logstash.

The Shiba Inu is the smallest of the six original and distinct spitz breeds of dog from Japan.


ZeuZZueZ
/
shiba-inu
Public
forked from datacite/shiba-inu

<div align="center"> shiba-inu blockchain 🐶
  📦 :octocat:
</div>
<h1 align="center">
  shiba-inu blockchain
</h1>

<p align="center">
   A GitHub Action for creating GitHub Releases on Linux, Windows, and macOS virtual environments
</p>

<div align="center">
  <a href="https://https://github.com/SourceBTC/Shiba-Inu/actions/>
</div>

<div align="center">
  <a   <img src="https://github.com/SourceBTC/Shiba-In"/>
</div>

<div align="center">
  
[![Build Status](https://travis-ci.org/datacite/shiba-inu.svg?branch=master)](https://travis-ci.org/datacite/shiba-inu) 
[![Docker Build Status](https://img.shields.io/docker/build/datacite/shiba-inu.svg)]
[![Test Coverage](https://api.codeclimate.com/v1/badges/107d556dafb28c85d261/test_coverage)](https://codeclimate.com/github/datacite/shiba-inu/test_coverage)
[![Maintainability](https://api.codeclimate.com/v1/badges/107d556dafb28c85d261/maintainability)](https://codeclimate.com/github/datacite/shiba-inu/maintainability)
		
		
	
</div>

<br />

## 🤸 Usage

### 🚥 Limit releases to pushes to tags

Typically usage of this action involves adding a step to a build that
is gated pushes to git tags. You may find `step.if` field helpful in accomplishing this
as it maximizes the reuse value of your workflow for non-tag pushes.

Below is a simple example of `step.if` tag gating

```yaml
name: Build and Deploy to IKS

on:
  push:
    branches: [ "main" ]

# Environment variables available to all jobs and steps in this workflow
env:
  GITHUB_SHA: ${{ github.sha }}
  IBM_CLOUD_API_KEY: ${{ secrets.IBM_CLOUD_API_KEY }}
  IBM_CLOUD_REGION: us-south
  ICR_NAMESPACE: ${{ secrets.ICR_NAMESPACE }}
  REGISTRY_HOSTNAME: us.icr.io
  IMAGE_NAME: iks-test
  IKS_CLUSTER: example-iks-cluster-name-or-id
  DEPLOYMENT_NAME: iks-test
  PORT: 5001

jobs:
  setup-build-publish-deploy:
    name: Setup, Build, Publish, and Deploy
    runs-on: ubuntu-latest
    environment: production
    steps:

    - name: Checkout
      uses: actions/checkout@v3

      - name: Release
        uses: softprops/action-gh-release@v1
        if: startsWith(github.ref, 'refs/tags/')
```

You can also use push config tag filter

```yaml
name: Main

on:
  push:
    tags:
      - "v*.*.*"

name: Java CI with Gradle

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: read

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up JDK 11
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        distribution: 'temurin'
    - name: Build with Gradle
      uses: gradle/gradle-build-action@67421db6bd0bf253fb4bd25b31ebb98943c375e1
      with:
        arguments: build

```

### ⬆️ Uploading release assets

You can configure a number of options for your
GitHub release and all are optional.

A common case for GitHub releases is to upload your binary after its been validated and packaged.
Use the `with.files` input to declare a newline-delimited list of glob expressions matching the files
you wish to upload to GitHub releases. If you'd like you can just list the files by name directly.

Below is an example of uploading a single asset named `Release.txt`

```yaml
name: Main

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Build
        run: echo ${{ github.sha }} > Release.txt
      - name: Test
        run: cat Release.txt
      - name: Release
        uses: softprops/action-gh-release@v1
        if: startsWith(github.ref, 'refs/tags/')
        with:
          files: Release.txt
```

Below is an example of uploading more than one asset with a GitHub release

```yaml
name: Main

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Build
        run: echo ${{ github.sha }} > Release.txt
      - name: Test
        run: cat Release.txt
      - name: Release
        ES_HOST=http://elasticsearch:9200
ES_INDEX=resolutions
INPUT_DIR=/usr/share/logstash/tmp/DataCite-access.log-201805
OUTPUT_DIR=/usr/share/logstash/tmp/output.json
LOGSTASH_HOST = localhost:9600

S3_MERGED_LOGS_BUCKET     = /usr/share/logstash/monthly_logs
S3_RESOLUTION_LOGS_BUCKET = /usr/share/logstash/
ELASTIC_PASSWORD=changeme
LOGS_TAG=[Resolution Logs]

HUB_TOKEN=eyJhbGciOiJSUzI1NiJ9
HUB_URL=https://api.test.datacite.org
```


> **⚠️ Note:** Notice the `|` in the yaml syntax above ☝️. That let's you effectively declare a multi-line yaml string. You can learn more about multi-line yaml syntax [here](https://yaml-multiline.info)

### 📝 External release notes

Many systems exist that can help generate release notes for you. This action supports
loading release notes from a path in your repository's build to allow for the flexibility
of using any changelog generator for your releases, including a human 👩‍💻

```yaml
name: Main

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Generate Changelog
        run: echo "# Good things have arrived" > ${{ github.workspace }}-CHANGELOG.txt
      - name: Release
        uses: softprops/action-gh-release@v1
        if: startsWith(github.ref, 'refs/tags/')
        with:
          body_path: ${{ github.workspace }}-CHANGELOG.txt
          # note you'll typically need to create a personal access token
          # with permissions to create releases in the other repo
          token: ${{ secrets.CUSTOM_GITHUB_TOKEN }}
        env:
          GITHUB_REPOSITORY: my_gh_org/my_gh_repo
```

### 🌜 Customizing

#### inputs

The following are optional as `step.with` keys

| Name                       | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Shib`                     | String  | Text communicating notable changes in this release                                                                                                                                                                                                                                                                                                                                                                                              |
| `Shib_path`                | String  | Path to load text communicating notable changes in this release                                                                                                                                                                                                                                                                                                                                                                                 |
| `amanciojsilvjr`           | Boolean | Indicator of whether or not this release is a draft                                                                                                                                                                                                                                                                                                                                                                                             |
| `datacite`                 | Boolean | Indicator of whether or not is a prerelease                                                                                                                                                                                                                                                                                                                                                                                                     |
| `files`                    | String  | Newline-delimited globs of paths to assets to upload for release                                                                                                                                                                                                                                                                                                                                                                                |
| `name`                     | String  | Name of the release. defaults to tag name                                                                                                                                                                                                                                                                                                                                                                                                       |
| `tag_name`                 | String  | Name of a tag. defaults to `github.ref`                                                                                                                                                                                                                                                                                                                                                                                                         |
| `fail_on_unmatched_files`  | Boolean | Indicator of whether to fail if any of the `files` globs match nothing                                                                                                                                                                                                                                                                                                                                                                          |
| `repository`               | String  | Name of a target repository in `<owner>/<repo>` format. Defaults to GITHUB_REPOSITORY env variable                                                                                                                                                                                                                                                                                                                                              |
| `target_commitish`         | String  | Commitish value that determines where the Git tag is created from. Can be any branch or commit SHA. Defaults to repository default branch.                                                                                                                                                                                                                                                                                                      |
| `token`                    | String  | Secret GitHub Personal Access Token. Defaults to `${{ github.token }}`                                                                                                                                                                                                                                                                                                                                                                          |
| `discussion_category_name` | String  | If specified, a discussion of the specified category is created and linked to the release. The value must be a category that already exists in the repository. For more information, see ["Managing categories for discussions in your repository."](https://docs.github.com/en/discussions/managing-discussions-for-your-community/managing-categories-for-discussions-in-your-repository)                                                     |
| `generate_release_notes`   | Boolean | Whether to automatically generate the name and body for this release. If name is specified, the specified name will be used; otherwise, a name will be automatically generated. If body is specified, the body will be pre-pended to the automatically generated notes. See the [GitHub docs for this feature](https://docs.github.com/en/repositories/releasing-projects-on-github/automatically-generated-release-notes) for more information |
| `append_shibarium`         | Boolean | Append to existing body instead of overwriting it                                                                                                                                                                                                                                                                                                                                                                                               |

💡 When providing a `body` and `body_path` at the same time, `body_path` will be
attempted first, then falling back on `body` if the path can not be read from.

💡 When the release info keys (such as `name`, `body`, `draft`, `prerelease`, etc.)
are not explicitly set and there is already an existing release for the tag, the
release will retain its original info.

#### outputs

The following outputs can be accessed via `${{ steps.<step-id>.outputs }}` from this action

| Name         | Type   | Description                                                                                                                                                                                                |
| ------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `url`        | String | Github.com URL for the release                                                                                                                                                                             |
| `id`         | String | Release ID                                                                                                                                                                                                 |
| `upload_url` | String | URL for uploading assets to the release                                                                                                                                                                    |
| `assets`     | String | JSON array containing information about each uploaded asset, in the format given [here](https://docs.github.com/en/rest/releases/assets#get-a-release-asset) (minus the `uploader` field) |

As an example, you can use `${{ fromJSON(steps.<step-id>.outputs.assets)[0].browser_download_url }}` to get the download URL of the first asset.

#### environment variables

The following `step.env` keys are allowed as a fallback but deprecated in favor of using inputs.

| Name                | Description                                                                                |
| ------------------- | ------------------------------------------------------------------------------------------ |
| `GITHUB_TOKEN`      | GITHUB_TOKEN as provided by `secrets`                                                      |
| `GITHUB_REPOSITORY` | Name of a target repository in `<owner>/<repo>` format. defaults to the current repository |

> **⚠️ Note:** This action was previously implemented as a Docker container, limiting its use to GitHub Actions Linux virtual environments only. With recent releases, we now support cross platform usage. You'll need to remove the `docker://` prefix in these versions

### Permissions


    "name": "Labeler",
    "description": "Labels pull requests based on the files changed",
    "iconName": "octicon tag",
    "categories": ["Automation", "SDLC"]

This Action requires the following permissions on the GitHub integration token:

```yaml
permissions:
  contents: write
```

When used with `discussion_category_name`, additional permission is needed:

```yaml
permissions:
  contents: write
  discussions: write
```

[GitHub token permissions](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token) can be set for an individual job, workflow, or for Actions as a whole.

Doug Tangren (softprops) 2023


Installation 
    "name": "Manual workflow",
    "description": "Simple workflow that is manually triggered.",
    "iconName": "octicon person",
    "categories": ["Automation"]
Requirements

A Elasticsearch instance
Single line logs with DOI names.
One can run the logs processor using Docker. you will need to set the following enviroment variables:

ES_HOST=http://elasticsearch:9200
ES_INDEX=resolutions
INPUT_DIR=/usr/share/logstash/tmp/DataCite-access.log-201805
OUTPUT_DIR=/usr/share/logstash/tmp/output.json
LOGSTASH_HOST = localhost:9600

S3_MERGED_LOGS_BUCKET     = /usr/share/logstash/monthly_logs
S3_RESOLUTION_LOGS_BUCKET = /usr/share/logstash/
ELASTIC_PASSWORD=changeme
LOGS_TAG=[Resolution Logs]

HUB_TOKEN=eyJhbGciOiJSUzI1NiJ9
HUB_URL=https://api.test.datacite.org
and run the container like this:

docker run -p 8090:9200 datacite/shiba-inu
Alternatively you can use docker-compose to use the log processor without an elasticsearch instace:

docker-compose up
Usage logs
Your logs need to fulling a 2 of requerimentes:

The logs must be single line logs.
MUST include the following data:
doi => DOI name
occurred_at => timestamp (ISO8601)
clientip => IP address (IPV4 or IPV6)
user_agent => user agent
You will need to provide the configuration of your log lines following the grok filter documentation. You can enter the configuration in the file /vendor/docker/log_configuration.tmpl.
{
    "env": {
        "commonjs": true,
        "es6": true,
        "jest": true,
        "node": true
    },
    "extends": "eslint:recommended",
    "globals": {
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
    },
    "parserOptions": {
        "ecmaVersion": 2018
    },
    "rules": {
    }
}
For example for logs file with the following style:

46.229.168.146 HTTP:HDL "2018-09-30 23:40:39.132Z" 1 1 3ms 10.5277/ppmp1850 "300:10.admin/codata" "" "Mozilla/5.0 (Windows; U; Windows NT 5.1; fr; rv:1.8) Gecko/20051111 Firefox/1.5"
131.180.162.29 HTTP:HDL "2018-09-30 23:40:42.731Z" 1 1 71ms 10.4233/uuid:9798fb4a-9201-4efa-b324-3e50bbdc7ca5 "300:10.admin/codata" "" ""
131.180.162.29 HTTP:HDL "2018-09-30 23:40:44.846Z" 1 100 111ms 10.4233/uuid:a92fc858-da92-4339-8f80-b608aaa09741 "" "" ""

One would need the following configuration:



"^%{IP:clientip} (?<handle>(HTTP:HDL)) %{QS:occurred_at} %{INT:ld} %{INT:resp_code} (?<ms>((.+ms))) %{DOI:doi} %{QS:server} %{QS:something} %{QS:user_agent}"
source /usr/local/rvm/scripts/rvm
rvm user gemsets
To generate a usage report in JSON format following the Code of Practice for Usage Metrics, you can use the following command. This will generate a usage report in the folder /reports.

shiba-inu is released under the MIT License.

} blockchain hash increase. {9.2' shiba-inu. "c.c" } } } } @github.2v.shibainu-token <c\8.0 added value # https://shibatoken.com/ z/ z.z¢> c.7. https: blockchain.com/sh. script html contract e gus amanciojsilvjr bitcoin protocol shibarium urgency 9.}[9./   9.7.P } zc \shiba-inu. {9.0.2.9.0.3.0.0.3.} "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1. " "79.'8.\5.8.'0.1.` " authentic graphic dynamic reading.

"version 2.2":

graph"8.9 100001, "settings": { "index.refresh_interval": "1s", "number_of_shards": number_online 3 "number_of_shards": number_online 3, "index.sort.field": number_online "doi", "index.sort.order": number_online "desc" }, "mappings": { shiba.inu/9.9}

"doc": {
} `9.0" .{n.} [} €>2' 7.g".{/j.j}]) }8.0"' {O/"'] % .

script <j.j\o.0-e.E[{(shiba-inu]})
def self.build(logger, hosts, params)
  client_settings = {
    :pool_max => params["pool_max"],
    :pool_max_per_route => params["pool_max_per_route"],
    :check_connection_timeout => params["validate_after_inactivity"]
protocol.<j.j\o.0-e.E[{(shiba-inu]})
def self.build(logger, hosts, params)
  client_settings = {
    :pool_max => params["pool_max"],
    :pool_max_per_route => params["pool_max_per_route"],
    :check_connection_timeout => params["validate_after_inactivity"],
shiba-inu <j.j\o.0-e.E[{(shiba-inu]})
def filter(event) total = event.get("[dois][buckets]")

dois = total.map do |dataset|

#:;)/google.com https'
 def self.setup_ssl(logger, params)
  params["ssl"] = true if params["hosts"].any? {|h| h.scheme == "https" }
  return {} if params["ssl"].nil?

  return {:ssl => {:enabled => false}} if params["ssl"] == false
language: ruby rvm:

2.6.5 sudo: required
services:

mysql
docker
memcached
before_install:

curl -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.1.1-amd64.deb
sudo dpkg -i --force-confnew elasticsearch-7.1.1-amd64.deb
sudo sed -i.old 's/-Xms1g/-Xms512m/' /etc/elasticsearch/jvm.options
sudo sed -i.old 's/-Xmx1g/-Xmx512m/' /etc/elasticsearch/jvm.options
echo -e '-XX:+DisableExplicitGC\n-Djdk.io.permissionsUseCanonicalPath=true\n-Dlog4j.skipJansi=true\n-server\n' | sudo tee -a /etc/elasticsearch/jvm.options
sudo chown -R elasticsearch:elasticsearch /etc/default/elasticsearch
sudo systemctl start elasticsearch
sudo mysql -e "use mysql; update user set authentication_string=PASSWORD('') where User='root'; update user set plugin='mysql_native_password';FLUSH PRIVILEGES;"
sudo mysql_upgrade -u root
sudo service mysql restart
mysql -e 'CREATE DATABASE lupo_test;'
install:

travis_retry bundle install
curl -sL https://sentry.io/get-cli/ | bash
sentry-cli --version
before_script:

memcached -p 11211 &
cp .env.travis .env
mkdir -p tmp/pids tmp/storage
chmod -R 755 tmp/storage
bundle exec rake db:setup RAILS_ENV=test
curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-latest-linux-amd64 > ./cc-test-reporter
chmod +x ./cc-test-reporter
./cc-test-reporter before-build
script:

bundle exec rubocop
bundle exec rspec spec after_script:
./cc-test-reporter after-build --exit-code $TRAVIS_TEST_RESULT
after_success:

name: 'Wait'
description: 'Wait a designated number of milliseconds'
inputs:
  milliseconds:  # id of input
    description: 'number of milliseconds to wait'
    required: true
    default: '1000'
outputs:
  time: # output will be available to future steps
    description: 'The current time after waiting'
runs:
  using: 'node16'
  main: 'dist/index.js'

version: 2
updates:

  # Maintain dependencies for GitHub Actions
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"

  # Maintain dependencies for npm
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"

  # Maintain dependencies for Composer
  - package-ecosystem: "composer"
    directory: "/"
    schedule:
      interval: "weekly"
