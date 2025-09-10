## Análise de Vulnerabilidades

Este diretório documenta o processo de análise de vulnerabilidades conduzido na aplicação crAPI (Completely Ridiculous API), executada em um ambiente de laboratório controlado. A análise prática é um componente fundamental deste Trabalho de Conclusão de Curso, permitindo a demonstração e exploração das falhas de segurança discutidas no referencial teórico.

### Objetivo
O objetivo desta etapa é identificar, explorar e documentar de forma sistemática as vulnerabilidades de segurança presentes na aplicação alvo, com foco principal nas falhas de Autenticação Quebrada e Autorização Quebrada em Nível de Objeto (BOLA), classificadas no OWASP API Security Top 10.

#### Evidências das Vulnerabilidades
A seguir, são detalhados os planos de teste para as duas vulnerabilidades centrais do escopo deste trabalho.

- API1:2023 – Broken Object Level Authorization (BOLA)
A falha de BOLA ocorre quando a aplicação não valida corretamente se o usuário autenticado tem permissão para acessar o objeto (recurso) solicitado.

Cenário de Teste:

Autenticar na aplicação com um usuário A (privilégio baixo).

Mapear os endpoints da API que acessam recursos específicos de um usuário (ex: visualizar perfil, histórico de compras, detalhes de um veículo).

Identificar o ID do usuário B (outro usuário na plataforma).

Realizar requisições aos endpoints mapeados, utilizando o token de autenticação do usuário A, mas alterando o ID no corpo da requisição ou na URL para o ID do usuário B.

Resultado Esperado (Evidência): Obter sucesso ao acessar ou modificar dados pertencentes ao usuário B, estando autenticado como usuário A, comprovando a falha de autorização.

- API2:2023 – Broken Authentication
Falhas de autenticação permitem que atacantes comprometam tokens de autenticação ou explorem falhas de implementação para assumir a identidade de outros usuários.

#### Cenário de Teste:

Analisar o fluxo de autenticação, incluindo os mecanismos de login, recuperação de senha e gerenciamento de sessão (tokens JWT, por exemplo).

Testar a ausência de limitação de tentativas (rate limiting) no endpoint de login, permitindo ataques de brute force.

Verificar se o token JWT possui uma assinatura fraca ou se o algoritmo de assinatura pode ser alterado para none, permitindo a falsificação do token.

Investigar a funcionalidade de "lembrar-me" ou a validação de tokens para identificar se eles expiram corretamente ou se podem ser reutilizados indefinidamente.

Resultado Esperado (Evidência): Obter acesso não autorizado à conta de outro usuário através da exploração de uma das fraquezas mencionadas, como um ataque de força bruta bem-sucedido ou a manipulação de um token JWT.
