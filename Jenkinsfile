pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // 빌드 단계에서 환경 변수를 이용하여 빌드 수행
                    sh "./gradlew build -Drds.url=${env.RDS_URL} -Drds.username=${env.RDS_USERNAME} -Drds.password=${env.RDS_PASSWORD}"
                }
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    // AWS 자격 증명을 불러와 S3 업로드에 사용
                    withCredentials([string(credentialsId: 'aws-access-key-id', variable: 'AWS_ACCESS_KEY_ID'),
                                     string(credentialsId: 'aws-secret-access-key', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                        // 빌드된 Jar 파일을 S3로 업로드
                        sh 'aws s3 cp build/libs/step18_empApp-0.0.1-SNAPSHOT.jar s3://ce09-bucket-02/'
                    }
                }
            }
        }
    }
}
