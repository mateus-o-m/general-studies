## CLI do Linux

### Sintaxe de comandos: `comando opcoes argumentos`

Argumento: específica algo para o comando agir
Opções: alteram o comportamento do comando
Exemplo: o comando `ls` imprime uma lista de arquivos na tela,
e exsitem as opções `l` (long), que imprime mais informações na tela
e `r` (reverse), que inverte a ordem da lista
Comandos:
```bash
ls -r
ls -l -r
ls -lr
```

### Imprimir o diretório atual de trabalho: `pwd opcoes`

### Mudar diretório: `cd`

|comando|descrição|
|-|-|
|`cd opcoes caminho`|muda o diretório de trabalho|
|`cd ..`|volta um diretório|
|`cd ~`|pula para o diretório home|

### Listar os arquivos

|comando|descrição|
|-|-|
|`ls opcoes argumentos`|se usado sem argumentos, lista arquivos do diretório atual|
|`ls -l`|lista longa, com mais detalhes dos arquivos|

#### Exemplo do comando `ls -l`

```bash
sysadmin@localhost:~$ ls -l /var/log/
total 844
-rw-r--r-- 1 root   root  18047 Dec 20  2017 alternatives.log
drwxr-x--- 2 root   adm    4096 Dec 20  2017 apache2
drwxr-xr-x 1 root   root   4096 Dec 20  2017 apt
-rw-r----- 1 syslog adm    1346 Oct  2 22:17 auth.log
-rw-r--r-- 1 root   root  47816 Dec  7  2017 bootstrap.log
-rw-rw---- 1 root   utmp      0 Dec  7  2017 btmp
-rw-r----- 1 syslog adm     547 Oct  2 22:17 cron.log
-rw-r----- 1 root   adm   85083 Dec 20  2017 dmesg
-rw-r--r-- 1 root   root 325238 Dec 20  2017 dpkg.log
-rw-r--r-- 1 root   root  32064 Dec 20  2017 faillog
drwxr-xr-x 2 root   root   4096 Dec  7  2017 fsck
-rw-r----- 1 syslog adm     106 Oct  2 19:57 kern.log
-rw-rw-r-- 1 root   utmp 292584 Oct  2 19:57 lastlog
-rw-r----- 1 syslog adm   19573 Oct  2 22:57 syslog
drwxr-xr-x 2 root   root   4096 Apr 11  2014 upstart
-rw-rw-r-- 1 root   utmp    384 Oct  2 19:57 wtmp
```

#### Tipos de arquivo

Primeiro digito no exemplo acima: `-` e `d`

|comando|descrição|
|-|-|
|`d`|diretório (pastas, etc)|
|`-`|arquivo comum|
|`l`|link simbólico, aponta para outro arquivo|
|`s`|tomada, permite comunicação entre processos|
|`p`|tubo, premite comunicação entre processos|
|`b`|arquivo bloqueado|
|`c`|arquivo de caracteres|

#### Permissões

Digitos após o primeiro: Indica como os usuários podem usar o arquivo
No exemplo: `rw-r--r--` e `rwxr-x---`

#### Contagem de links físicos/rígidos

Após o indicador de permissões: Indicam quantos links físicos/rigidos apontam para o arquivo
No exemplo: `1` e `2`

#### Proprietário do usuário

Usuário dono do arquivo: quando um arquivo é criado, essa propriedade é atribuída
ao usuário que o criou. No exemplo: `syslog` e `root`

#### Propriedade de grupo

Indica qual grupo possui o arquivo
No exemplo: `utmp` e `adm` e `root`

#### Tamanho do arquivo

Logo após a indicação do grupo. Arquivos pequenos em bytes, arquivos grandes em kilobytes

#### Ordenação(opções) do comando `ls`

|comando|descrição|
|-|-|
|`-t`|classifica arquivos por ordem de data|
|`-s`|classifica arquivos por ordem de tamanho|
|`-r`|inverte a ordem de classificação|

### Acesso administrativo

Permite atuar temporariamente com acesso administrativo: `su opcoes nome`
Se o nome não for especificado, o comando abrirá um shell como usuário root

#### Opção de login

Configura o shell com as configurações do novo usuário: `su -`, `su -l` ou `su --login`

#### Comando `sudo`

Permite a execução de um comando como outro usuário, sem criar um novo shell.
Utiliza o usuário root como padrão

### Permissões

Determina as maneiras pelas quais diferentes usuários podem interagir com o arquivo/diretório
Exemplo (CLI): `drwxr-x--- 2 root   adm    4096 Dec 20  2017 apache2`
As permissões do exemplo acima são:

|todas as permissões|proprietário|grupo|outros|
|-|-|-|-|
|`rwxr-x---`|`rwx`|`r-x`|`---`|

#### Tipos de permissão

|permissão|ação no arquivo|ação no diretório|
|-|-|-|
|`r`|permite ler ou copiar|com permissões de execução,
o comando`ls -l` fornecerá lista detalhada de arquivos|
|`w`|permite substituir ou modificar,
também permite adicionar ou removerde um diretório|é necessário a permissão de execução|
|`x`|permite executar como processo,
arquivos script exigempermissão de leitura|permite mudar para um diretório,
se o diretório pai tiver a mesmapermissão (de execução)|

### Alterar permissões de arquivos: `chmod`

Método simbólico: `chmod CONJUNTO AÇAO PERMISSÕES ARQUIVO`

|conjunto|descrição|
|-|-|
|`u`|usuário, proprietário|
|`g`|grupo|
|`o`|outros|
|`a`|todos: `u`, `g` e `o`|

|ação|descrição|
|-|-|
|`+`|adicionar permissão|
|`-`|remover permissão|
|`=`|especificar permissão exata|

Permissões, especificar uma ou mais: `r`, `w` e `x`

### Alterar propriedades de arquivos: `chown`

Comando: `chown OPÇÕES PROPRIETÁRIO ARQUIVO`
Proprietário: indica qual usuário será o novo proprietário do arquivo
Usar `sudo` para obter privilégios administrativos necessários

### Exibir arquivos

|comando|descrição|
|-|-|
|`cat opcoes arquivo`|concatenar: exibirá todo o conteúdo do arquivo,
uso recomendado para arquivos pequenos|
|`head opcoes arquivo`|exibe somente linhas superiores|
|`tail opcoes arquivo`|exibe linhas da parte inferior|
|`head -n numDeLinhas arquivo`|para especificar a quantidade de linhas
que serão exibidas pelos comandos `head` ou `tail`|	

### Copiar arquivos

Comando `cp`, ou `dd` (copiar a nível de bits)
Sintaxe: `cp OPÇÕES FONTE DESTINO`, `dd OPÇÕES OPERANDO`

#### Argumentos de dd

Exemplo: `dd if=/dev/zero of=/tmp/swapex bs=1M count=50`

|argumento|descrição|
|-|-|
|`if`|arquivo de entrada, que será lido|
|`of`|arquivo de saída, que será gravado|
|`bs`|tamanho do bloco que será usado, pode ser: `K`(kilobytes),
`M`(megabytes),`G`(gigabytes) ou `T`(terabytes)|
|`count`|número da contagem dos blocos a partir do arquivo de entrada|

### Mover arquivos: `mv FONTE DESTINO`

Fonte: é o arquivo em questão
Destino: local de destino. Se for indicado como o nome de um arquivo,
o arquivo fonte será renomeado pelo nome do arquivo de destino
Exemplo: `mv animals.txt zoo.txt`, renomeia animals.txt para zoo.txt

### Remover arquivos `rm OPÇÕES ARQUIVO`

Remove arquivos permanentemente
Sem instrução(opções): remove arquivos regulares
Opção recursiva: `-r` ou `-R`, remove todos os arquivos e subdiretórios

### Filtragem de entrada

Comando: <cod>grep OPÇÕES PADRÃO ARQUIVO`
PADRÃO: é o termo que será pesquisado em ARQUIVO

#### Caracteres básicos

|caractere Regex básico|descrição|
|-|-|
|`.`|qualquer caractere único|
|`[ ]`|qualquer caractere específicado|
|`[^ ] `|não é o caractere especificado|
|`*`|zero ou mais caracteres anteriores|
|`^`|se for o primeiro caractere do padrão:
o padrão deve estar no inicio da linha paracorresponder;
se não for o primeiro caractere: apenas um `^` literal|
|`$`|se for o úttimo caractere do padrão:
o padrão deve estar no final da linha para corresponder;
se não for o último caractere: apenas um `$` literal|

#### Expressões estendidas

Devem ser usadas com comandos: `egrep` ou `grep -E`

|caracteres Regex extendidos|descrição|
|-|-|
|`+`|um ou mais do padrão anterior|
|`?`|o padrão anterior é opcional|
|`{ }`|especifica correspondência mínima,
máxima ou exata do padrão anterior|
|`\|`|alternação: um `OR` (ou) lógico|
|`( )`|criar grupos|

### Desligando: `shutdown OPÇÕES TEMPO MENSAGEM`

### Configuração de rede

|comando|descrições|
|-|-|
|`ifconfig OPÇÕES`|configurações de interface|
|`iwconfig OPÇÕES`|configurações wireless|
|`ping -c mumDePings`|verificar a conectividade|

### Exibindo processos: `ps OPÇÕES`

Processos em execução:
```bash
sysadmin@localhost:~$ ps
PID TTY          TIME CMD
80 pts/0        00:00:00 bash
94 pts/0        00:00:00 os
```

Exibir todos os processsos
```bash
sysadmin@localhost:~$ ps -e
PID TTY          TIME CMD  
1 pts/0        00:00:00 init  
33 ?            00:00:00 rsyslogd  
37 ?            00:00:00 cron  
39 ?            00:00:00 sshd  
56 ?            00:00:00 named  
69 pts/0        00:00:00 login  
79 pts/0        00:00:00 bash  
94 pts/0        00:00:00 os
```

Exibir todos os processos de forma detalhada
Inclui detalhes na saída do comando, como opções e argumentos
```bash
sysadmin@localhost:~$ ps -ef
UID        PID  PPID  C STIME TTY      TIME CMD
root         1     0  0 19:16 pts/0    00:00:00 /sbin??? /init
syslog      33     1  0 19:16 ?        00:00:00 /usr/sbin/rsyslogd
root        37     1  0 19:16 ?        00:00:00 /usr/sbin/cron
root        39     1  0 19:16 ?        00:00:00 /usr/sbin/sshd
bind        56     1  0 19:16 ?        00:00:00 /usr/sbin/named -u bind
root        69     1  0 19:16 pts/0    00:00:00 /bin/login -f
sysadmin    79    69  0 19:16 pts/0    00:00:00 -bash
sysadmin    95    79  0 19:43 pts/0    00:00:00 ps -ef
```

Identificadores de processo

|comando|descrição|
|-|-|
|`PTD`|id do processo, exclusivo para cada processo|
|`TTY`|nome do terminal de execução do processo|
|`TIME`|tempo usado pelo processo|
|`CMD`|comando que iniciou o processo|

### Gerenciamento de pacotes

|comando|descrição|
|-|-|
|`dpkg`|gerenciamento de pacotes Debian, no nível maix baixo|
|`apt`|Advanced Package Tool, programa front-end para a ferramenta dpkg|

#### Comandos `apt`

Para utilização do `apt` é recomendado o uso do comando `sudo`

|comando|descrição|
|-|-|
| `sudo apt-get update` | atualiza a lista de pacotes disponíveis |
| `sudo apt-get upgrade` | todos os pacotes/dependências disponíveis serão atualizados |
| `apt-cache seach (palavra chave)` | procura por nome ou descrição de algum pacote |
| `sudo apt-get install pacote` | instala o pacote especificado |
| `sudo apt-get remove pacote` | Remove o pacote especificado |
| `sudo apt-get purge pacote` | limpa completamente o pacote especificado |

### Atualizar senhas: `passwd OPÇÕES USUÁRIO`

#### Exemplo do comando `passwd`

```bash
sysadmin@localhost:~$ passwd -S sysadmin
sysadmin P 12/20/2017 0 99999 7 -1
```

|comando|descrição|
|-|-|
|`-S`|opção que exibe o status da senha|
|`sysadmin`|nome do usuário|
|`P`|P: senha utlizavelL: senha bloqueadaNP: não há senha|
|`12/20/2017`|última data em que a seha foi alterada|
|`0`|mínimo de dias antes que a senha possa ser alterada|
|`99999`|dias restantes para a senha expirar|
|`7`|dias antes da data de expiração que o usuário é notificado|
|`-1`|dias após a expiração da senha que a conta permanece ativa|

### Redirecionamento: `COMANDO > ARQUIVO`

Redireciona a saída(STDOUT), que normalmente é o terminal, de um comando para um arquivo
Exemplos:
Substituir: `echo "conteúdo" > ARQUIVO`, substitui o conteúdo de ARQUIVO pelo "conteúdo" especificado
Anexar: `echo "conteúdo" >> ARQUIVO`, anexa "conteúdo" ao ARQUIVO

### Editor de texto

