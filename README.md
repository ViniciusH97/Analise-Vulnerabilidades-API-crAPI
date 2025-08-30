![GitHub last commit](https://img.shields.io/github/last-commit/ViniciusH97/Analise-Vulnerabilidades-API-crAPI)

# TCC - Análise de Vulnerabilidades em APIs RESTful (crAPI)

Este repositório documenta o projeto de Trabalho de Conclusão de Curso (TCC) com foco na **identificação e exploração de vulnerabilidades críticas em APIs RESTful**, utilizando a aplicação vulnerável **crAPI** desenvolvida pela OWASP.

## Objetivo

Demonstrar de forma prática, como vulnerabilidades como **Broken Object Level Authorization (BOLA)** e **Broken Authentication** entre outras, podem ser exploradas por atacantes, e apresentar **boas práticas de mitigação** baseadas no OWASP Top 10.

---

## Metodologia Utilizadas

A metodologia se seguirá pelos preceitos do (Penetration Testing Execution Standard), que auxiliará em uma análise mais ténica e eficiente dos testes. O metódo de teste seguirá com espeçoes manuais e automatizadas com uso de ferramentas e scripts com o conhecimento parcial da aplicação crAPI. Além disso, a categorização e a compreensão dos riscos serão aprimoradas pela consulta ao MITRE ATT&CK, tornando a visão das táticas e técnicas de um invasor real com foco nas vulnerabilidades críticas das APIs.

## Tecnologias Utilizadas

- Docker e Docker Compose
- Ferramentas de Pentest: Burp Suite, ZAP, Nmap, ffuf, Hydra, Postman entre outros.
- Scripts em **Python** e **Bash** para automação de testes
- PostgreSQL/MySQL (no backend da crAPI)

---

## Referências

- [OWASP Top 10 - API Security](https://owasp.org/www-project-api-security/)
- [crAPI - Completely Ridiculous API](https://github.com/OWASP/crAPI)
- [Meu Fork do Projeto do crAPI ajustado para o trabalho](https://github.com/ViniciusH97/crAPI.git)
- [Pentest em aplicações Web](https://novatec.com.br/livros/pentest-em-aplicacoes-web/)

---

## Aviso 

Este projeto foi desenvolvido exclusivamente para fins educacionais, voltado para demonstração controlada em ambiente de testes. Nenhuma técnica aqui documentada deve ser usada em ambientes reais sem autorização explícita.
