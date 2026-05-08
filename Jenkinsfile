pipeline{
  agent any

  stages{

    stage('Build'){
     steps{
      bat 'gradlew.bat clean build'
     }
    }

    stage('Stop Old Application'){
      steps{
        bat '''
                        for /f "tokens=5" %%a in ('netstat -aon ^| findstr :8081') do (
                            if NOT "%%a"=="0" (
                                taskkill /F /PID %%a
                            )
                        )
                        exit /b 0
                        '''
      }
    }

    stage('Deploy Application'){
      steps{
        bat '''
         java -jar build\\libs\\SpringBootAppDeployment-0.0.1-SNAPSHOT.jar
        '''
      }
    }

  }

}