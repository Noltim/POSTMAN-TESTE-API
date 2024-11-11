# Sobre o Projeto

Seu início se dá pela pasta Teste, onde está contido o desenvolvimento dos teste, assim como o report em newman, testes em postman arquitetados em JavaScript, provas visuais dos teste em pleno funcionamento, Apache JMeter com teste de performance/carga, anotações e afins.
Navegando entre os arquivos supracitados temos os testes extraidos do postman no formato Json, assim como os recursos necessarios para usa-los, Local.postman_enviroment, ServeREst.postman_collection. Estes serão acrescidos ao newman para obter o report html, conforme documentação a abaixo.

## Tecnologias e ferramentas utilizadas
- Git 
- GitHub
- Visual Studio Code
- Javascript
- Postman
- Nodejs
- Mocha
- Chai
- Apache JMeter

## Conteúdo do Projeto 
- Testes
- Newman
- Postman
- Local.postman_environment
- ServeRest.postman_collection
- ServeRest.postman_test_run
- Mapa atualizado dos Status code
- Apache JMeter e seus resultados

# Sobre o Projeto

## Prepraração para execução do projeto

- Requer o Nodejs 14.0 ou superior instalado, postman, newman instalados na sua maquina e o Apache JMeter.(Na instalação você verá onde baixar e como instalar.)
- Baixar o repositório ou cloná-lo
- Iniciar o Postman e importar os arquivos '.postman' nas pastas. 
- Os Arquivos estão localizados na pasta 'teste'com nome Local.postman... e ServeRest.postman...

PS: O JMeter não é obrigatorio, mas caso deseje ver ou executar o teste de performance localmente pode baixa-lo.

## Instalação

### Apache JMeter

- Instalando o JMeter
Na data de hoje a versão mais atual é a 5.5, vamos para o passo a passo da instalação:

- Faça o download do JMeter no site oficial (https://jmeter.apache.org/download_jmeter.cgi).

- Extraia o arquivo "apache-jmeter-5.5.zip" para uma pasta desejada.

- Pronto estamos pronto para usar o JMeter.

### Postman
- Para instalação do postman deve-se seguir ao site oficial (https://www.postman.com/downloads/) e baixar a versão correspondente ao seu sistema operacional.

### Newman + Nodejs
- Para instalação do newman deve-se seguir os seguintes passos:

- Baixar o NodeJS do site oficial ( https://nodejs.org/ ). Apenas certifique-se de instalar a versão que corresponde ao seu sistema operacional. 
- Durante a configuração da instalação, confirme se o gerenciador de pacotes npm está selecionado, pois usaremos este pacote na próxima etapa.

- Verificando o sucesso da instalação
- Podemos verificar se o NodeJS e o npm foram instalados com sucesso abrindo cmd e digitando:

- node-v

- A versão do NodeJS deve aparecer.

- npm -v

- A versão Npm deve aparecer.

- Instalando Newman e HTML Reports
- Newman é o executor de coleção que nos permite executar e testar uma coleção Postman a partir da linha de comando. A instalação é bem simples. 
- Use cmd mais uma vez e digite:

- npm install -g newman

- Assim que a instalação do Newman estiver concluída, podemos instalar os reports digitando:

- npm install -g newman-reporter-html
- npm install -g newman-reporter-htmlextra

- Finalmente, estamos prontos para criar os relatórios HTML!

## Execução


### JMeter

- Para executar o JMeter, devemos ir no diretório $Local de instalação do JMeter\bin\.
- Para executar no Windows devemos utilizar o arquivo jmeter.bat, para executar no Linux ou Mac devemos utilizar o arquivo jmeter.
- Ao acessar o diretório, navegue até a aba "Exibir" e marque a opção "Extensões de nomes de arquivos". Após selecionar o arquivo que corresponde ao seu SO o JMeter será executado e está pronto para uso.
- Bom agora estamos sabendo como executar nosso JMeter. Estão prontos para começar a rodar nossos testes?

- Para rodar nossos teste abra o JMeter e clique em file > Open > teste > JMeter > TesteServeRest.jmx. Pronto abrimos nosso teste.
PS: a pasta teste é baixada deste repositorio.

- Para rodar nosso testes clique em grupo de usuários e preencha os campos: Number of Threads(users) com quantos usuarios desejas para o teste, por default recomendo 500, pois é o modelo que fizemos para o teste. E em Loop Count coloque quantas interações deseja por usuário, por default recomendamos 2.

- Configurado nosso teste para iniciar clique Edit > Start e para ver os resultado você deve expandir a aba grupo de usuários e clica em: Aggregate Graph e Aggregate Report ambos externam os testes realizados.

### Newman

- Executando nossos arquivos JSON
- Esta é a nossa última etapa na criação dos relatórios HTML. 

- Primeiro, precisamos abrir o cmd e acessar a pasta onde salvamos nossos arquivos JSON (por exemplo, cd C:\Users\YourName\ExportedJSONs). 

- Uma vez que acessamos esta pasta, podemos executar os arquivos dentro dela usando este comando:

- newman run ServeRest.postman_collection.json -e Local.postman_environment.json -n 4 -r htmlextra

# Testes - Postman

Este repositório contém exemplos de diferentes tipos de testes que podem ser realizados no Postman. Os testes incluem: Testes de Funcionalidade, Integração, Regressão, Performance, Segurança, Aceitação e Contrato.

## Índice
- [Testes de Funcionalidade](#testes-de-funcionalidade)
- [Testes de Integração](#testes-de-integração)
- [Testes de Regressão](#testes-de-regressão)
- [Testes de Performance e Carga](#testes-de-performance-e-carga)
- [Testes de Segurança](#testes-de-segurança)
- [Testes de Aceitação](#testes-de-aceitação)
- [Testes de Contrato](#testes-de-contrato)

### Exemplos


```javascript
// Teste de sucesso para uma requisição GET
pm.test("Successful GET request", function () {
    pm.expect(pm.response.code).to.be.oneOf([200]);
});

// Verifica se o status da resposta é 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Verifica se o nome do status da resposta é "OK"
pm.test("Status code name has string", function () {
    pm.response.to.have.status("OK");
});

// Verifica se o tempo de resposta é menor que 1000ms
pm.test("Response time is less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});

// Verifica se a resposta é válida, possui um corpo e está no formato JSON
pm.test("response must be valid and have a body", function () {
     pm.response.to.be.ok;
     pm.response.to.be.withBody;
     pm.response.to.be.json;
});

// Verifica se a resposta contém atributos específicos
const atributos = ['quantidade', 'usuarios'];
atributos.forEach((atributo) => {
    pm.test(`Resposta contém atributo "${atributo}"`, () => {
        pm.expect(pm.response.json()[atributo]).to.exist;
    });
});

// Define um esquema JSON para validar a resposta
var schema = {
  "type": "object",
  "properties": {
    "quantidade": {
      "type": "integer"
    },
    "usuarios": {
      "type": "array",
      "items": [
        {
          "type": "object",
          "properties": {
            "nome": { "type": "string" },
            "email": { "type": "string" },
            "password": { "type": "string" },
            "administrador": { "type": "string" },
            "_id": { "type": "string" }
          },
          "required": ["nome", "email", "password", "administrador", "_id"]
        }
      ]
    }
  },
  "required": ["quantidade", "usuarios"]
};

// Valida o esquema da resposta
pm.test("Validating schema", () => {
    pm.response.to.have.jsonSchema(schema);
});
````

# Considerações Finais

Durante todo a trilha foi possivel um vislumbre de todo o andamento desse mundo tão vasto chamados de testes. Ser um analista QA não é facil requer muito estudo e dedicação, assim como atenção e cuidado. Agradeço muito aos meus companheiros que ajudaram a todo momento na criação de todos os testes.

## Autores

- José Milton de Oliveira Neto - 11035714
- Dielder Leal                 - 01461719
- Jailton Júnior               - 01225496
- Leonardo Emanuel             - 01418337
- Lucas Crespo                 - 01419654
