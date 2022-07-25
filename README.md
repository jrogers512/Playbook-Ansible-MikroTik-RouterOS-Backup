# Línguas
Traduções alternativas podem ser encontradas nos links abaixo.
- [English](README-en.md)

# Introduction
Playbook de Backup de Routeadores RouterOS MikroTik

Automatizando o processo de backup de roteadores Mikrotik com playbooks Ansible e o Cron do Linux.

A parte mais legal desse playbook é que ao final do playbook, a última task do Ansible realiza a chamada de um script que faz commit/push dos arquivos de configuração do backup, onde os mesmo já podem ser copiados para um repositório Git.

Para que no momento do push, o Git use a chave privada para se autenticar no repositório faça a seguinte configuração:

# Configuração SSH/Git
Uma dica!! Antes de tudo, crie o repositório e logo após clone o mesmo no servidor.
----------
1. Gerar as chaves ssh
```bash
$ ssh-keygen -t rsa -b 2048 -C "kessix@example.com"
```
2. As chaves ficam armazenadas dentro do diretório home do usuário logado:
```bash
~/.ssh/id_rsa (privada)
~/.ssh/id_rsa.pub (pública)
```
3. Crie o arquivo ~/.ssh/config
A configuração pode mudar dependendo do seu repositório.
Adionce o conteúdo abaixo e mude os parâmetros de acordo com seu repositório:
```bash
- GitRepo
Host gitrepo.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/gitrepo_com_rsa (essa linha deve apontar para a chave privada)
 ```
4. Dida ao cliente SSH para apontar para a chave privada:
```bash
$ eval $(ssh-agent -s)
$ ssh-add ~/.ssh/id_rsa (privada)
```
5. Adicione a chave pública na plataforma do seu repositório.
- Consulte a documentação do reposótio e veja como fazer esse procedimento.

6. Teste a cominicação entre o agente ssh e o repositório
```bash
$ ssh -Tvvv git@gitrepo.com
```
