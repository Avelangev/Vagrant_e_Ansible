# Projeto Vagrant e Ansible

## Autor
- Avelange Viana

## Disciplina
- Administração de Sistemas Abertos

## Professor
- Pedro Batista de Carvalho Filho

## Descrição do Projeto
Este projeto tem como objetivo provisionar uma infraestrutura virtual utilizando Vagrant, e configurar serviços essenciais através do Ansible. Ele automatiza a configuração de sistemas operacionais, usuários, serviços como SSH, LVM, NFS, e outras tarefas de administração de sistemas.

### Configuração da VM
- **Provider**: VirtualBox
- **Box**: generic/debian12
- **IP**: 192.168.57.10
- **Discos adicionais**: 3x 10GB
- **Hostname**: p01_Avelange

### Serviços Configurados
1. Atualização do sistema operacional.
2. Configuração do hostname.
3. Criação de usuários e grupos.
4. Configuração de mensagem de saudação.
5. Configuração de permissões de SUDO.
6. Configuração de SSH (incluindo chave pública e desabilitação de senha).
7. Gerenciamento de LVM (Logical Volume Manager).
8. Configuração de servidor NFS.
9. Monitoramento de acessos via NFS.

## Instruções para Execução

### Pré-requisitos
Antes de iniciar, certifique-se de que as seguintes ferramentas estão instaladas:
- [Vagrant](https://developer.hashicorp.com/vagrant/install?product_intent=vagrant)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html)

### Passos para Execução

1. **Clone este repositório**:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd <NOME_DO_REPOSITORIO>

2. **Gere uma chave SSH para autenticação**: Caso ainda não tenha uma chave SSH, gere uma com o comando:
   ```bash
   ssh-keygen -t rsa -b 4096 -f /home/<Seu_Usuário>/.ssh/id_rsa

3. **Inicie a máquina virtual com o Vagrant: Antes de rodar o Vagrant, defina a variável de ambiente para utilizar o recurso experimental de discos:
   ```bash
    export VAGRANT_EXPERIMENTAL="disks"

4. Em seguida, inicie a máquina virtual:
   ```bash
   vagrant up

5. **Acesse a VM via SSH: Após a execução do playbook, você pode acessar a VM usando SSH com a chave gerada:
   ```bash
   ssh -i /home/<Seu_Usuário>/.ssh/id_rsa avelange@192.168.57.10

### Observações

- Substitua `<Seu_Usuário>` pelo seu nome de usuário no sistema.
- O IP da VM está configurado como `192.168.57.10`, então, verifique se a rede está configurada corretamente.
- O playbook configura o SSH para autenticação via chave pública e desabilita o login com senha. Certifique-se de que a chave pública esteja corretamente configurada.

### Testes de Configuração

1. **Subir a VM com Vagrant:**
   ```bash
   vagrant up

2. **Executar o provisionamento com Vagrant:
   ```bash
    vagrant provision

3. **Acessar a VM via SSH:
    ```bash
    vagrant ssh

4. **Verificar o hostname:
    ```bash
    hostname
    cat /etc/hostname

5. **Verificar grupos e usuários:
    ```bash
    getent group acesso_ssh
    id avelange
    id nfs-ifpb

6. **Verificar status do SSH:
    ```bash
    sudo systemctl status sshd

7. **Testar conexão SSH com chave privada:
    ```bash
    ssh -i /home/avelange/.ssh/id_rsa avelange@192.168.57.10

8. **Verificar configurações do SSH:
    ```bash
    grep PermitRootLogin /etc/ssh/sshd_config
    grep PasswordAuthentication /etc/ssh/sshd_config
    grep AllowGroups /etc/ssh/sshd_config

9. **Verificar informações do LVM:
    ```bash
    sudo vgdisplay dados
    sudo lvdisplay /dev/dados/sistema
    sudo blkid /dev/dados/sistema
    df -h | grep /dados
    grep /dados /etc/fstab

10. **Verificar status do NFS:
    ```bash
    sudo systemctl status nfs-kernel-server
    cat /etc/exports
    sudo exportfs -v

11. **Montar e testar o compartilhamento NFS:
    ```bash
    sudo mount -t nfs 192.168.57.10:/dados/nfs /mnt
    ls /mnt
    touch /mnt/test_file
    ls /mnt
    sudo umount /mnt

12. **Verificar logs de acessos NFS: 
    ```bash
    ls -l /dados/nfs/acessos
    cat /dados/nfs/acessos
    ssh -i /home/avelange/.ssh/id_rsa avelange@192.168.57.10
    tail -n 5 /dados/nfs/acessos
