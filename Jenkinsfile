pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Build # ${env.BUILD_NUMBER} | Branche : ${env.BRANCH_NAME}"
            }
        }
        stage('Build') {
            steps {
                // Utilisation de Progra~1 pour éviter le bug d'espace Windows
                bat '''
                set JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Program Files\\Apache\\apache-maven-3.9.16
                "C:\\Progra\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" clean package -DskipTests
                '''
            } 
        }
        stage('Lint') {
            steps {
                bat '''
                set JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra Files\\Apache\\apache-maven-3.9.16
                "C:\\Program\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" checkstyle:check
                '''
            }
        }
        stage('Tests Unitaires') {
            steps {
                bat '''
                set JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra Files\\Apache\\apache-maven-3.9.16
                "C:\\Program\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" test
                '''
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Couverture') {
            steps {
                bat '''
                set JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Program Files\\Apache\\apache-maven-3.9.16
                "C:\\Program\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" verify
                '''
            }
            post {
                always {
                    jacoco(
                        execPattern: 'target/*.exec',
                        classPattern: 'target/classes',
                        sourcePattern: 'src/main/java'
                    )
                }
            }
        }
        stage('Archivage') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    post {
        success { echo 'Pipeline reussi avec succes !' }
        failure { echo 'Pipeline echoue -- consultez les logs.' }
    }
}
