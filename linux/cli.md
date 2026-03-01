## CLI do Linux

### Sintaxe de comandos: <code>comando opcoes argumentos</code>

<p>Argumento: específica algo para o comando agir<br>
Opções: alteram o comportamento do comando<br>
Exemplo: o comando <code>ls</code> imprime uma lista de arquivos na tela, e exsitem as opções <code>l</code> (long),<br>
que imprime mais informações na tela e <code>r</code> (reverse), que inverte a ordem da lista<br>
Comandos: <code>ls -r</code> ,<code>ls -l -r</code>, <code>ls -lr</code></p>

### Imprimir o diretório atual de trabalho

<code>pwd opcoes</code>

### Mudar diretório: <code>cd</code>

|||
|-|-|
|<code>cd opcoes caminho</code>|muda o diretório de trabalho|
|<code>cd ..</code>|volta um diretório|
|<code>cd ~</code>|pula para o diretório home|

### Listar os arquivos

|||
|-|-|
|<code>ls opcoes argumentos</code>|se usado sem argumentos, lista arquivos do diretório atual|
|<code>ls -l</code>|lista longa, com mais detalhes dos arquivos|

#### Exemplo do comando <code>ls -l</code>

<p><code>sysadmin@localhost:~$ ls -l /var/log/
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
-rw-rw-r-- 1 root   utmp    384 Oct  2 19:57 wtmp</code></p>

#### Tipos de arquivo

Primeiro digito no exemplo acima: <code>-</code> e <code>d</code>

|||
|-|-|
|<code>d</code>|diretório (pastas, etc)|
|<code>-</code>|arquivo comum|
|<code>l</code>|link simbólico, aponta para outro arquivo|
|<code>s</code>|tomada, permite comunicação entre processos|
|<code>p</code>|tubo, premite comunicação entre processos|
|<code>b</code>|arquivo bloqueado|
|<code>c</code>|arquivo de caracteres|

#### Permissões

<p>Digitos após o primeiro: Indica como os usuários podem usar o arquivo<br>
No exemplo: <code>rw-r--r--</code> e <code>rwxr-x---</code></p>

#### Contagem de links físicos/rígidos

<p>Após o indicador de permissões: Indicam quantos links físicos/rigidos apontam para o arquivo<br>
No exemplo: <code>1</code> e <code>2</code></p>

#### Proprietário do usuário

<p>Usuário dono do arquivo: quando um arquivo é criado, essa propriedade é atribuída<br>
ao usuário que o criou. No exemplo: <code>syslog</code> e <code>root</code></p>

#### Propriedade de grupo

<p>Indica qual grupo possui o arquivo<br>
No exemplo: <code>utmp</code> e <code>adm</code> e <code>root</code></p>

#### Tamanho do arquivo

Logo após a indicação do grupo. Arquivos pequenos em bytes, arquivos grandes em kilobytes

#### Ordenação(opções) do comando <code>ls</code>

|||
|-|-|
|<code>-t</code>|classifica arquivos por ordem de data|
|<code>-s</code>|classifica arquivos por ordem de tamanho|
|<code>-r</code>|inverte a ordem de classificação|

### Acesso administrativo

<p>Permite atuar temporariamente com acesso administrativo<br>
<code>su opcoes nome</code><br>
Se o nome não for especificado, o comando abrirá um shell como usuário root</p>

#### Opção de login

Configura o shell com as configurações do novo usuário: <code>su -</code>, <code>su -l</code> ou <code>su --login</code>

#### Comando <code>sudo</code>

<p>Permite a execução de um comando como outro usuário, sem criar um novo shell.<br>
Utiliza o usuário root como padrão</p>

### Permissões

<p>Determina as maneiras pelas quais diferentes usuários podem interagir com o arquivo/diretório<br>
Exemplo (CLI): <code>drwxr-x--- 2 root   adm    4096 Dec 20  2017 apache2</code><br>
As permissões do exemplo acima são:</p>

|todas as permissões|proprietário|grupo|outros|
|-|-|-|-|
|<code>rwxr-x---</code>|<code>rwx</code>|<code>r-x</code>|<code>---</code>|

#### Tipos de permissão

|permissão|ação no arquivo|ação no diretório|
|-|-|-|
|<code>r</code>|permite ler ou copiar|com permissões de execução, o comando<br><code>ls -l</code> fornecerá lista detalhada de arquivos|
|<code>w</code>|permite substituir ou modificar,<br> também permite adicionar ou remover<br>de um diretório|é necessário a permissão de execução|
|<code>x</code>|permite executar como processo,<br>arquivos script exigem<br>permissão de leitura|permite mudar para um diretório,<br>se o diretório pai tiver a mesma<br>permissão (de execução)|

### Alterar permissões de arquivos: <code>chmod</code>

<p>Método simbólico: <code>chmod CONJUNTO AÇAO PERMISSÕES ARQUIVO</code></p>

|conjunto|descrição|
|-|-|
|<code>u</code>|usuário, proprietário|
|<code>g</code>|grupo|
|<code>o</code>|outros|
|<code>a</code>|todos: <code>u</code>, <code>g</code> e <code>o</code>|

|ação|descrição|
|-|-|
|<code>+</code>|adicionar permissão|
|<code>-</code>|remover permissão|
|<code>=</code>|especificar permissão exata|

<p>Permissões, especificar uma ou mais: <code>r</code>, <code>w</code> e <code>x</code></p>

### Alterar propriedades de arquivos> <code>chown</code>

<p>Comando: <code>chown OPÇÕES PROPRIETÁRIO ARQUIVO</code><br>
Proprietário: indica qual usuário será o novo proprietário do arquivo<br>
Usar <code>sudo</code> para obter privilégios administrativos necessários</p>

### Exibir arquivos

|||
|-|-|
|<code>cat opcoes arquivo</code>|concatenar: exibirá todo o conteúdo do arquivo,<br> uso recomendado para arquivos pequenos|
|<code>head opcoes arquivo</code>|exibe somente linhas superiores|
|<code>tail opcoes arquivo</code>|exibe linhas da parte inferior|
|<code>head -n numDeLinhas arquivo</code>|para especificar a quantidade de linhas que<br> serão exibidas pelos comandos <code>head</code> ou <code>tail</code>|	

### Copiar arquivos

<p>Comando <code>cp</code>, ou <code>dd</code> (copiar a nível de bits)<br>
Sintaxe: <code>cp OPÇÕES FONTE DESTINO</code>, <code>dd OPÇÕES OPERANDO</code></p>

#### Argumentos de dd

<p>Exemplo: <code>dd if=/dev/zero of=/tmp/swapex bs=1M count=50</code></p>

|argumento|descrição|
|-|-|
|<code>if</code>|arquivo de entrada, que será lido|
|<code>of</code>|arquivo de saída, que será gravado|
|<code>bs</code>|tamanho do bloco que será usado,<b>pode ser: <code>K</code>(kilobytes), <code>M</code>(megabytes),<br><code>G</code>(gigabytes) ou <code>T</code>(terabytes)|
|<code>count</code>|número da contagem dos blocos<b>a partir do arquivo de entrada|

### Mover arquivos: <code>mv FONTE DESTINO</code>

<p>Fonte: é o arquivo em questão<br>
Destino: local de destino. Se for indicado como o nome de um arquivo,<br>
o arquivo fonte será renomeado pelo nome do arquivo de destino<br>
Exemplo: <code>mv animals.txt zoo.txt</code>, renomeia animals.txt para zoo.txt</p>

### Remover arquivos <code>rm OPÇÕES ARQUIVO</code>

<p>Remove arquivos permanentemente<br>
Sem instrução(opções): remove arquivos regulares<br>
Opção recursiva: <code>-r</code> ou <code>-R</code>, remove todos os arquivos e subdiretórios</p>

### Filtragem de entrada

<p>Comando: <cod>grep OPÇÕES PADRÃO ARQUIVO</code><br>
PADRÃO: é o termo que será pesquisado em ARQUIVO</p>

#### Caracteres básicos

|caractere Regex básico|descrição|
|-|-|
|<code>.</code>|qualquer caractere único|
|<code>[ ]</code>|qualquer caractere específicado|
|<code>[^ ] </code>|não é o caractere especificado|
|<code>*</code>|zero ou mais caracteres anteriores|
|<code>^</code>|se for o primeiro caractere do padrão:<br> o padrão deve estar no inicio da linha para<br>corresponder; se não for o primeiro caractere:<br> apenas um <code>^</code> literal|
|<code>$</code>|se for o úttimo caractere do padrão:<br> o padrão deve estar no final da linha para<br> corresponder; se não for o último caractere:<br> apenas um <code>$</code> literal|

#### Expressões estendidas
<p>Devem ser usadas com comandos: <code>egrep</code> ou <code>grep -E</code></p>

|caracteres Regex extendidos|descrição|
|-|-|
|<code>+</code>|um ou mais do padrão anterior|
|<code>?</code>|o padrão anterior é opcional|
|<code>{ }</code>|especifica correspondência mínima,<br>máxima ou exata do padrão anterior|
|<code>\|</code>|alternação: um <code>OR</code> (ou) lógico|
|<code>( )</code>|criar grupos|

### Desligando: <code>shutdown OPÇÕES TEMPO MENSAGEM</code>

### Configuração de rede

|||
|-|-|
|<code>ifconfig OPÇÕES</code>|configurações de interface|
|<code>iwconfig OPÇÕES</code>|configurações wireless|
|<code>ping -c mumDePings</code>|verificar a conectividade|

### Exibindo processos: <code>ps OPÇÕES</code>

<p>Processos em execução:<br>
<code>sysadmin@localhost:~$ ps
PID TTY          TIME CMD
80 pts/0        00:00:00 bash
94 pts/0        00:00:00 ps</code></p>

<p>Exibir todos os processsos<br>
<code>sysadmin@localhost:~$ ps -e
PID TTY          TIME CMD  
1 pts/0        00:00:00 init  
33 ?            00:00:00 rsyslogd  
37 ?            00:00:00 cron  
39 ?            00:00:00 sshd  
56 ?            00:00:00 named  
69 pts/0        00:00:00 login  
79 pts/0        00:00:00 bash  
94 pts/0        00:00:00 ps</code></p>

<p>Exibir todos os processos de forma detalhada<br>
Inclui detalhes na saída do comando, como opões e argumentos<br>
<code>sysadmin@localhost:~$ ps -ef
UID        PID  PPID  C STIME TTY      TIME CMD
root         1     0  0 19:16 pts/0    00:00:00 /sbin??? /init
syslog      33     1  0 19:16 ?        00:00:00 /usr/sbin/rsyslogd
root        37     1  0 19:16 ?        00:00:00 /usr/sbin/cron
root        39     1  0 19:16 ?        00:00:00 /usr/sbin/sshd
bind        56     1  0 19:16 ?        00:00:00 /usr/sbin/named -u bind
root        69     1  0 19:16 pts/0    00:00:00 /bin/login -f
sysadmin    79    69  0 19:16 pts/0    00:00:00 -bash
sysadmin    95    79  0 19:43 pts/0    00:00:00 ps -ef</code></p>

<p>Identificadores de processo</p>

|||
|-|-|
|<code>PTD</code>|id do processo, exclusivo para cada processo|
|<code>TTY</code>|nome do terminal de execução do processo|
|<code>TIME</code>|tempo usado pelo processo|
|<code>CMD</code>|comando que iniciou o processo|

### Gerenciamento de pacotes

|||
|-|-|
|<code>dpkg</code>|gerenciamento de pacotes Debian, no nível maix baixo|
|<code>apt</code>|Advanced Package Tool, programa front-end para a ferramenta dpkg|

#### Comandos <code>apt</code>

<p>Para utilização do <code>apt</code> é recomendado o uso do comando <code>sudo</code></p>

| | |
|-|-|
| <code>sudo apt-get update</code> | atualiza a lista de pacotes disponíveis |
| <code>sudo apt-get upgrade</code> | todos os pacotes/dependências disponíveis serão atualizados |
| <code>apt-cache seach (palavra chave)</code> | procura por nome ou descrição de algum pacote |
| <code>sudo apt-get install pacote</code> | instala o pacote especificado |
| <code>sudo apt-get remove pacote</code> | Remove o pacote especificado |
| <code>sudo apt-get purge pacote</code> | limpa completamente o pacote especificado |

### Atualizar senhas

<code>passwd OPÇÕES USUÁRIO</code>

#### Exemplo do comando <code>passwd</code>

<code>sysadmin@localhost:~$ passwd -S sysadmin
sysadmin P 12/20/2017 0 99999 7 -1</code>

|||
|-|-|
|<code>-S</code>|opção que exibe o status da senha|
|<code>sysadmin</code>|nome do usuário|
|<code>P</code>|P: senha utlizavel<br>L: senha bloqueada<br>NP: não há senha|
|<code>12/20/2017</code>|última data em que a seha foi alterada|
|<code>0</code>|mínimo de dias antes que a senha possa ser alterada|
|<code>99999</code>|dias restantes para a senha expirar|
|<code>7</code>|dias antes da data de expiração que o usuário é notificado|
|<code>-1</code>|dias após a expiração da senha que a conta permanece ativa|

### Redirecionamento: <code>COMANDO > ARQUIVO</code>

<p>Redireciona a saída(STDOUT), que normalmente é o terminal, de um comando para um arquivo<br>
Exemplos:<br>
Substituir: <code>echo "conteúdo" > ARQUIVO</code>, substitui o conteúdo de ARQUIVO pelo "conteúdo" especificado<br>
Anexar: <code>echo "conteúdo" >> ARQUIVO</code>, anexa "conteúdo" ao ARQUIVO</p>

### Editor de texto

