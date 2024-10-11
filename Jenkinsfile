pipeline {
    agent any

    stages {
        stage('Fetch Secrets') {
            steps {
                script {
                    env.RDS_URL = credentials['RDS_URL']
                    env.RDS_USERNAME = credentials['RDS_USERNAME']
                    env.RDS_PASSWORD = credentials['RDS_PASSWORD']
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    // Spring Boot 빌드
                    sh './gradlew build'
                }
            }
        }
        stage('Upload to S3') {
            steps {
                script {
                    // 빌드된 Jar 파일을 S3로 업로드
                    sh 'aws s3 cp build/libs/step18_empApp-0.0.1-SNAPSHOT.jar s3://ce09-bucket-02/'
                }
            }
        }
    }
}
