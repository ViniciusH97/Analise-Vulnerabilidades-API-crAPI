## Pré-planejamento

### Teste de penetração de aplicativo Web

Antes de iniciarmos, é importante respondermos algumas perguntas para realizar o teste de invasão em uma aplicação web. Seguindo os preceitos do Penetration Testing Execution Standard (PTES).

---

**Perguntas**

Quantos aplicativos da web estão sendo avaliados?
R: Somente um chamado de crAPI

Quantos sistemas de login estão sendo avaliados?
R: Será avaliado apenas um: tela de Logon do crAPI.

Quantas páginas estáticas estão sendo avaliadas? (aproximado)
R: Aproximadamente 8 páginas.

Quantas páginas dinâmicas estão sendo avaliadas? (aproximado)
R: Aproximadamente 15 páginas.

O código-fonte será disponibilizado prontamente?
R: Sim, o código-fonte está disponível publicamente no repositório oficial do crAPI no GitHub.

Haverá algum tipo de documentação?
R: Sim, a documentação oficial do projeto, incluindo instruções de instalação e arquitetura da aplicação.

Se sim, que tipo de documentação?
R: Documentação técnica básica para instalação e uso da aplicação, além de informações sobre os endpoints da API.

A análise estática será realizada neste aplicativo?
R: Sim, será realizada análise estática de código para identificar más práticas de segurança no código-fonte.

O cliente deseja que o fuzzing seja executado neste aplicativo?
R: Sim, será executado fuzzing nos endpoints da API para avaliar como a aplicação lida com entradas inesperadas ou maliciosas.

O cliente deseja que o teste baseado em função seja executado neste aplicativo?
R: Sim, será realizado teste baseado em função, explorando os fluxos principais da aplicação (autenticação, gerenciamento de veículos e mensagens).

O cliente deseja que sejam executadas verificações credenciadas de aplicativos Web?
R: Sim, serão realizados testes autenticados para verificar permissões, controles de acesso e exposição de dados após login.

---

### Ambiente de Testes

- **Sistema Host:** Ubuntu Server em máquina virtual
- **Sistema Atacante:** Kali Linux em máquina virtual

#### Configuração do ambiente de teste:

- [Video autoral - Instalação do Ubuntu Server parte 1](https://youtu.be/EXaSY-5y3yI?si=aASKbSbslIPukknB)
- [Video autoral - Instalação do Ubuntu Server parte 2](https://youtu.be/nb0mQ3gPHeQ?si=RAPE3cow92k8rOch)

- [Video autoral - Instalação do Kali Linux](https://youtu.be/aUyct83SRX0?si=rcahdz4w6uTPCFk1)
---

![image](https://github.com/user-attachments/assets/f15b8548-66d0-4602-89f4-cd0348af392d)
  
- **Aplicação Alvo crAPI:** Em containers no Docker (vulnerável por design)

- ![image](https://github.com/user-attachments/assets/2898daad-3f63-4ac1-9d25-a5d5ea3a89df)
> Subindo a aplicação no Docker.

- **Rede:** Os testes foram realizados em ambiente controlado, com duas máquinas virtuais onde ambas estavam em uma rede interna, Isolada e controlada.

### Comunicação entre as máquinas virtuais após configurar ambas na mesma subrede (Rede interna)

- ![image](https://github.com/user-attachments/assets/ed68f0a9-8e89-4a8a-aef6-0d63940b435e)
> ping do Ubuntu Server para o Kali linux.

- ![image](https://github.com/user-attachments/assets/72dbb6a0-d4fa-4c21-a179-10bdd98391cb)
> ping do Kali Linux para o Ubuntu Server.


