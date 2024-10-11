pipeline {
    agent any

    stages {
        stage('Fetch Secrets') {
            steps {
                script {
                    // Secret Text로 RDS_URL, RDS_USERNAME, RDS_PASSWORD 불러오기
                    withCredentials([string(credentialsId: 'RDS_URL', variable: 'RDS_URL'),
                                     string(credentialsId: 'RDS_USERNAME', variable: 'RDS_USERNAME'),
                                     string(credentialsId: 'RDS_PASSWORD', variable: 'RDS_PASSWORD')]) {
                        
                        // 자격 증명 출력 (테스트용, 실제 배포 시 민감 정보 출력하지 않도록 주의)
                        echo "RDS URL: $RDS_URL"
                        echo "RDS Username: $RDS_USERNAME"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // 빌드 단계에서 환경 변수를 이용하여 빌드 수행
                    sh "./gradlew build -Drds.url=$RDS_URL -Drds.username=$RDS_USERNAME -Drds.password=$RDS_PASSWORD"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment Stage'
            }
        }
    }
}
