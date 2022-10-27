node {
    stage 'Build, Test and Package'
    git 'https://github.com/Saurav-infostride/JmeterPractise.git'
  
    dir('jmeter') {
        sh "./mvnw clean install -DskipTests"
        sh 'nohup ./mvnw spring-boot:run -Dserver.port=8989 &'
        sh "while ! httping -qc1
          http://localhost:8081 ; do sleep 1 ; done"
                
        sh "jmeter -j jmeter.save.saveservice.output_format=xml
          -n -t TestingMultipleGetRequests.jmx 
            -l reports\jenkins.io.report.jtl"
        step([$class: 'ArtifactArchiver', artifacts: 'JMeter.jtl'])
        sh "pid=\$(lsof -i:8989 -t); kill -TERM \$pid || kill -KILL \$pid"
    }
}
