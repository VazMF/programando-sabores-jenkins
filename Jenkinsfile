pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Passo 1: Checkout do repositório Git
                git 'https://github.com/VazMF/programando-sabores-jenkins'
            }
        }

        stage('Setup Hugo') {
            steps {
                // Passo 2: Configurar o Hugo
                sh 'peaceiris/actions-hugo@v2'
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
                sh 'https://github.com/VazMF/programando-sabores-jenkins'
                sh 'cp -R pasta-do-seu-blog/* seu-repositorio/'
                dir('seu-repositorio') {
                    sh 'git add .'
                    sh 'git commit -m "Atualizando blog"'
                    sh 'git push origin master'
                }
            }
        }

        stage('Notification') {
            steps {
                // Passo 5: Notificação por e-mail
                emailext body: 'A pipeline do blog foi concluída com sucesso!',
                    subject: 'Notificação de Pipeline - Programando Sabores',
                    to: 'vazfernandam@gmail.com'
            }
        }
    }
}
