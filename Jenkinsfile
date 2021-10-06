pipeline {
    agent any
    tools {
        /**
        Aqui se agregan los tools a utilizar, estos se configuran en el GlobalToolConfigutration de Jenkins y se "llaman" por medio de su label
        */
        maven 'maven-3.6.3'
        /**
        DOCUMENTACION DE OPEN JDK
        https://plugins.jenkins.io/adoptopenjdk/
        https://www.py4u.net/discuss/581429
        */
        jdk 'openjdk-14'
    }
    stages {
        stage('Construccion') {
            /**
            DOCUMENTACION DE TOOLS POR STAGE
            https://stackoverflow.com/questions/47895668/how-to-select-multiple-jdk-version-in-declarative-pipeline-jenkins
            https://newbedev.com/java-how-to-make-jenkins-pipeline-choose-specific-java-version-code-example
            */
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/jglick/simple-maven-project-with-tests.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"
                //echo 'Hello'

                    //withMaven(maven: '')
                    sh 'mvn clean package -DskipTests -B -ntp'
            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
            stage('Despliegue') {
            /**
            DOCUMENTACION DE TOOLS POR STAGE
            https://stackoverflow.com/questions/47895668/how-to-select-multiple-jdk-version-in-declarative-pipeline-jenkins
            https://newbedev.com/java-how-to-make-jenkins-pipeline-choose-specific-java-version-code-example
            */
                steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/jglick/simple-maven-project-with-tests.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"
                echo 'Hello, :3'

                //withMaven(maven: '')
                sh 'ssh ec2-3-144-114-102.us-east-2.compute.amazonaws.com rm -rf /saul/temp_deploy/'

                    /* sh 'ssh ec2-3-144-114-102.us-east-2.compute.amazonaws.com mkdir -p /saul/temp_deploy/' */


                sh 'scp -r target/*.jar ec2-3-144-114-102.us-east-2.compute.amazonaws.com:/home/ubuntu/saul/temp_deploy/'
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
                }
            }
    }
    post {
        // If Maven was able to run the tests, even if some of the test
        // failed, record the test results and archive the jar file.
        success {
                //junit '**/target/surefire-reports/TEST-*.xml'
                //archiveArtifacts 'target/*.jar'
                archiveArtifacts(artifacts: 'target/*.jar', excludes: '**/maven-wrapper.jar')
                emailext(from: 'saul.dios@loquesea.com', body: 'Se contruyó satisfactoriamente', subject: 'EXITO!', to: 'saul.avila.dev@outlook.com', attachmentsPattern: 'target/*.jar.original')
                echo 'Success'
        }
    }
}

