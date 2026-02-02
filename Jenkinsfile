pipeline {
    agent any
    
    environment {
        // Invocamos la credencial que creamos en el paso 1.3
        AWS_ACCESS_KEY_ID     = credentials('aws-credentials')
        AWS_SECRET_ACCESS_KEY = credentials('aws-credentials')
    }

    stages {
        stage('Install AWS CLI') {
            steps {
                sh '''
                curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
                unzip -o awscliv2.zip
                ./aws/install --install-dir /tmp/aws-cli/ --bin-dir /tmp/aws-cli/bin --update
                '''
            }
        }

        stage('Push files') {
            steps {
                // Aquí usamos la ruta donde se instaló el CLI arriba (/tmp/aws-cli/bin/aws)
                // Modifica el nombre del bucket si es necesario
                sh '/tmp/aws-cli/bin/aws s3 cp index.html s3://efm1-erika-masterd/'
            }
        }
    }
}

