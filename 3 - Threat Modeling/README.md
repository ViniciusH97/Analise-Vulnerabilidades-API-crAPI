## Modelagem de Ameaças

Documentação do processo de análise de vulnerabilidades conduzido na aplicação crAPI (Completely Ridiculous API).

### Objetivo

O objetivo desta etapa é identificar e documentar de forma sistemática as vulnerabilidades de segurança presentes na aplicação alvo, com foco principal nas falhas de Autenticação Quebrada (API2:2023) e Autorização Quebrada, incluindo BOLA (Broken Object Level Authorization - API1:2023) e BFLA (Broken Function Level Authorization - API5:2023), conforme o OWASP API Security Top 10.

### Estrutura da Análise

Parte 1: Autenticação: explorar Broken Authentication.

Parte 2: Autorização: explorar BOLA e BFLA (Autorização Quebrada em Nível de Função)

### Identificação de Endpoints Críticos:


**Endpoints que envolve identidade de usuário (Broken Authentication)**

Endpoints em que o atacante pode se passar por outra pessoa ou quebrar o fluxo de login.

**Crítica**

- POST /identity/api/auth/login: É possível teste de brute force, e pode manipular o login da aplicação?

**Alta**
- POST /identity/api/v2/user/reset-password: É possível recuperar a senha da conta de outro usuário manipulando a requisição?

**Média**
- POST /identity/api/auth/signup : É possível criar usuário com senhas fracas e enumerar contas existentes?

---

**Endpoints que envolve a permissão do usuário para acessar e modificar objetos (BOLA e API5:2023 - BFLA)**

Após o usuário estar logado, esses endpoints são usados para verificar a permissão do usuário para acessar e modificar recursos da aplicação.

**Crítica**

- GET /identity/api/v2/user/dashboard: Como Usuário A, consigo acessar .../user/B/dashboard e ver os dados do Usuário B?

- POST /identity/api/v2/user/verify-email-token : (BFLA) Conta A pode ser usado para confirmar a troca de e-mail na Conta B, levando ao roubo da conta?

**Alta**

- GET /identity/api/v2/vehicle/vehicles : (BOLA) É possível ver os veículos de outro usuário alterando o ID ou de outra forma?

- POST /identity/api/v2/user/change-email : (BFLA) Um usuário só pode iniciar essa ação para sua própria conta?

**Média**

- POST /workshop/api/shop/orders : (BOLA) Pode-se realizar uma compra em nome de outro usuário? 


Os endpoints foram categorizados por criticidade. Dessa forma, a próxima etapa será a [análise de vulnerabilidade(Vulnerability Analysis)](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/4%20-%20Vulnerability%20Analysis)
