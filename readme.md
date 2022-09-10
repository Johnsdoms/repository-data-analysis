# Data Analysis Script for Thesis

This script was used as part of the case study I conducted as part of my thesis ''. In the thesis it was used to analyse different characteristics of the main direct dependencies from a German public sector software project build up on Open Source Software.

The dependencies' repositories need to be defined in an Array in order to use this script for analysing any GitHub repository.

By using the GitHub API repo data is fetched to calculate multiple metrics and visualize them:
- Languages in repositories
- Summed language extent over all repositories
- Number of pull requests, number of closed ones, closed and merge, resp. closed not merged
- Time to merge pull request (mean, std, min, max)
- Number of Dependabot pull requests, number of opem/ closed Dependabot pull requests, their age, closed and merged/ not merged pull requests, time to merge Dependabot pull requests (mean, std, min, max)

The data is based on the last 1000 pull requests, if there are that many. This is done to not get rate limited when analyzing multiple repositories. If more data is needed or even more repositories should be analyzed at the same time, this can easily be adjusted.

By using the Debricked API the repositories' lock files, defining the used open source software dependencies, are uploaded and scanned. Following metrics are retrieved from the API:
- Dependencies of each repository, number of dependencies
- Number of vulnerabilities in those dependencies
- Number of vulnerabilities having a fix available


## How to use
1. First, access tokens for both APIs are needed and should be pasted in the respective variables in the beginning of the script:
    - `github_api_token` for the GitHub API token
    - `debricked_access_token` for the Debricked API token

Information on how to get token can be found under: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api#authenticating, resp.: https://debricked.com/docs/integrations/api.html#authenticate. For getting an access key, both platforms require users to create a free account

2. The repositories to analyse need to be defined in the `repos` array. The identifier can be retrieved from a GitHub repository page (owner, repository name). The `dependency_files` Array needs to contain the path/ file name to the repository's dependency file(s). The regular file name is enough when the dependency file, e.g., 'package-lock.json', is in the base level of the repository.
The dependency files are needed for the Debricked part of the analysis. Which languages and files are supported can be seen here: https://debricked.com/docs/language-support/. Note that a repository can have mutliple dependency files, therefore multiple can be defined.

3. Run the script from top to bottom, all required packages will be installed in the first code block

4. In the first run, all fetched data will be stored in .pkl files. Next time the visualization parts can make use of the saved data in order to not over and over fetch the same data. If new data should be fetched explicitly, set the `overwrite_existing_data` flag to true in both data getter methods or delete the backup data files from their original location.
