pipeline {
    agent any
    
    environment {
        // Variáveis de ambiente que podem ser úteis no processo
        VENV_DIR = 'venv'  // Diretório do ambiente virtual
        DEPLOY_SERVER = 'your-server.com' // Substitua pelo seu servidor de deploy
        DEPLOY_PATH = '/var/www/your-app' // Caminho no servidor de deploy
    }

    stages {
        // Etapa para realizar o checkout do repositório
        stage('Checkout') {
            steps {
                script {
                    // Faz o clone do repositório e seleciona a branch correta
                    git branch: 'main', url: 'https://github.com/GuilhermeGaffuri/devOpsTrabalho.git'
                }
            }
        }
        
        // Etapa para instalar as dependências do projeto
        stage('Install Dependencies') {
            steps {
                script {
                    // Cria o ambiente virtual Python
                    sh 'python3 -m venv $VENV_DIR'
                    // Ativa o ambiente virtual
                    sh '. $VENV_DIR/bin/activate'
                    // Instala as dependências do Flask (ou outras dependendo do seu projeto)
                    sh 'pip install -r flask/requirements.txt'
                }
            }
        }

        // Etapa para executar os testes do projeto
        stage('Run Tests') {
            steps {
                script {
                    // Executa os testes (aqui usando pytest, mas adapte conforme necessário)
                    sh 'source $VENV_DIR/bin/activate && pytest'
                }
            }
        }

        // Etapa de Build (compilação ou preparação do projeto)
        stage('Build') {
            steps {
                script {
                    // Executa comandos de build necessários, por exemplo:
                    // Para um projeto Flask:
                    sh 'source $VENV_DIR/bin/activate && python setup.py install'
                    // Outro exemplo de build, se for um arquivo compilado:
                    // sh 'source $VENV_DIR/bin/activate && python manage.py build'
                }
            }
        }

        // Etapa de Deploy
        stage('Deploy') {
            steps {
                script {
                    // Exemplo de deploy para um servidor remoto utilizando SCP (Secure Copy Protocol)
                    // Copia os arquivos para o servidor
                    sh 'scp -r * $DEPLOY_SERVER:$DEPLOY_PATH'
                    
                    // Exemplo de reiniciar o serviço no servidor (ajuste conforme sua necessidade)
                    // Neste caso, estamos reiniciando um servidor Flask usando systemctl
                    sh 'ssh $DEPLOY_SERVER "sudo systemctl restart flask-app"'
                }
            }
        }
    }

    post {
        always {
            // Limpa o workspace após o término do pipeline
            cleanWs()
        }
        success {
            // Notifica que o pipeline foi bem-sucedido
            echo 'Deploy concluído com sucesso!'
        }
        failure {
            // Notifica que algo deu errado no pipeline
            echo 'Falha no pipeline. Verifique os logs!'
        }
    }
}
