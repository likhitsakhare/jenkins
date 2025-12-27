sh '''
cd backend
mvn clean verify -DskipTests org.sonarsource.scanner.maven:sonar-maven-plugin:3.10.0.2594:sonar -Dsonar.projectKey=studentappJenkins -Dsonar.projectName=studentappJenkins
'''