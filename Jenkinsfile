pipeline {
    agent {
        docker {
            image 'maven:3.9.2'
            args '-u root'
        }
    }
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'testing', description: 'Nombre de la rama a compilar')
    }
    environment {
        PROJECT_DIR = "simple-java-maven-app"
    }
    stages {
        stage('Cleanup') {
            steps {
                script {
                    if (fileExists(PROJECT_DIR)) {
                        echo "📂 Proyecto existente. Eliminando..."
                        sh "rm -rf ${PROJECT_DIR}"
                    }
                }
            }
        }
        stage('Checkout') {
            steps {
                script {
                    echo "🛠 Clonando la rama ${params.BRANCH_NAME}..."
                    sh "git clone --branch ${params.BRANCH_NAME} https://github.com/Ricardo965/simple-java-maven-app.git"
                }
            }
        }
        stage('Build') {
            steps {
                dir(PROJECT_DIR) {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test') {
            steps {
                dir(PROJECT_DIR) {
                    sh 'mvn test'
                }
            }
        }
    }
}
