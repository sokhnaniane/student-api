stage('Build') {
            steps {
                bat '''
                set JAVA_HOME=C:\\Progra~1\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra~1\\Apache\\apache-maven-3.9.16
                "C:\\Program Files\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" clean package -DskipTests
                '''
            }
        }
        stage('Lint') {
            steps {
                bat '''
                set JAVA_HOME=C:\\Progra~1\\Eclipse Adoptium\\jdk-25.0.3.9
                set MAVEN_HOME=C:\\Progra~1\\Apache\\apache-maven-3.9.16
                "C:\\Program Files\\Apache\\apache-maven-3.9.16\\bin\\mvn.cmd" checkstyle:check
                '''
            }
        }
        stage('Tests Unitaires') {
// ... le reste du fichier reste identique
