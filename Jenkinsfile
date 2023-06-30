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
                // Passo 4: Implantação do blog no GitHub Pages
                sh 'peaceiris/actions-gh-pages@v3'
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
