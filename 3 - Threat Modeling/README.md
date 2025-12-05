## Modelagem de Ameaças

Documentação do processo de análise de vulnerabilidades na aplicação crAPI.

### Objetivo

O objetivo desta etapa é identificar e registrar de forma organizada as vulnerabilidades de segurança na aplicação que estamos analisando.  O foco principal está nas falhas relacionadas à Autenticação Quebrada (API2:2023) e BOLA (Broken Object Level Authorization - API1:2023) e o BFLA (Broken Function Level Authorization - API5:2023), de acordo com o OWASP API Security Top 10.

### Estrutura da Análise

Parte 1: Autenticação: identificar possíveis Broken Authentication.

Parte 2: Autorização: identificar possíveis BOLA e BFLA (Autorização Quebrada em Nível de Função)

### Identificação de Endpoints Críticos:


**Endpoints que envolve identidade de usuário (Broken Authentication)**

Endpoints em que o atacante pode se passar por outra pessoa ou quebrar o fluxo de login.

**Crítica**

- POST /identity/api/auth/login: É possível realizar uma força bruta, pode manipular o login da aplicação e enumerar contas de usuários?

**Alta**
- POST /identity/api/v2/user/reset-password: É possível recuperar a senha da conta de outro usuário manipulando a requisição?

**Média**
- POST /identity/api/auth/signup : É possível criar usuários com senhas fracas?

---

**Endpoints que envolve a permissão do usuário para acessar e modificar objetos (BOLA e API5:2023 - BFLA)**

Após o usuário estar logado, esses endpoints são usados para verificar a permissão do usuário para acessar e modificar recursos da aplicação.

**Crítica**

- GET /identity/api/v2/user/dashboard: Como Usuário A, consigo acessar .../user/B/dashboard e ver os dados do Usuário B?

- POST /identity/api/v2/user/verify-email-token : (BFLA) Conta A pode ser usado para confirmar a troca de e-mail na Conta B, levando ao roubo da conta?

**Alta**

- GET /identity/api/v2/vehicle/{vehicleId}/location : É possível ver a localização do veículo de outro usuário?

- GET /identity/api/v2/vehicle/vehicles : É possível ver os veículos de outro usuário alterando o ID ou de outra forma?

- GET /community/api/v2/community/posts : Quais dados estão sendo retornados nas publicações?

- POST /identity/api/v2/user/change-email : Um usuário só pode iniciar essa ação para sua própria conta ou consegue solicitar para outra conta?

**Média**

- POST /workshop/api/shop/orders : (BOLA) Pode-se realizar uma compra em nome de outro usuário? 


Os endpoints foram categorizados pelo a hipótese de criticidade. Dessa forma, a próxima etapa será a [análise de vulnerabilidade(Vulnerability Analysis)](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/4%20-%20Vulnerability%20Analysis). Essa etapa vai evidênciar se realmente há vulnerabilidades nos endpoints classificados com grau de criticidade.
