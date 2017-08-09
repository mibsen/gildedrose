node {
   stage('Preparation') {
        git credentialsId: 'ubuntu', url: 'git@github.com:mibsen/gildedrose.git'
   }
   
   stage('parallel'){
        parallel(
            'Build' : {
                sh "mvn clean package"  
       },
       'Javadoc' : {
            sh "mvn site"
            archive 'target/site/*'  
       }
    )
   }
       
   stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
   }
}
