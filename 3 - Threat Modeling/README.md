## Análise de Vulnerabilidades

Documentação do processo de análise de vulnerabilidades conduzido na aplicação crAPI (Completely Ridiculous API).

### Objetivo

O objetivo desta etapa é identificar, explorar e documentar de forma sistemática as vulnerabilidades de segurança presentes na aplicação alvo, com foco principal nas falhas de Autenticação Quebrada (Broken Authentication) e de Autorização Quebrada, incluindo BOLA (Broken Object Level Authorization) e BFLA (Broken Function Level Authorization), classificadas no OWASP API Security Top 10 (2023).

### Estrutura da Análise

Parte 1: Autenticação: explorar Broken Authentication.

Parte 2: Autorização: explorar BOLA e BFLA.

### Vulnerabilidades e Cenários de Teste
#### API1:2023 – Broken Object Level Authorization (BOLA)

A falha de BOLA ocorre quando a aplicação não valida corretamente se o usuário autenticado possui permissão para acessar o objeto (recurso) solicitado.

##### Cenário de Teste:

- Autenticar na aplicação com um usuário A (privilégio baixo).
- Mapear os endpoints da API que acessam recursos específicos de um usuário (ex.: visualizar perfil, histórico de compras, detalhes de um veículo).
- Identificar o ID do usuário B (outro usuário na plataforma).
- Realizar requisições aos endpoints mapeados utilizando o token de autenticação do usuário A, mas alterando o ID no corpo da requisição ou na URL para o ID do usuário B.

#### Resultado esperado:

#### API5:2023 – Broken Function Level Authorization (BFLA)

A falha de BFLA ocorre quando a aplicação não restringe corretamente o acesso a funções de diferentes níveis de privilégio.

##### Cenário de Teste:

- Autenticar na aplicação com um usuário comum.

[Evidências]


- Mapear endpoints administrativos (ex.: gerenciamento de usuários, configuração de permissões, exclusão de dados).

[Evidências]


- Tentar acessar esses endpoints utilizando o token do usuário comum.

[Evidências]

#### Resultado Esperado:
O usuário comum consegue executar funções administrativas, demonstrando falha no controle de autorização por nível de função.

#### API2:2023 – Broken Authentication

Falhas de autenticação permitem que atacantes comprometam tokens ou explorem implementações inseguras para assumir a identidade de outros usuários.

#### Cenário de Teste:

- Analisar o fluxo de autenticação, incluindo mecanismos de login, recuperação de senha e gerenciamento de sessão (tokens JWT, por exemplo).

[Evidências]

- Testar a ausência de limitação de tentativas (rate limiting) no endpoint de login, permitindo ataques de brute force.

[Evidências]

- Verificar se o token JWT possui uma assinatura fraca ou se o algoritmo pode ser alterado para none, permitindo a falsificação do token.

[Evidências]


- Investigar a funcionalidade de "lembrar-me" ou a validação de tokens para identificar se eles expiram corretamente ou podem ser reutilizados indefinidamente.

[Evidências]

#### Resultado Esperado (Evidência):
Obter acesso não autorizado à conta de outro usuário através da exploração de fraquezas, como um ataque de força bruta bem-sucedido ou a manipulação de um token JWT.

