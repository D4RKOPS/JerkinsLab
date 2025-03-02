pipeline {
    agent any

    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Rama a compilar (ej: declarative, testng)')
    }

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Preparar entorno') {
            steps {
                script {
                    def projectDir = "${WORKSPACE}/simple-java-maven-app"
                    if (fileExists(projectDir)) {
                        echo " El proyecto ya existe. Eliminando carpeta..."
                        sh "rm -rf ${projectDir}"
                    } else {
                        echo "No se encontró carpeta previa, procediendo con la clonación."
                    }
                }
            }
        }

        stage('Clonar código') {
            steps {
                echo "Clonando la rama '${BRANCH}' desde el repositorio..."
                git url: 'https://github.com/jenkins-docs/simple-java-maven-app.git', branch: "${BRANCH}"
            }
        }

        stage('Compilar') {
            steps {
                echo "Iniciando compilación con Maven..."
                sh 'mvn clean package'
            }
        }
    }
}
