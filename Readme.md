# SonarQube
SonarQube is a Code Quality Assurance tool that collects and analyzes source code, and provides reports for the code quality of your project. 

It combines static and dynamic analysis tools and enables quality to be measured continually over time. Everything from minor styling choices, to design errors are inspected and evaluated by SonarQube. This provides users with a rich searchable history of the code to analyze where the code is messing up and determine whether or not it is styling issues, code defeats, code duplication, lack of test coverage, or excessively complex code. The software will analyze source code from different aspects and drills down the code layer by layer, moving module level down to the class level, with each level producing metric values and statistics that should reveal problematic areas in the source code that needs improvement.

SonarQube also ensures code reliability, Application security, and reduces technical debt by making your code base clean and maintainable. SonarQube also provides support for 29 different languages, including C, C++, Java, JavaScript, PHP, GO, Python, and much more. SonarQube also provides Ci/CD integration, and gives feedback during code review with branch analysis and pull request decoration.

## SonarQube Benefits

### Why SonarQube?
Why not just existing and proven tools and configure them in the CI server ourselves? Well for SonarQube there are a lot of benefits:

- CI tools lack a unified plugin for seamless integration of various tools.

- They don't offer plugins with advanced drill-down features comparable to SonarQube.

- CI Plugins does not talk about overall compliance value

- CI plugins do not provide managerial perspective

- No CI plugin addresses design or architectural issues.

- CI plugins do not provide a dashboard for overall project quality

### Features of SonarQube

- Doesn’t just show you what’s wrong, but also offers quality and management tools to actively helps you correct issues

- Focuses on more than just bugs and complexity and offers more features to help the programmers write code, such as coding rules, test coverage, de-duplications, API documentation, and code complexity all within a dashboard

- Gives a moment-in-time snapshot of your code quality today, as well as trends of past and potentially future quality indicators. Also provides metrics to help you make the right decisions

## Getting Started

SonarQube comes in different versions to suit your development needs:

1. Community edition: It's the starting point for integrating code quality into your CI/CD process.

2. Developer Edition: Offers maximum application security and value, especially across different branches and pull requests (PRs).

3. Enterprise Edition: Ideal for managing your application portfolio and implementing code quality and security at an enterprise level.

4. Data Center Edition: Provides high availability for global deployments.

To analyze a project locally, you can install SonarQube using either a zip file, or a Docker image.

#### Getting SonarQube from a Zip file

You can download the SonarQube community edition zip file from here:[Download | SonarQube](https://www.sonarsource.com/products/sonarqube/downloads/)

Please refer the document installation.md for full installation 

#### Getting SonarQube from Docker Image

- Find the community version of SonarQube that you want to use on Docker Hub:[SonarQube - Official Image | Docker Hub](https://hub.docker.com/_/sonarqube/)
- Start the server by running:
 '''bash
docker run -d --name sonarqube -p 9000:9000 <image name>
'''
- Login to http://localhost:9000 with the following credentials for system admin: (admin/admin)

