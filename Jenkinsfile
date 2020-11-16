pipeline {
	agent any
	parameters {
	  string (name: 'REPOSITORIO', defaultValue: 'sin valor', description: 'bla bla')
	}
	stages { 
		stage('Git') {
			steps {
				echo "Obteniendo Git => ${params.REPOSITORIO}"
				git "${params.REPOSITORIO}"
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



