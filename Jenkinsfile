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
                // Configurar o ambiente do GitHub Pages
                sh 'git config --global user.email "vazfernandam@gmail.com"'
                sh 'git config --global user.name "VazMF"'

                // Copiar os arquivos gerados para o diretório do GitHub Pages
                sh 'cp -R public/* https://github.com/VazMF/programando-sabores-jenkins/'

                // Fazer commit e push para o GitHub Pages
                dir('https://github.com/VazMF/programando-sabores-jenkins') {
                    sh 'git add .'
                    sh 'git commit -m "Atualizando blog"'
                    sh 'git push origin main'
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
