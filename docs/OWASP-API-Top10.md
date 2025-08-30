## OWASP Top 10 API Security Risks – 2023


**API1:2023 - Broken Object Level Authorization**	As APIs tendem a expor mais endpoints que manipulam identificadores de objetos, tornando as falhas no controlo de acessos mais suscetíveis a ataques. A verificação da autorização para acesso aos objetos deve ser tida em consideração em todas as funções que acedem a dados com base em informação fornecida pelo utilizador.


**API2:2023 - Broken Authentication**	Com frequência os mecanismos de autenticação são implementados de forma incorreta, permitindo aos atacantes comprometer os tokens de autenticação ou abusar das falhas na implementação por forma a assumir a identidade de outros utilizadores de forma temporária ou permanente.

**API3:2023 - Broken Object Property Level Authorization**	Esta categoria combina **API3:2019 - Excessive Data Exposure e API6:2019 - Mass Assignment**, focando na causa principal: a falta de validação de autorização adequada ao nível das propriedades do objeto. Isso leva à exposição ou manipulação de informações por partes não autorizadas.

**API4:2023 - Unrestricted Resource Consumption**	Satisfazer pedidos de API requer recursos como largura de banda de rede, CPU, memória e armazenamento. Outros recursos como emails/SMS/chamadas telefónicas ou validação biométrica são disponibilizados por fornecedores de serviços através de integrações de API, sendo pagos por pedido. Ataques bem-sucedidos podem levar a uma negação do serviço (DoS) ou a um aumento dos custos operacionais.

**API5:2023 - Broken Function Level Authorization**	Políticas de controlo de acesso complexas com diferentes níveis hierárquicos, grupos e perfis e uma não tão clara separação entre o que são ou não funcionalidades administrativas tendem a conduzir a falhas de autorização. Abusando destas falhas os atacantes podem ganhar acesso a recursos de outros utilizadores e/ou a funcionalidades administrativas.

**API6:2023 - Unrestricted Access to Sensitive Business Flows**	As APIs vulneráveis a este risco expõem um fluxo de negócio - como comprar um bilhete ou publicar um comentário - sem compensar por como a funcionalidade poderia prejudicar o negócio se fosse usada de forma excessiva e automatizada. Isto não resulta necessariamente de falhas de implementação.

**API7:2023 - Server Side Request Forgery	As falhas de Server-Side Request Forgery (SSRF)** podem ocorrer quando uma API está a obter um recurso remoto sem validar o URI fornecido pelo utilizador. Isto permite que um atacante force a aplicação a enviar um pedido manipulado para um destino inesperado, mesmo quando protegido por um firewall ou uma VPN.

**API8:2023 - Security Misconfiguration**	As APIs e os sistemas que as suportam normalmente contêm configurações complexas, destinadas a tornar as APIs mais personalizáveis. Os engenheiros de software e de DevOps podem ignorar essas configurações ou não seguir as melhores práticas de segurança quando se trata de configuração, abrindo a porta para diferentes tipos de ataques.

**API9:2023 - Improper Inventory Management**	As APIs tendem a expor mais endpoints do que as aplicações web tradicionais, fazendo com que a documentação se torne ainda mais importante. Um inventário dos hosts e APIs em execução também têm um papel importante na mitigação de falhas tais como versões de APIs descontinuadas e exposição de endpoints para análise de problemas.

**API10:2023 - Unsafe Consumption of APIs**	Os programadores tendem a confiar mais nos dados recebidos de APIs de terceiros do que os fornecidos pelo utilizador, e por isso tendem a adotar padrões de segurança mais fracos. Para comprometer APIs, os atacantes visam os serviços de terceiros integrados em vez de tentarem comprometer a API alvo diretamente.

Este documento utiliza trechos do **OWASP API Security Top 10**.

Fonte: [OWASP API Security Project](https://owasp.org/API-Security/)  
Licença: [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/)  

Todos os direitos pertencem à **OWASP Foundation**.