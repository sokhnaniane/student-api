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
                bat '''
                set JAVA_HOME=C:\\Progra~1\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra~1\\Apache\\apache-maven-3.9.16
                "C:\\Progra~1\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" clean package -DskipTests
                '''
            }
        }

        // Stage Lint désactivé
        /*
        stage('Lint') {
            steps {
                bat '"%MAVEN_HOME%\\bin\\mvn.cmd" checkstyle:check'
            }
        }
        */

        stage('Tests Unitaires') {
            steps {
                bat '''
                set JAVA_HOME=C:\\Progra~1\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra~1\\Apache\\apache-maven-3.9.16
                "C:\\Progra~1\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" test
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
                set JAVA_HOME=C:\\Progra~1\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra~1\\Apache\\apache-maven-3.9.16
                "C:\\Progra~1\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" verify
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
        success {
            echo 'Pipeline reussi avec succes !'
        }

        failure {
            echo 'Pipeline echoue -- consultez les logs.'
        }
    }
