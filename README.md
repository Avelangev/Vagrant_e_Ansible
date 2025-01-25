# Projeto Vagrant e Ansible

## Autor
- Avelange Viana
## Disciplina
- Administração de Sistemas Abertos
## Professor
- Pedro Batista de Carvalho Filho
## Descrição do Projeto
Este projeto provisiona uma infraestrutura virtual usando Vagrant e configura serviços essenciais com Ansible.

### Configuração da VM
- Provider: VirtualBox
- Box: generic/debian12
- IP: 192.168.57.10
- Discos adicionais: 3x 10GB
- Hostname: p01_Avelange

### Serviços Configurados
1. Atualização do sistema operacional.
2. Configuração de hostname.
3. Criação de usuário.
4. Configuração de mensagem de saudação.
5. Configuração de permissões SUDO.
6. Configuração de SSH.
7. Gerenciamento de LVM.
8. Configuração de servidor NFS.
9. Monitoramento de acessos.

## Instruções para Execução
1. Clone este repositório.
2. Certifique-se de ter Vagrant, VirtualBox e Ansible instalados.
3. Gere uma chave para realizar o ssh
   ```bash
   ssh-keygen -t rsa -b 4096 -f /home/<Seu_Usuário>/.ssh/id_rsa
5. Execute:
   ```bash
   export VAGRANT_EXPERIMENTAL="disks"
   vagrant up
6. Após executar o playbook.yml será necessário logar utilizando a chave pública gerada anteriormente, exemplo:
   ```bash
   ssh -i /home/<Seu_Usuário>/.ssh/id_rsa avelange@192.168.57.10
