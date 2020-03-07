node{
    stage('source code managment'){
        git credentialsId: 'GITCredential', url: 'https://github.com/RSI1982/netcore-boilerplate.git'
    }
    stage('project Build'){
        sh label: '', script: 'dotnet build -o ${WORKSPACE}/target/ HappyCode.NetCoreBoilerplate.sln'
    }
    stage('sonarqube scanner'){
        sh label: '', script: '''dotnet sonarscanner begin /k:"netcore-boilerplate" /d:sonar.host.url="http://40.115.40.190" /d:sonar.login="fca6be3e22eb502b07f9c61f9d9a48114ccec284"
        dotnet build -o ${WORKSPACE}/target/ HappyCode.NetCoreBoilerplate.sln
        dotnet sonarscanner end /d:sonar.login="fca6be3e22eb502b07f9c61f9d9a48114ccec284"'''
    }
    stage('Nexusartifactory store'){
        sh label: '', script: '''cd ${WORKSPACE}/target/
        zip -r netcoreboilerplate.zip .
        curl -v -u admin:admin123 --upload-file netcoreboilerplate.zip http://52.166.192.86:8081/repository/netcore-boilerplate/${BUILD_NUMBER}'''
    }
    stage('Mail Notification to user'){
        mail bcc: '', body: '''Hi Team,
        Please find the build state of project and take necessary action according to that''', cc: '', from: '', replyTo: '', subject: 'Build Status of Projects ', to: 'err.rakeshsingh@gmail.com'
    }
}
