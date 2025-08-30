## Pré-planejamento

### Ambiente de Testes

- **Sistema Host:** Ubuntu Server em máquina virtual
- **Sistema Atacante:** Kali Linux em máquina virtual

- ![image](https://github.com/user-attachments/assets/f15b8548-66d0-4602-89f4-cd0348af392d)
  
- **Aplicação Alvo crAPI:** Em containers no Docker (vulnerável por design)

- ![image](https://github.com/user-attachments/assets/2898daad-3f63-4ac1-9d25-a5d5ea3a89df)
> Subindo a aplicação no Docker.

- **Rede:** Os testes foram realizados em ambiente controlado, com duas máquinas virtuais onde ambas estavam em uma rede interna, Isolada e controlada.

### Comunicação entre as máquinas virtuais após configurar ambas na mesma subrede (Rede interna)

- ![image](https://github.com/user-attachments/assets/ed68f0a9-8e89-4a8a-aef6-0d63940b435e)
> ping do Ubuntu Server para o Kali linux.

- ![image](https://github.com/user-attachments/assets/72dbb6a0-d4fa-4c21-a179-10bdd98391cb)
> ping do Kali Linux para o Ubuntu Server.