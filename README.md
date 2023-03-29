# Desafio Atados

Fala, pessoal do Atados! 

Para resolver esse desafio eu separei o código em duas branchs. Uma contém um modo mais simples de armazenamento dos dados recebidos através das requisições. Nessa branch, os valores são salvos na memória em listas. No segundo caso, na outra branch, os valores estão sendo salvos num banco de dados PostgreSQL. Cada vez que a API recebe uma requisição POST nós salvamos no banco que estará rodando num container docker. Para cada requisição GET nós coletamos do banco os dados e devolvemos.

## Modo simples:

O modo simples pode ser rodado na branch main a partir do docker no repositório com o comando `docker build -t atadosapi .` e na sequência `docker run -dp 5000:5000 --name atadosapi atados api`. Isso irá criar uma imagem docker e por fim iniciar um container que conterá a imagem da API rodando.

Para requisições eu criei uma pequena collection no Postman com apenas 4 requisições (2 GET e 2 POST). 

https://api.postman.com/collections/25338713-43954dda-38e4-4e63-837a-459492b4ec6f?access_key=PMAT-01GWNSNFMZWGMRYJZJ6T00G74Q

Caso não consigam acessar, a uri para a requisição é a `localhost:5000` e os endpoints 

- POST /api/v1/newvolunteer - adiciona um novo voluntário
- POST /api/v1/newsocialcause - adiciona uma nova ação social
- GET /api/v1/volunteers - retorna os voluntários
- GET /api/v1/socialcauses - retorna as ações sociais

#### Testes unitários:

Foram feitos 4 testes, um para cada endpoint. Os testes estão no arquivo `test_app.py` e podem rodar apenas com o comando `python test_app.py`.

## Modo Completo:

Tentei fazer esse modo com o docker-compose. Infelizmente ao rodar a API e o Banco de Dados, tive problemas de conexão ao tentar criar as tabelas. A única solução que encontrei foi a de rodar o banco de dados em um container e rodar manualmente a API. Dessa forma, basta-se usar o comando `docker-compose up -d` para iniciar o banco de dados (esse comando vai cirar uma API também, mas ela vai exitar quando não conseguir criar as tabelas). Na sequência, pode-se iniciar a API com o comando `python app.py`. A partir desse momento será possível enviar requisições para a API adicionando e coletando as informações de volta do PostgreSQL. 

Alguns resultados que obtive aqui:

- Enviando uma requisição de novo voluntário e nova ação social:

![image](https://user-images.githubusercontent.com/56874672/228428180-8057bcc2-1709-415f-8ad7-e7abbdabfe5a.png)

![image](https://user-images.githubusercontent.com/56874672/228428184-a99dcb33-349f-42f6-af7a-c3c5d0e7bd0e.png)


- Requisitando a informação do banco:

![image](https://user-images.githubusercontent.com/56874672/228428113-e21f5e24-7852-47d2-8554-fe0c9d6cfe7b.png)

![image](https://user-images.githubusercontent.com/56874672/228428124-72ae7756-fc5b-4195-adb1-feb091ca5ea3.png)

### No banco de dados:

- Tabela volunteer_db:

![image](https://user-images.githubusercontent.com/56874672/228428441-2275b180-94ff-4057-9bf9-a77fa1bfb63b.png)

- Tabela social_cause_db:

![image](https://user-images.githubusercontent.com/56874672/228428463-4a4c2b16-a7bd-4e39-bce6-ed965475ef14.png)





