pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Récupération du code depuis Git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Compilation de l'application sans lancer les tests
                bat 'mvn clean compile -DskipTests'
            }
        }

        stage('Lint') {
            steps {
                // Étape demandée à l'exercice 6.1
                bat 'mvn checkstyle:check'
            }
        }

        stage('Tests Unitaires') {
            steps {
                // Exécution des tests unitaires
                bat 'mvn test'
            }
        }

        stage('Couverture') {
            steps {
                // Génération du rapport de couverture (ex: Jacoco)
                bat 'mvn jacoco:report'
            }
        }

        stage('Archivage') {
            steps {
                // Archivage du fichier JAR généré
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }
}