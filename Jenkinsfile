pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Passo 1: Checkout do repositório Git
                git branch: 'master', credentialsId: 'hugo-blog', url: 'git@github.com:VazMF/programando-sabores-jenkins.git'
            }
        }

        stage('Build') {
            steps {
                // Passo 3: Executar o build do blog com o Hugo
                sh 'hugo --minify'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([
            sshUserPrivateKey(credentialsId: 'hugo-blog', keyFileVariable: 'SSH_KEY')
        ]) {
                    sh 'git push origin master'
        }
            }
        }
    }
    post {
        always {
            mail to: 'maria.romero@edu.unifil.br',
            subject: 'Notificação de Pipeline - Programando Sabores',
            body: 'A pipeline do blog foi concluída com sucesso!'
        }
    }
}
