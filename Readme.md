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

You can download the SonarQube community edition zip file from here: [Download | SonarQube](https://www.sonarsource.com/products/sonarqube/downloads/)

Please refer the document installation.md for full installation 

#### Getting SonarQube from Docker Image

- Find the community version of SonarQube that you want to use on Docker Hub: [SonarQube - Official Image | Docker Hub](https://hub.docker.com/_/sonarqube/)
- Start the server by running:
  ```
  docker run -d --name sonarqube -p 9000:9000 <image name>
  ```
- Login to http://localhost:9000 with the following credentials for system admin: (admin/admin)

#### Analyzing a project with SonarQube

Once you are logged into sonarqube, to analyze a project follow the following steps:

- Click "Create a Local project"

- Provide a Project display name and Project key for your project, then proceed to the next step.

- Choose the baseline for new code in your project.

- Under the "Analysis method," select "Locally."

- Generate a token for your project and proceed by clicking "Continue."

- Specify your project's main language under "Run analysis on your project."

- Select your project’s main language under Run analysis on your project, and follow the instructions to analyze your project. Here you’ll download and execute a Scanner on your code (if you’re using Maven or Gradle, the Scanner is automatically downloaded).

## Tool Walk Through

Once you access SonarQube, the first step involves importing a project. You can either create a project manually within SonarQube or import it directly from various DevOps platforms, including GitHub and Bitbucket, leveraging SonarQube's seamless integration capabilities. After setting up your projects, navigate to the 'Projects' tab, as shown below, to view a high-level overview of the health of each project in your organization.

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/9cb49948-c5bd-4100-80c3-c716098420dd)

1. **Projects** :
   
On this page, you can view a comprehensive list of projects, offering options for creating a new project, along with various filtering capabilities.

For more, please refer [Official Documentation](https://docs.sonarsource.com/sonarqube/latest/project-administration/creating-and-importing-projects/)

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/1782c363-df54-4c1a-aa12-fd58b23c2dff)

2. **Issues** :
   
The "Issues" page provides a detailed overview of code-related problems, also known as issues or violations, within your software projects. These issues can include code smells, bugs, security vulnerabilities, and other areas where the code might not adhere to best practices or coding standards.

For more, please refer [Official Documentation](https://docs.sonarsource.com/sonarqube/latest/user-guide/issues/#:~:text=Issues-,Overview,issues%20(new%20technical%20debt).)

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/e0b5b9c0-e716-4c38-85e1-2b6ab181dc49)

3. **Rules** :

SonarQube executes rules on source code to generate issues. It has more than 5,000 rules that are regularly updated and enhanced for more than 30 of the most popular and widely used languages and frameworks.

For more, please refer [Official Documenation](https://docs.sonarsource.com/sonarqube/9.8/user-guide/rules/overview/)

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/4dc616ad-9348-452e-8cb1-4041fadfe96e)

4. **Quality Profiles** :
Quality profiles are a key part of your SonarQube configuration. They define the set of rules to be applied during code analysis.

Every project has a quality profile set for each supported language. When a project is analyzed, SonarQube determines which languages are used and uses the active quality profile for each of those languages in that specific project.

For more, please refer [Quality Profiles Documentation](https://docs.sonarsource.com/sonarqube/latest/instance-administration/quality-profiles/)

5. **Quality Gates** :

Quality Gates in SonarQube are a set of predefined criteria or conditions that a project must meet before it can be considered of acceptable quality. These gates serve as a checkpoint during the development and analysis process, ensuring that certain quality standards are met before allowing the project to proceed further.

For more, please refer [Quality Gates Documentation](https://docs.sonarsource.com/sonarqube/latest/user-guide/quality-gates/)

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/e2cbf832-0efd-4831-b3d7-d78064951087)

### Run a sample application on SonarQube for code analysis
**Prerequisites:**
- Java application code hosted on a repository
- Jenkins server

**Environment Setup**

1. Install the necessary plugins
   - Git plugin
   - Maven Integration plugin
   - SonarQube Scanner

2. Create a new Jenkins pipeline:
    - In Jenkins, create a new pipeline job and configure it with the GitHub repository https://github.com/kcheth/Shopping-cart for the Java application.
    - Add a Jenkinsfile to the repository to define the pipeline stages.

3. Define the pipeline stages:
    - Stage 1: Checkout the source code from Git.
    - Stage 2: Build the Java application using Maven.
    - Stage 3: Run SonarQube analysis to check the code quality.

Jenkinsfile stored in GitHub
```
pipeline {
    agent any
    tools{
        jdk 'jdk11'
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: '9f6d6649-facc-4222-acd4-7fadeb51ce05', poll: false, url: 'https://github.com/kcheth/Shopping-cart.git'
            }
        }
        
        stage('COMPILE') {
            steps {
                sh "mvn clean compile -DskipTests=True"
            }
        }
        
        stage('OWASP SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Sonarqube') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh "mvn sonar:sonar"
                }
            }
        }
    }
}
```

Execute the Jenkins pipeline to initiate a comprehensive process outlined in the Jenkinsfile. This process involves retrieving code from the GitHub repository, fetching dependencies specified in the pom.xml file using Maven, creating a package through Maven, and performing a code analysis using SonarQube.

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/7f60e7df-5b6b-4493-8e10-03f48ce2a047)

Verify the SonarQube platform to examine the pipeline results, assessing the code analysis conducted throughout the pipeline execution.

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/1ffb291a-9c8f-4736-9cf0-d3048e5f6f83)

Based on the results presented above, here is a comprehensive analysis of each parameter:

1. #### Bugs (1 Issue):

This category represents code issues that are likely to cause runtime errors or unexpected behavior in your application. Addressing this bug will improve code stability.

2. #### Vulnerabilities (1 Issue): 

Vulnerabilities indicate potential security risks in your code that could be exploited by attackers. It's crucial to fix vulnerabilities to protect your application from security threats.

3. #### Code Smells (8 Issues):

Code smells represent areas of code that may not be technically incorrect but could benefit from improvement. Addressing code smells enhances code readability and maintainability.

4. #### Hotspots Reviewed (0 Issues):

Hotspots are typically complex or critical parts of your codebase. The absence of reviewed hotspots suggests that there may be areas of code that require further attention and analysis.

5. #### Coverage (0%):

Code coverage measures how much of your code is tested. A 0% coverage indicates that none of your code is currently tested. Consider adding tests to improve code quality.

6. #### Duplications (0%):

This result signifies that there were no instances of duplicated code blocks within the scanned codebase.

7. #### Lines of Code (825 Lines):

This metric indicates the total number of lines in your application's source code. Understanding your codebase's size helps in managing and maintaining it effectively.

Upon selecting the project in the image above, you can view an analysis of the entire code in the image below.

![image](https://github.com/kcheth/SonarQube-Guide/assets/106922418/5e188ca2-0257-46e3-a95b-a31398ef12e6)

After SonarQube analysis, if a DevOps engineer identifies errors or the pipeline results show failures, the typical next steps involve addressing and fixing the issues in the code. This may include collaborating with developers to resolve bugs, vulnerabilities, or code smells, and making necessary improvements to meet coding standards. 

Once the issues are addressed, the code can be retested and the pipeline rerun to ensure a successful and clean build. The iterative process continues until the code meets quality standards and can be deployed confidently.

### Conclusion

SonarQube stands as a powerful ally in ensuring code quality, security, and maintainability. From comprehensive static code analysis and issue detection to customizable rules and automated quality gates, SonarQube empowers development teams to foster a culture of continuous improvement. By providing actionable insights and fostering adherence to best practices, SonarQube plays a vital role in elevating the overall software development life-cycle, resulting in more reliable and efficient software projects.



