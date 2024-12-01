
# **Monitoramento de Aplicação Flask com Grafana, Prometheus e Jenkins**

Este projeto configura um ambiente monitorado para uma aplicação Flask utilizando ferramentas como Grafana, Prometheus e Jenkins. As instruções abaixo guiam você no processo de configuração, execução e uso das ferramentas integradas.

## **Pré-requisitos**
Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Postman](https://www.postman.com/)
- [Git](https://git-scm.com/)
- [Jenkins](https://www.jenkins.io/) (opcional para pipelines)

---

## **Clonando o Projeto**
1. Clone este repositório:
   ```bash
   git clone https://github.com/GuilhermeGaffuri/devOpsTrabalho.git
   cd devOpsTrabalho
   ```

2. Construa os containers com:
   ```bash
   docker-compose build --no-cache
   ```

3. Inicie os containers em segundo plano:
   ```bash
   docker-compose up -d
   ```

4. Verifique se os containers estão ativos:
   ```bash
   docker ps
   ```
![Capturar](https://github.com/user-attachments/assets/7def12da-a995-498f-817d-75ad63db5d13)

---

## **Serviços Disponíveis**
Após inicializar os containers, os seguintes serviços estarão disponíveis:

| Serviço      | URL                           |
|--------------|-------------------------------|
| **App Flask** | [http://localhost:5000](http://localhost:5000) |
| **Grafana**   | [http://localhost:3000](http://localhost:3000) |
| **MariaDB**   | `http://localhost:3306`       |
| **Prometheus**| [http://localhost:9090](http://localhost:9090) |

---

## **Configuração do Grafana**
1. Acesse o Grafana: [http://localhost:3000](http://localhost:3000)
2. Faça login com as credenciais padrão:
   - Usuário: `admin`
   - Senha: `admin`
    ![Capturar22](https://github.com/user-attachments/assets/5eaa1e7b-4eed-4892-874c-6fd2c2989ff7)



3. Navegue até a página inicial e explore o **Dashboard**, que exibirá os logs da aplicação Flask.
   ![Capturar24](https://github.com/user-attachments/assets/ae31c05b-3b56-4081-938b-4d245def0d7f)


  ![Uploading Capturar22.PNG…]()

### Configuração de Data Source
1. Vá para: **Configuration > Data Sources**.
   ![Capturar26](https://github.com/user-attachments/assets/2ddf08fc-b869-4d09-87f5-6d291a77045c)
3. Data Sources Prometheus configurado.

  ![Capturar27](https://github.com/user-attachments/assets/96a7f3aa-390b-4a70-a7ea-3072ace2a303)


---

## **Utilizando a Aplicação Flask**
1. Acesse a aplicação em: [http://localhost:5000](http://localhost:5000)
2. Clique em "Login" no canto superior direito.

   ![Login](https://raw.githubusercontent.com/GuilhermeGaffuri/devOpsTrabalho/main/assets/login.png)

3. Credenciais de login:
   - Usuário: `admin`
   - Senha: `admin`
   
![CapturarF3](https://github.com/user-attachments/assets/b117c745-1cea-476b-bcd2-41344141896f)

### Cadastro de Alunos
#### Método 1: Interface Web
1. Após o login, acesse: [http://localhost:5000/alunomodelview/list/](http://localhost:5000/alunomodelview/list/)
   ![CapturarF1](https://github.com/user-attachments/assets/3b42bb48-0d74-4dcd-8c45-2114fe906a55)

3. Utilize a interface para cadastrar novos alunos.

#### Método 2: Postman
1. Crie uma requisição POST para: [http://localhost:5000/alunomodelview/](http://localhost:5000/alunomodelview/)
2. Use o seguinte corpo JSON:
   ```json
   {
       "nome": "Teste",
       "sobrenome": "Teste",
       "turma": "Teste",
       "disciplinas": "Teste1, Teste2"
   }
   ```
   ![CapturarF6](https://github.com/user-attachments/assets/18e3e589-cff4-4334-85ad-0e28e400a84f)

3. Atualize a página para ver o novo aluno listado.

   ![CapturarF7](https://github.com/user-attachments/assets/ad2ee6a7-cc2e-4ef3-bbd4-4a6c9d74935a)


---

## **Pipeline de Automação com Jenkins**
### Configuração do Jenkins
1. Inicie o Jenkins:
   ```bash
   sudo systemctl start jenkins
   sudo systemctl enable jenkins
   ```

2. Verifique o status do Jenkins:
   ```bash
   sudo systemctl status jenkins
   ```

3. Configure um pipeline utilizando o arquivo `Jenkinsfile` disponível no repositório.

   ![Jk](https://github.com/user-attachments/assets/2cd31f7d-b082-4981-a7ea-505c42704982)


### Fluxo do Pipeline
O pipeline automatiza a construção e o monitoramento da aplicação, garantindo integração contínua com o ambiente configurado.

---

## **Arquitetura**
O ambiente é composto pelas seguintes ferramentas e funcionalidades:
- **Flask**: API e interface para interação com alunos.
- **Grafana**: Monitoramento de métricas e logs.
- **Prometheus**: Coleta de métricas.
- **MariaDB**: Banco de dados para persistência.
- **Jenkins**: Automação de CI/CD.

---

## **Referências**
- Documentação oficial:
  - [Docker](https://docs.docker.com/)
  - [Grafana](https://grafana.com/docs/)
  - [Prometheus](https://prometheus.io/docs/)
  - [Jenkins](https://www.jenkins.io/doc/)
- Repositório oficial: [https://github.com/GuilhermeGaffuri/devOpsTrabalho](https://github.com/GuilhermeGaffuri/devOpsTrabalho)

---

Esse README foi estruturado para facilitar a leitura e o entendimento de quem for utilizar ou contribuir para o projeto.
