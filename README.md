Testes Automatizados de API REST com Postman & Newman

Projeto de testes automatizados de API REST cobrindo validações de contrato, regras de negócio, tempos de resposta, autenticação via Token e execução em linha de comando (CI/CD).

 Objetivo
Garantir a integridade e confiabilidade de APIs públicas utilizando boas práticas de QA: validação do Caminho Feliz (Happy Path), Cenários Negativos (Unhappy Path), parametrização de ambientes com variáveis, extração dinâmica de Tokens de autenticação e automação headless via terminal.

 Tecnologias e Ferramentas
- **Postman Desktop** (Design de requisições e execução em lote com Collection Runner)
- **Newman CLI** (Execução automatizada em linha de comando para pipelines de CI/CD)
- **Node.js** (Ambiente de execução de JavaScript)
- **JavaScript / Chai Assertion Library** (Scripts de validação e asserções automatizadas)
- **Git & GitHub** (Versionamento de código e documentação)
- **APIs Testadas:** [JSONPlaceholder](https://jsonplaceholder.typicode.com/) e [ReqRes](https://reqres.in/)

---

 Cenários de Teste Cobertos

| Método | Endpoint | Cenário / Objetivo | Validações Automatizadas | Status Esperado |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `{{baseUrl}}/posts/1` | Consulta de post por ID | - Status Code 200<br>- Validação do `id == 1` | `200 OK` |
| **POST** | `{{baseUrl}}/posts` | Cadastro de novo post | - Status Code 201<br>- Tempo de resposta < 1000ms<br>- Integridade do título enviado | `201 Created` |
| **GET** | `{{baseUrl}}/posts/9999` | Cenário negativo (id inexistente) | - Validação de erro controlado | `404 Not Found` |
| **POST** | `https://reqres.in/api/login` | Login com sucesso | - Status Code 200<br>- Extração dinâmica do token para a variável `userToken` | `200 OK` |
| **POST** | `https://reqres.in/api/login` | Login sem senha (cenário negativo) | - Status Code 400<br>- Validação da mensagem `"Missing password"` | `400 Bad Request` |

---

 Como Executar a Bateria de Testes

### Opção 1: Via Linha de Comando (Newman CLI / CI-CD)
> Requer Node.js instalado. Instale o Newman globalmente: `npm install -g newman`

Execute no terminal na raiz do projeto:
```bash
newman run "My Collection.postman_collection.json" --env-var "baseUrl=https://jsonplaceholder.typicode.com"