# TCC - Análise de Vulnerabilidades em APIs RESTful (crAPI)

Este repositório documenta o projeto de Trabalho de Conclusão de Curso (TCC) com foco na **identificação e exploração de vulnerabilidades críticas em APIs RESTful**, utilizando a aplicação vulnerável **crAPI** desenvolvida pela OWASP.

## Objetivo

Demonstrar, de forma prática, como vulnerabilidades como **Broken Object Level Authorization (BOLA)** e **Broken Authentication** podem ser exploradas por atacantes, e apresentar **boas práticas de mitigação** baseadas no OWASP Top 10.

## Ambiente de Testes

- **Sistema Host:** Ubuntu Server em máquina virtual
- **Sistema Atacante:** Kali Linux em máquina virtual

- ![image](https://github.com/user-attachments/assets/f15b8548-66d0-4602-89f4-cd0348af392d)
  
- **Ferramentas:** Docker, Kali Linux, Burp Suite, Postman, OWASP ZAP

- **Aplicação Alvo crAPI:** Em containers no Docker (vulnerável por design)

- ![image](https://github.com/user-attachments/assets/2898daad-3f63-4ac1-9d25-a5d5ea3a89df)
> Subindo a aplicação no Docker.

- **Rede:** O testes serão realizados em ambiente controlado, com duas máquinas virtuais onde ambas estarão em uma rede interna, Isolada e controlada para fins educacionais.

### Comunicação entre as máquinas virtuais após defini-las ambas na mesma subrede

- ![image](https://github.com/user-attachments/assets/ed68f0a9-8e89-4a8a-aef6-0d63940b435e)
> ping do Ubuntu Server para o Kali linux.

- ![image](https://github.com/user-attachments/assets/72dbb6a0-d4fa-4c21-a179-10bdd98391cb)
> ping do Kali Linux para o Ubuntu Server.

---

## Tecnologias Utilizadas

- Docker e Docker Compose
- Ferramentas de Pentest: Burp Suite, ZAP, Nmap, Wireshark
- Scripts em **Python** e **Bash** para automação de testes
- PostgreSQL/MySQL (no backend da crAPI)

---

## Estrutura do Projeto

| Pasta         | Descrição |
|---------------|-----------|
| `docs/`       | Relatório técnico e referências do projeto |
| `lab/`        | Arquivos e instruções para replicar o ambiente com Docker |
| `ataques/`    | Relatos de exploração de vulnerabilidades com ferramentas |
| `scripts/`    | Scripts para varredura e enumeração |
| `evidencias/` | Prints e logs das execuções dos testes |

---

## Mitigações Propostas

[Em processo]

---

## Referências

- [OWASP Top 10 - API Security](https://owasp.org/www-project-api-security/)
- [crAPI - Completely Ridiculous API](https://github.com/OWASP/crAPI)
- [Pentest em aplicações Web](https://novatec.com.br/livros/pentest-em-aplicacoes-web/)

---

## Aviso 

Este projeto foi desenvolvido exclusivamente para fins educacionais, voltado para demonstração controlada em ambiente de testes. Nenhuma técnica aqui documentada deve ser usada em ambientes reais sem autorização explícita.
