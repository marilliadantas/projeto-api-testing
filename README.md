# **Testes automatizados de API REST com Postman** 👨‍🚀🚀

Este projeto tem como finalidade mostrar a automação de testes de API REST <br> utilizando a ferramenta Postman.

## **O que são as requisições HTTP, na prática?** 💻

- Na prática, as requisições HTTP são chamadas feitas pelo cliente ao servidor <br> e que, dependendo do método, esperam uma resposta.
  <br>
  <br>

  ![Referência card métodos](/img/card-metodos.png)

## **API utilizada:**

- Para a realização do teste, utilizei além da ferramenta [Postman](https://www.postman.com/), a fake API [JSONPlaceholder](https://jsonplaceholder.typicode.com/).

- Essa API possui os seguintes endpoints:
  <br>
  <br>
  ![Referência endpoints](/img/endpoints.png)

## **Organizando as requisições no Postman:** 📚

Para organizar as minhas requisições, segui o seguinte "breadcrumb": **Workspace** > **Coleção** > **Requisição**.
<br>

- Inicialmente, criei o **Workspace** "API Testing - JSONPlaceholder" e em seguida, as **coleções** referentes à cada endpoint da API:
  <br>
  <br>
  ![Referência workspace](/img/workspace.png)
  <br>
  <br>
- E por fim, criei a **requisição** dentro da coleção referente ao endpoint que quero fazer a chamada.
  <br>
  <br>
  ![Referência colecoes](/img/colecoes.png)

## **Criando uma variável de ambiente:**

- As variáveis de ambiente evitam repetição e re-trabalho nos testes e também tornam a visualização menos complexa.

- Criei o ambiente que comportará todas as variáveis criadas, seguindo o seguinte passo a passo:
  <br>
  <br>
  ![Referência variável de ambiente](/img/variavel%20de%20ambiente.gif)
  <br>
  <br>

## **Criando as primeiras requisições no Postman:** 👨‍🚀

Neste tópico, realizei as requisições mais comuns no endpoint /posts e analisei as suas respostas.

## **GET em /posts**

- Para realizar a requisição **GET** em /posts, inseri o link da API com o endpoint /posts e selecionei o método **GET**.
  <br>
  <br>
  ![Referência método get](/img/get.gif)
  <br>
  <br>
- Nesta requisição, conseguimos verificar que o **GET** em /posts retorna uma estrutura com várias publicações, tais publicações contém em suas respectivas estruturas os seguintes atributos:

  ![Referência método get](/img/get.gif)
  <br>
  <br>

## **POST em /posts**

- Para realizar a requisição **POST** em /posts, inseri o link da API com o endpoint /posts e selecionei o método POST e passei o corpo da requisição.

- Observação: Não foi preciso passar o "id" da publicação, pois a API assimila a nova publicação ao próximo "id" não cadastrado. Mas há a possibilidade de passar qualquer "id" no corpo da requisição, desde que o mesmo já não tenha sido assimilado anteriormente.
  <br>
  <br>
  ![Referência método post](/img/post.gif)
  <br>
  <br>
- Nesta requisição, é possível verificar os dados da publicação que foram passados na requisição e o "id" da publicação que foi assimilado pela API.

## **GET em /posts/{id}**

- O **GET** em /posts/{id} retorna **somente** os dados da publicação referente ao id passado no endpoint.
  <br>
  <br>
  ![Referência método get id](/img/id1.gif)
  <br>
  <br>
- Nesta requisição, é possível notar que no corpo da resposta, temos apenas a estrutura da publicação referente ao id que foi passado.

## **PUT em /posts/{id}**

- O **PUT** no endpoint /posts/{id}, foi passado no corpo da request todos os dados que farão o "update" do id referido. Esses dados irão sobrepor o que existe atualmente no endpoint.
  <br>
  <br>
  ![Referência método put](/img/put.gif)
  <br>
  <br>
- Nesta requisição, é possível conferir a diferença do conteúdo do endpoint /posts/1 antes e depois do **PUT**.

- Neste exemplo, nota-se que o corpo da resposta é preenchido somente com os dados passados do corpo da requisição do método **PUT**.

**Antes**

    {
    "userId": 1, <br>
    "id": 1,<br>
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
    }

<br>

**Depois**

    {
    "title": "Meu novo título",<br>
    "id": 1
    }

## **PATCH em /posts/{id}**

- O **PATCH** em /posts/{id}, foi passado no corpo somente os campos que serão alterados na estrutura do id referido. Os dados irão sobrepor **somente** os campos que foram passados no corpo da requisição, diferente do método **PUT**.
  <br>
  <br>
  ![Referência método patch](/img/patch.gif)
  <br>
  <br>
- Levando em consideração o exemplo da requisição **GET** /posts/1, é possível notar a diferença do conteúdo do endpoint /posts/1 antes e depois do **PATCH:** Onde somente o "title" foi passado no corpo da requisição, somente ele foi alterado na estrutura.

**Antes**

    {
      "userId": 1,
      "id": 1,
      "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
      "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
    }

<br>

**Depois**

    {
      "userId": 1,
      "id": 1,
      "title": "Meu novo título",
      "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
    }

## **DELETE em /posts/{id}**

- O método **DELETE** foi selecionado no Postman, foi passado o parâmetro do "id" desejado no endpoint e o corpo da resposta ficou vazio.
  <br>
  <br>
  ![Referência método delete](/img/delete.gif)
  <br>
  <br>
- Para confirmar a deleção, foi verificado o status da requisição que tinha que ser 200 e em seguida que não há corpo de resposta.
  <br>
  <br>

## **Testes de validação de status code** ✅

- Utilizando o **GET** em /posts, para a automatização de testes de validação, foi utilizado a seguinte sintaxe:

  pm.test("nome do teste", function () {
  pm.response.to.have.status(200);
  });

- Note que, tendo um status que valida o status code, se ele for igual o esperado o resultado é positivo para o teste.

<br>

## **Testes de resposta da requisição** ✅

- Os testes do response body, validam todo o conteúdo que é recebido no corpo da resposta, com a utilização de diversos "asserts" que são contemplados pela "Chai Assertion Library".
  <br>
  <br>

// Teste de resposta em texto do status code<br>

    pm.test("status code é 200", function(){
      pm.response.to.have.status(200);
    });

<br>
// Teste de tempo de resposta.

    pm.test("O tempo de resposta é menor que 150ms", ( ) => {
      pm.expect(pm.response.responseTime). to.be.below(150);
    });

<br>

// Validações do corpo da resposta
<br>

    pm.test("O response da requisição foi validado.", ( ) => {

    // Criação da constante para fazer o parse do JSON <br>

      const respostaDoJson = pm.response.json();

    // Teste que valida o o conteúdo de uma variável

    pm.expect(respostaDoJson.userId).to.eql(1);

    // Teste que valida o tipo de uma variável

    pm.expect(respostaDoJson.userId).to.be.a("number");
    pm.expect(respostaDoJson.id).to.eql(1);
    pm.expect(respostaDoJson.id).to.be.a("number");
    pm.expect(respostaDoJson.title).to.be.a("string");
    pm.expect(respostaDoJson.title).to.eql("sunt aut facere repellat provident occaecati excepturi optio reprehenderit");

<br>

// Teste que valida a quantidade de caracteres no conteúdo de uma variável. <br>

    pm.expect(responseDoJson.title).to.have.lengthOf(74);
    });

- Aqui está o resultado dos testes utilizando o método GET no endpoint /posts/1 da API utilizada:
  <br>
  <br>
  ![Referência status code](/img/testes.gif)
  <br>
  <br>
