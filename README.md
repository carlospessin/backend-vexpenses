# Teste técnico - Backend Cartões 


Análise da aplicação da **VExpenses**

## Integração
 - Estou certo que é proposital, mas ao pingar https://api.banking.com.br/ não encontrou o host, o que deu ruim pra fazer as requisições da **camada de integração**.

## UseCases
- **Construtor com parâmetros:**  
    Sugestão de passar os parâmetros diretamente no construtor (SOLID).

- **Padronização de nomes:**  
    No `Login`, renomearia o nome da classe `create_token` para `CreateToken`, inclusive no nome do arquivo.

- **Transações:**  
    Quando a persistência atinge mais de uma tabela, usar `DB::transaction()` evita inconsistências em caso de erro.

- **Services/Repositories:**  
    Se os métodos crescerem em complexidade é interessante tratar numa camada de **Service** em vez de ser direto no **Repository**.

- **Comentário incorreto:**  
    O comentário da Login::handler() não condiz com o que o método faz.

- **Rotas públicas:**  
    Usaria prefix('auth') nas rotas públicas de `login` e `register`.

 - **Validações reutilizáveis:**  
    Criar uma camada de `Validators` para evitar duplicação, como no `validateUser()`.

- **SRP no CreateFirstUser:**  
    Em `User/CreateFirstUser`, existe mais de uma responsabilidade. Mas, sendo que o objetivo dele é criar um usuário **completo** isso envolve outras ações.

## Domains
- **Enums:**  
    Em `User/Create` e `User/Update`, seria interessante usar as constantes com ENUM.

- **Domínio Account:**  
    Criaria um domínio **Account** para centralizar validações e evitar duplicação, como no caso de `updateStatus` e `updateDatabase`

- **Validações no Update da Empresa:**  
    Em `Company/Update`, adicionar:
    - Verificação de existência da empresa
    - Validação do nome
    - Validação do número de documento

## Controller
- No `UserController`, escolheria usar `camelCase` nos parâmetros do `CreateFirstUserParams()`.

## Repositories
- Em `User/Retrieve`, o valor inserido pelo usuário é concatenado dentro da string SQL sem `bindings`. Existe a possibilidade de ocorrer um **SQL Injection**.

## Requests   
- Em `User/CreateRequest` e `User/RegisterRequest`, poderia ser usado regras mais seguras e coesas para os parametros.

## Testes
- Em `Feature/Company/UpdateTest`, o `"update name"` está falhando pois exite um erro no `find()` do método `update` do `CompanyController`.