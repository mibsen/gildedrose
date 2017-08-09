node {
   stage('Preparation') {
        checkout scm
   }
   
   stage('parallel'){
        parallel(
            'Build' : {
                sh "docker run --rm -i -v $WORKSPACE:/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn clean package"  
       },
       'Javadoc' : {
            sh "docker run --rm -i -v $WORKSPACE:/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn site"
            archive 'target/site/*'  
       }
    )
   }
       
   stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
   }
}
