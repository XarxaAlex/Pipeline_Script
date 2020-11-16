pipeline {
   //agent none
	agent any
	parameters {
	  string (name: 'REPOSITORIO', defaultValue: '', description: '')
	}
	stages { 
		stage('Git') {
			steps {
				echo 'Obteniendo Git'
				git "${params.GIT_URL}"
			}
		}
		stage('Maven y package'){
			tools{
			  maven 'LocalMaven'
			  jdk 'LocalJDK'
			}
			steps {
				echo 'Ejecutando Maven PMD CHECKSTYLE Y FINDBUGS. Paquetizando'
				bat 'mvn clean pmd:pmd checkstyle:checkstyle findbugs:findbugs package'
			}

		}
		stage('Despliegue Tomcat'){
			steps {
				echo 'Ejecutando despliegue Tomcat'
				//copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: '060-copy-artifact'
				//deploy adapters: [tomcat8(credentialsId: 'f393c254-f0ea-4063-899b-957a6d24a1cd', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '.\\webapp\\target\\webapp.war'
			}

		}
	}
}



