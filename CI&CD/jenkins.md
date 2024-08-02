# Jenkins CI/CD Documentation

Jenkins is an open-source automation server that enables developers to build, test, and deploy applications continuously. This documentation outlines the steps to set up Jenkins for Continuous Integration (CI) and Continuous Deployment (CD) in your projects.

## Prerequisites

1. **Jenkins Installed:** Make sure you have Jenkins installed on your server. You can download it from [Jenkins official site](https://www.jenkins.io/download/).
2. **Java Installed:** Jenkins requires Java LTS to run. Ensure Java is installed on your system [JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html).
3. **Source Code Repository:** Ensure your source code is stored in a version control system like Git.

## Jenkins Configuration

### 1. Install Jenkins

- Download and install Jenkins following the instructions provided for your operating system.
- **_You can use it in a portable way by downloading jenkins.war. This way you can run it with: `java -jar jenkins.war`_**
- Start Jenkins and access the web interface at `http://localhost:8080` (or the port you configured).

### 2. Configure Jenkins

1. **Unlock Jenkins:**
   - Retrieve the initial admin password from the Jenkins log file or the path provided during installation.
   - Enter the password in the Jenkins web interface to unlock it.

2. **Install Suggested Plugins:**
   - After unlocking, Jenkins will prompt you to install plugins. Choose "Install suggested plugins" for a default setup.

3. **Create Admin User:**
   - Set up an admin user account and complete the initial setup.

### 3. Configure Jenkins for CI/CD

#### Creating a New Job

1. **Create a New Item:**
   - Click on "New Item" on the Jenkins dashboard.
   - Enter a name for the job, select "Freestyle project" or "Pipeline" depending on your needs, and click "OK."

2. **Configure Source Code Management:**
   - In the job configuration, under "Source Code Management," select "Git" (or your preferred SCM).
   - Enter the repository URL and credentials if needed.

3. **Add Build Steps:**
   - Under "Build," add the necessary build steps for your project (e.g., "Invoke Gradle script," "Execute shell").

4. **Add Post-Build Actions:**
   - Configure post-build actions such as "Archive the artifacts" or "Publish JUnit test result report."

#### Setting Up a Pipeline Job

1. **Create a Pipeline Job:**
   - Follow the same steps to create a new item, but select "Pipeline" instead of "Freestyle project."

2. **Define Pipeline Script:**
   - In the job configuration, define your pipeline script. You can use the "Pipeline" section to write a script in Groovy, or load it from a `Jenkinsfile` in your repository.

   Example of a basic pipeline script:
   ```groovy
   pipeline {
       agent any
       stages {
           stage('Build') {
               steps {
                   // Add your build steps here
                   sh 'mvn clean install'
               }
           }
           stage('Test') {
               steps {
                   // Add your test steps here
                   sh 'mvn test'
               }
           }
           stage('Deploy') {
               steps {
                   // Add your deployment steps here
                   sh 'mvn deploy'
               }
           }
       }
   }
   ```

### 4. Configure Jenkins for Continuous Integration

1. **Set Up Webhooks:**
   - Configure webhooks in your source code repository to trigger Jenkins builds on code commits or pull requests.

2. **Schedule Builds:**
   - In the job configuration, under "Build Triggers," you can set up triggers such as "Poll SCM" to schedule builds.

### 5. Configure Jenkins for Continuous Deployment

1. **Add Deployment Steps:**
   - In your pipeline script or job configuration, add steps to deploy your application to the desired environment (e.g., production, staging).

2. **Set Up Deployment Triggers:**
   - Configure deployment triggers such as successful build completions or manual approvals.

### 6. Monitor and Maintain Jenkins

1. **Monitor Build Status:**
   - Use the Jenkins dashboard to monitor build status and view build logs.

2. **Manage Jenkins:**
   - Regularly update Jenkins and installed plugins to ensure security and compatibility.
   - Back up Jenkins configuration and data to prevent data loss.



## Jenkinsfile Example for Pipeline with Microservices

[Complete Jenkinsfile](./Jenkinsfile)

```groovy
pipeline {
    agent any

    environment {
        SONAR_SCANNER_BIN = "/opt/sonar-scanner-6.1.0.4477-linux-x64/bin"
        PATH = "${SONAR_SCANNER_BIN}:${env.PATH}"
        PROJECT_DIR = "/home/neodev/Documents/projects/Enrollment-Management-System-UNSA"

        AUTH_MCSV_DIR = "${PROJECT_DIR}/auth-microservice"
        USERS_MCSV_DIR = "${PROJECT_DIR}/users-microservice"
        COURSES_MCSV_DIR = "${PROJECT_DIR}/courses-microservice"
        ENROLLMENTS_MCSV_DIR = "${PROJECT_DIR}/enrollments-microservice"
        SCHOOLS_MCSV_DIR = "${PROJECT_DIR}/schools-microservice"
        NOTIFICATIONS_MCSV_DIR = "${PROJECT_DIR}/notifications-microservice"
        PAYMENTS_MCSV_DIR = "${PROJECT_DIR}/payments-microservice"
        
        UNIT_TESTING_RESULTS = "${PROJECT_DIR}/reports/unitTests"
        API_TESTING_RESULTS = "${PROJECT_DIR}/reports/apiTests"
        PERFORMANCE_TESTING_RESULTS = "${PROJECT_DIR}/reports/performanceTests"
        SECURITY_TESTING_RESULTS = "${PROJECT_DIR}/reports/securityTests"
    }

    stages {
        stage("Build") { // One sub-stage for each microservice 
            parallel { // Run all sub-stages in parallel
                stage ("Build Auth Microservice") {
                    steps {
                        dir(AUTH_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj" // build command
                        }
                    }
                }
                stage("Build Users Microservice") {
                    steps {
                        dir(USERS_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj"
                        }
                    }
                }
                stage("Build Courses Microservice") {
                    steps {
                        dir(COURSES_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj"
                        }
                    }
                }
                stage("Build Enrollments Microservice") {
                    steps {
                        dir(ENROLLMENTS_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj"
                        }
                    }
                }
                stage ("Build Schools Microservice") {
                    steps {
                        dir(SCHOOLS_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj"
                        }
                    }
                }
                stage("Build Notifications Microservice") {
                    steps {
                        dir(NOTIFICATIONS_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj"
                        }
                    }
                }
                stage("Build Payments Microservice") {
                    steps {
                        dir(PAYMENTS_MCSV_DIR) {
                            sh "dotnet --version"
                            sh "dotnet build src/src.csproj"
                        }
                    }
                }
                stage("Build Frontend") {
                    steps {
                        dir("${PROJECT_DIR}/client") {
                            sh "pwd"
                            // sh "npm install"
                            // sh "npm run build"
                        }
                    }
                }
            }
        }

        // ...
    }
}
```


For more detailed information, refer to the [Jenkins documentation](https://www.jenkins.io/doc/).