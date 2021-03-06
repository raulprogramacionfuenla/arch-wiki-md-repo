**Status de tradução:** Esse artigo é uma tradução de [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines"). Data da última tradução: 2019-01-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=AUR_Trusted_User_Guidelines&diff=0&oldid=562395) na versão em inglês.

Artigos relacionados

*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")

O **Trusted User (TU)** ("Usuário confiado") é um membro da comunidade encarregado de manter o AUR funcionando. Ele/Ela mantém pacotes populares ([comunicando com o *upstream* e enviando-o patches quando necessário](https://mailman.archlinux.org/pipermail/aur-general/2010-September/010649.html)) e vota em assuntos administrativos. Um TU é eleito de membros ativos da comunidade pelos atuais TUs em um processo democrático. TUs são os únicos membros que têm a última palavra na direção do AUR.

Os TUs são governados usando as [TU bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html) ("Estatuto dos TUs")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Lista de tarefas para novos Trusted Users](#Lista_de_tarefas_para_novos_Trusted_Users)
*   [2 O TU e o AUR](#O_TU_e_o_AUR)
    *   [2.1 Reescrevendo histórico Git](#Reescrevendo_histórico_Git)
*   [3 O TU e [community], Diretrizes para Manutenção de Pacotes](#O_TU_e_[community],_Diretrizes_para_Manutenção_de_Pacotes)
    *   [3.1 Regras para a Entrada de Pacotes no Repositório [community]](#Regras_para_a_Entrada_de_Pacotes_no_Repositório_[community])
    *   [3.2 Acessando e Atualizando o Repositório](#Acessando_e_Atualizando_o_Repositório)
    *   [3.3 Abandonando pacotes](#Abandonando_pacotes)
    *   [3.4 Movendo pacotes do unsupported para [community]](#Movendo_pacotes_do_unsupported_para_[community])
    *   [3.5 Movendo pacotes do [community] para unsupported](#Movendo_pacotes_do_[community]_para_unsupported)
    *   [3.6 Movendo pacotes do [community-testing] para [community]](#Movendo_pacotes_do_[community-testing]_para_[community])
    *   [3.7 Excluindo pacotes do unsupported](#Excluindo_pacotes_do_unsupported)
    *   [3.8 Compilação remota no PKGBUILD.com](#Compilação_remota_no_PKGBUILD.com)
*   [4 Lista de TODO na retirada de um Trusted User](#Lista_de_TODO_na_retirada_de_um_Trusted_User)
*   [5 Veja também](#Veja_também)

## Lista de tarefas para novos Trusted Users

1.  Ler este artigo de wiki por completo.
2.  Ler as [TU Bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html).
3.  Certificar-se de que os detalhes da sua conta no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") estejam atualizados.
4.  Adicionar a si próprio à página de [Trusted Users](/index.php/Trusted_Users "Trusted Users").
5.  Se inscrever na lista de discussão pública de desenvolvimento do Arch Linux, [arch-dev-public](https://lists.archlinux.org/listinfo/arch-dev-public).
6.  Lembrar um [administrador do BBS](https://bbs.archlinux.org/userlist.php?username=&show_group=1&sort_by=username&sort_dir=ASC&search=Submit) de alterar sua conta nos fóruns.
7.  Perguntar a algum TU pela chave do #archlinux-tu@freenode e se fazer presente no canal. Você não tem que fazer isso, mas seria interessante já que é lá que a maioria dos segredos ocultos são apresentados e é onde muitas novas ideias são concebidas.
    *   Se você precisar de um bouncer, peça ao heftig por um convite de [Matrix](/index.php/Matrix "Matrix") ou execute `givemequassel` no servidor *soyuz.archlinux.org*, então autentique-se usando [Quassel](/index.php/Quassel "Quassel").
    *   Uma vez no canal, se você quiser uma manta de @archlinux/trusteduser/*, peça ao nosso [contato no grupo](https://freenode.net/groupreg#two-types-of-group-contacts-exist-for-freenode), ioni, para obter uma.
8.  Criar uma chave PGP para [assinatura de pacotes](/index.php/Assinatura_de_pacote "Assinatura de pacote") ou usar sua chave PGP existente. Certifique-se de que a chave também contém uma subchave criptográfica de forma você possa receber tokens de verificação criptografados.
9.  Enviar um e-mail assinado para Florian Pritz (bluewind@xinu.at) ou Bartłomiej Piotrowski (bpiotrowski@archlinux.org):
    *   Anexar uma chave pública SSH. Se você não possuir uma, use `ssh-keygen` para gerar uma. Verifique na página wiki [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") para mais informações sobre chaves SSH.
    *   Solicitar que ele lhe dê permissão à arch-dev-public.
    *   Falar para ele se você deseja um e-mail @archlinux.org.
    *   Nome de usuário e endereço de e-mail preferidos cuja senha inicial deve ser enviada para ter acesso na interface dev (archweb). Se você já tem uma conta, peça para ser adicionado ao grupo de Trusted Users.
10.  Pedir a seu patrocinador (*sponsor*):
    *   para lhe conceder o status de TU no AUR.
    *   para abrir uma nova tarefa no projeto "Keyring" do rastreador de erro seguindo as instruções [nesta mensagem](https://lists.archlinux.org/pipermail/arch-dev-public/2013-September/025456.html) na ordem de ter sua chave PGP assinado pelos três detentores de chave mestre.
11.  Instalar o pacote [devtools](https://www.archlinux.org/packages/?name=devtools).
12.  [Configurar sua chave privada ssh](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Autenticação "Arch User Repository (Português)") para os servidores `orion.archlinux.org` e `repos.archlinux.org`.
13.  Testar a conexão SSH para seunome@orion.archlinux.org (assim que você tiver permissões).
14.  Se você não for promovido a um grupo de Trusted User no rastreador de erro em dois dias, relate isso como um bug para arch-dev-public.
15.  Começar a contribuir!

## O TU e o AUR

Os TUs deveriam também fazer um esforço para verificar o envio de pacotes no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") por códigos maliciosos e o correto seguimento dos padrões dos PKGBUILD. Em cerca de 80% dos casos, os PKGBUILDs no UNSUPPORTED são muito simples e podem ter rapidamente verificadas a sanidade e os códigos maliciosos pela equipe de TUs.

Os TUs devem também verificar os PKGBUILDs por pequenos erros, sugerir correções e melhoras. O TU deve se tentar certificar-se de que todos os pacotes sigam Arch Packaging Guidelines/Standards (Diretrizes/Padrões de Empacotamento do Arch) e ao fazer isso, compartilhar suas habilidades com outros criadores de pacotes em um esforço em criar um padrão de criação de pacotes por toda a distribuição.

Os TUs também estão em uma posição de documentar práticas recomendadas.

### Reescrevendo histórico Git

Em alguns casos, é necessário reescrever o histórico de um repositório do AUR, por exemplo, quando um usuário inadvertidamente usa seu nome real em um commit publicado. Isso pode ser automatizado com [git-filter-branch(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-filter-branch.1).

Para realizar um push forçado para um novo histórico, encaminhe a variável de ambiente `AUR_OVERWRITE=1` para o [git-push(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-push.1). Veja [[1]](https://git.archlinux.org/aurweb.git/commit/?id=c5302d3a33028f483cc2e01225226d4ae047dd4a) para detalhes.

**Atenção:** É recomendado criar um backup do repositório antes de reescrever o histórico.

	Modificar a identidade do committer ou autor

Use `git filter-branch --env-filter` com as [variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente") `GIT_AUTHOR_NAME`, `GIT_AUTHOR_EMAIL`, `GIT_COMMITTER_NAME` and `GIT_COMMITTER_EMAIL`. Por exemplo:

```
git filter-branch --env-filter '
if test "$GIT_AUTHOR_EMAIL" = "lepetit@prince.com"; then
  GIT_AUTHOR_EMAIL=user@users.noreply.github.com
fi
if test "$GIT_AUTHOR_NAME" = "Antoine de Saint-Exupéry"; then
  GIT_AUTHOR_NAME=user
fi'
```

**Nota:** [git-log(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-log.1) só exibe o *author* git por padrão. Use `git log --pretty=fuller` para exibir o *author* e o *committer*.

## O TU e [community], Diretrizes para Manutenção de Pacotes

### Regras para a Entrada de Pacotes no Repositório [community]

*   Um pacote não pode já existir em qualquer um dos repositórios do Arch Linux. você deve tomar os cuidados necessários para se certificar que nenhum outro empacotador está no processo de promoção do mesmo pacote. Veja os comentários do pacote do AUR, leia os últimos títulos de assuntos no [aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general), pesquise [todos os projetos no rastreador de erro](https://bugs.archlinux.org/index.php?project=0&do=index&switch=1), use [grep](https://en.wikipedia.org/wiki/Grep "wikipedia:Grep") no [log do Subversion](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.log.html) e envie uma mensagem rápida para o [canal IRC](/index.php/Canal_IRC "Canal IRC") privado de TUs.

*   Auxiliares do AUR, como uma exceção especial, nunca serão permitidos.

*   Somente pacotes "populares" podem entrar no repositório, sendo definido pelo 1% de uso no [pkgstats](https://www.archlinux.de/?page=PackageStatistics) ou 10 votos no AUR.

*   Exceções automáticas a esta regra são:
    *   pacotes de internacionalização (i18n)
    *   pacotes de acessibilidade
    *   drivers
    *   dependências de pacotes que satisfazem a definição de populares, incluindo **makedeps** e **optdeps**
    *   pacotes que são parte de uma coleção e têm a intenção de ser distribuídos juntos, fornecendo uma parte da coleção satisfaz a definição de popular

*   Quaisquer adições não cobertas por nenhum dos critérios acima devem ser propostas na lista de discussão aur-general, explicando o motivo para a dispensa (ex.: pacote renomeado, novo pacote). O acordo de três outros TUs é necessário para que o pacote seja aceito na [community]. Adições propostas por TUs com grande número de pacotes "não-populares" provavelmente serão rejeitadas.

*   Os TUs são incentivados a mover os pacotes mantidos do [community], se eles tiverem baixo uso. Nenhuma aplicação será necessária, apesar de que a renúncia de pacotes de TUs pode ser filtrada antes que ocorra adoção.

*   É uma boa prática sempre incrementar o **pkgrel** em *1* (em outras palavras, defina o para *n + 1*) ao promover um pacote do AUR. Isso é para facilitar atualizações automáticas para aqueles que já têm o pacote instalado, de forma que eles podem continuar a receber atualizações a partir do canal oficial. Um outro efeito positivo disto é que usuários não são avisados que sua cópia local é mais nova, como é o caso se um empacotador redefinir o **pkgrel** para *1*.

### Acessando e Atualizando o Repositório

O repositório [community] agora usa **devtools**, que é o mesmo sistema usado para enviar pacotes para o [core] e [extra], apesar de usar outro servidor `nymeria.archlinux.org` ao invés de `gerolde.archlinux.org`. Por isso, a maioria das instruções no [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") funciona sem qualquer outro comentário. Informações que são específicas para o repositório [community] (como URLs alteradas) foram inseridas aqui. O devtools exige que os empacotadores [definam a variável PACKAGER](/index.php/Makepkg_(Portugu%C3%AAs)#Informação_do_empacotador "Makepkg (Português)") no `makepkg.conf`.

Inicialmente, você deve fazer um **checkout não-recursivo** do repositório [community]: svn checkout -N svn+ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn svn-community

Isso cria um diretório chamado "svn-community" contendo nada, além de uma pasta ".svn".

Para realizar **checkout**, **atualizar** todos os pacotes ou **adicionar** um pacote, veja o [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager").

Para **remover** um pacote:

```
ssh orion.archlinux.org /community/db-remove community arch pkgname

```

Aqui e no texto seguinte, *arch* pode ser *i686* ou *x86_64*, que são as duas arquiteturas às quais o Arch Linux oferece suporte.

**Nota:** Se você está editando pacotes da arquitetura *any*, você pode executar os scripts x64 que também vão funcionar.

Quando você tiver finalizado a edição do PKGBUILD, etc, você deve fazer um **commit** das alterações (`svn commit`).

Compile o pacote com `mkarchroot` ou os scripts auxiliares `extra-i686-build` e `extra-x86_64-build`. Se você deseja enviar para *testing*, você também precisará compilar com os scripts de teste `testing-i686-build` e `testing-x86_64-build`.

Assine o pacote com `gpg --detach-sign *.pkg.tar.xz`. Se você está usando uma chave PGP diferente para assinatura de pacote, você pode adicioná-la ao `~/.makepkg.conf` com `GPGKEY=<identifier>`.

Quando você quiser publicar (**release**) um pacote, primeiro copie o pacote junto com sua assinatura para o diretório *staging/community* no *orion.archlinux.org* usando `scp` e, então, marque (**tag**) o pacote no diretório *pkgname/trunk* e chamando `archrelease community-arch`. Isso faz uma cópia svn das entradas do trunk em um diretório chamado *community-i686* ou *community-x86_64* indicando que este pacote está no repositório *community* para aquela arquitetura. Note que o diretório *staging* é diferente do repositório *staging* e todo pacote precisa ser enviado para o diretório *staging*. Esse processo pode ser automatizado com o script `communitypkg`. Veja o resumo abaixo.

***Nota:** Em alguns casos, especialmente para pacotes do [community], um TU de x86_64 pode incrementar o pkgrel por .1 (e não por +1). Isso indica que a alteração do PKGBUILD é especificamente de x86_64 e mantenedores de i686 **não devem** recompilar o pacote para i686\. Quando o TU decide incrementar o pkgrel, isso deveria ser feito com o acréscimo normal de +1\. Porém, um pkgrel=2.1 anterior não deve se tornar pkgrel=3.1 quando incrementado pelo TU e deve ser pkgrel=3\. Em resumo, mantenha os lançamentos com ponto (.) exclusivamente para TUs de x86_64 para evitar confusão.*

**Resumo da atualização de pacote:**

*   **Atualizar** o diretório de pacote (`svn update algum-pacote`)
*   **Mudar** para o diretório trunk do pacote (`cd algum-pacote/trunk`)
*   **Editar** o PKGBUILD, fazer alterações necessárias, atualizar o checksums com `updpkgsums`.
*   **Compilar** o pacote: com `makechrootpkg` ou `extra-i686-build` e `extra-x86_64-build`. É **obrigatório** compilar em um [*chroot* limpo](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot").
*   **[Namcap](/index.php/Namcap_(Portugu%C3%AAs) "Namcap (Português)")** no PKGBUILD e no binário `pkg.tar.gz`.
*   **Commit**, **Copiar** e **Tag** o pacote usando `communitypkg "mensagem de commit"`. Isso automatiza o seguinte:
    *   Fazer **commit** das alterações no trunk: `svn commit`.
    *   **Assinar** o pacote: `gpg --detach-sign *.pkg.tar.xz`.
    *   **Copiar** o pacote e sua assinatura para *orion.archlinux.org*: `scp *.pkg.tar.xz *.pkg.tar.xz.sig orion.archlinux.org:staging/community/`.
    *   Aplicar um **tag** do pacote: {{ic|archrelease community-{i686,x86_64}}}.
*   **Atualizar** o repositório: `ssh orion.archlinux.org /community/db-update`.

Veja também a seção de *Miscelânia* no [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") and [SSH keys#ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys"). Para a seção *Avoid having to enter your password all the time* ("evite de precisar digitar sua senha toda vez"), use *orion.archlinux.org* em vez do *gerolde.archlinux.org*.

### Abandonando pacotes

Se um TU não pode ou não quer mais manter um pacote, um aviso deve ser postado na Lista de Discussão do AUR, para que outro TU possa mantê-lo. Um pacote pode ainda ser abandonado mesmo se nenhum outro TU quiser mantê-lo, mas os TUs devem evitar de deixar muitos pacotes soltos (eles não deveriam manter mais do que possam dar conta). Se um pacote se tornou obsoleto ou não é mais usado, ele também pode ser completamente removido.

Se um pacote foi removido completamente, o mesmo pode ser enviado novamente (do zero) para o UNSUPPORTED, onde um usuário normal pode manter o pacote ao invés de um TU.

### Movendo pacotes do unsupported para [community]

Siga os procedimentos normais para adição de um pacote ao [community], mas lembre-se de remover o pacote correspondente do *unsupported*!

### Movendo pacotes do [community] para unsupported

Remova o pacote usando as instruções acima e envie o seu tarball fonte para o AUR.

### Movendo pacotes do [community-testing] para [community]

```
$ ssh repos.archlinux.org /community/db-move community-testing community <pacote>

```

### Excluindo pacotes do unsupported

Não há sentido em remover pacotes-modelos, porque eles serão recriados na tentativa de atender dependências. Se alguém enviar um pacote real, então todos os dependentes irão apontar para o local correto.

### Compilação remota no PKGBUILD.com

**Atenção:** Os procedimentos a seguir invalidam o modelo Web Of Trust: um usuário com acesso root ao PKGBUILD.com poderia alterar o pacote e/ou a assinatura antes de publicá-lo.

Trusted Users e desenvolvedores podem se conectar ao [PKGBUILD.com](http://pkgbuild.com/) via SSH para, entre outros, criar pacotes usando o devtools. Isso tem diversas vantagens sobre a configuração local:

*   Compilações são rápidas e a velocidade de rede é alta.
*   O ambiente precisa ser configurado apenas uma vez.
*   Seu sistema local não precisa ser Arch Linux.

O processo é semelhante ao de uma configuração local com devtools. Seu GnuPG privado é necessário para assinar, mas você não quer enviá-lo para soyuz por razões óbvias de segurança. Como tal, você precisará encaminhar o soquete de agente do GnuPG de sua máquina local para o servidor: isso permitirá que você assine pacotes em soyuz sem comunicar sua chave. Isso também significa que precisamos desabilitar o agente no servidor antes de podermos executar qualquer coisa.

Primeiro, conecte-se ao soyuz e desabilite-o:

```
 $ ssh soyuz.archlinux.org
 $ systemctl --user mask gpg-agent.service

```

Certifique-se de que o gpg-agent não esteja em execução (`systemctl --user stop gpg-agent.service`). Neste ponto, certifique-se de que não existem soquetes na pasta apontada por `gpgconf --list-dir socketdir`. Em caso afirmativo, remova-os ou efetue o logout e novamente. Se você tem um $GNUPGHOME personalizado (por exemplo, para movê-lo para `~/.config/gnupg`), você precisará desmarcar isso, pois não é possível no gnupg definir o homedir sem configurar o socketdir. No soyuz, *StreamLocalBindUnlink yes* está definido no *sshd_config*, então remover os soquetes manualmente no logout não é necessário.

Enquanto as chaves privadas PGP permanecem em sua máquina local, as chaves públicas **devem** estar no soyuz. Exportar sua chave público para soyuz, por exemplo da sua máquina local

```
 $ scp ~/.gnupg/pubring.gpg soyuz.archlinux.org:~/.gnupg/pubring.gpg

```

O SSH é necessário para fazer *checkout* e *commit* no repositório SVN. Você pode configurar um novo par de chaves SSH no servidor (é altamente desencorajado colocar sua chave privada local no soyuz por motivos de segurança) ou reutilizar as chaves locais por meio do encaminhamento de soquete. Se você optar por este último, certifique-se de desabilitar o ssh-agent no soyuz se você o habilitou anteriormente (ele não está em execução por padrão).

Configure seu ambiente de compilação no soyuz:

 `~/.makepkg.conf` 
```
PACKAGER="John Doe <john@doe.example>"
## Opcional
PKGDEST="/home/johndoe/packages"
SRCDEST="/home/johndoe/sources"
SRCPKGDEST="/home/johndoe/srcpackages"
LOGDEST="/home/johndoe/logs"
## Se sua chave PGP não é a padrão, especifique a impressão digital correta:
GPGKEY="ABCD1234..."
```

**Atenção:** Encaminhar seu soquete gpg-agent para uma máquina remota possibilita que qualquer pessoa com acesso root a esse sistema use suas credenciais GPG desbloqueadas. Para contornar esse problema, precisamos desabilitar o armazenamento em cache da frase secreta.

desabilite o cache de senha com as seguintes configurações:

 `gpg-agent.conf` 
```
default-cache-ttl 0
max-cache-ttl 0

```

Como desejaremos manter nosso agente GPG normal em execução com suas configurações atuais, executaremos outro agente GPG dedicado à tarefa em questão. Crie uma pasta `~/.gnupg-archlinux` e crie uma ligação simbólica de `~/.gnupg`, exceto `~/.gnupg/gpg-agent.conf`. Configure o novo agente GPG:

 `~/.gnupg-archlinux` 
```
extra-socket /home/doe/.gnupg-archlinux/S.gpg-agent.extra
default-cache-ttl 0
max-cache-ttl 0
pinentry-program /usr/bin/pinentry-gtk-2

```

O `gpg-agent-extra.socket` será encaminhado para PKGBUILD.com.

Inicie o agente dedicado com:

```
 $ gpg-agent --homedir ~/.gnupg-archlinux --daemon

```

Conecte-se com:

```
 $ ssh -R $REMOTE_SSH_AUTH_SOCK:$SSH_AUTH_SOCK -R /run/user/$REMOTE_UID/gnupg/S.gpg-agent:/home/doe/.gnupg-archlinux/S.gpg-agent.extra soyuz.archlinux.org

```

ou, se estiver usando GnuPG como seu agente SSH, com:

```
 $ ssh -R /run/user/$REMOTE_UID/gnupg/S.gpg-agent.ssh:/run/user/$LOCAL_UID/gnupg/S.gpg-agent.ssh -R /run/user/$REMOTE_UID/gnupg/S.gpg-agent:/home/doe/.gnupg-archlinux/S.gpg-agent.extra soyuz.archlinux.org

```

Substitua *$REMOTE_UID* e *$LOCAL_UID* pelo seu identificador de usuário como retornado por `id -u` no soyuz e localmente, respectivamente. Se estiver usando ssh-agent, substitua *$REMOTE_SSH_AUTH_SOCK* pelo caminho para o soquete SSH no host remoto (pode ser qualquer coisa).

Você pode tornar o encaminhamento permanente para esse host. Por exemplo, com gpg-agent.ssh:

 `~/.ssh/config` 
```
Host soyuz.archlinux.org
  RemoteForward /run/user/$REMOTE_UID/gnupg/S.gpg-agent /run/user/$LOCAL_UID/gnupg/S.gpg-agent.extra
  RemoteForward /run/user/$REMOTE_UID/gnupg/S.gpg-agent.ssh /run/user/$LOCAL_UID/gnupg/S.gpg-agent.ssh

```

Novamente, substitua *$REMOTE_UID* e *$LOCAL_UID* pelos seus respectivos valores.

A partir de então, o procedimento deve ser exatamente igual a uma compilação local:

```
 $ ssh soyuz.archlinux.org
 $ svn checkout -N svn+[ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn](ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn) svn-community
 $ ...

```

**Nota:** pinentry-curses pode não funcionar com encaminhamento de soquete. Se ele falhar para você, tente usar um pinentry diferente.

## Lista de TODO na retirada de um Trusted User

Quando um TU renuncia, a seguinte lista tem que ser seguida -- essas etapas não se aplicam quando um TU renuncia, mas ainda é um desenvolvedor.

1.  Todos os pacotes empacotados pelo TU retirado devem ser resignados (portanto, recompilados). Pacotes empacotados pelo retirado podem ser localizados no Archweb [https://www.archlinux.org/packages/?sort=&q=&empacotador=$empacotador&flagged=](https://www.archlinux.org/packages/?sort=&q=&empacotador=$empacotador&flagged=), sendo empacotador o nome de usuário no Archweb.
2.  A conta do retirado deve ser desabilitada no Archweb e adicionada ao grupo "Retired Trusted users". O retirado deve ser removido dos "Trusted Users" e as permissões de repositório devem ser reduzidas a zero.
3.  O acesso shell a nossos servidores devem ser desabilitados. (especialmente repos.archlinux.org, pkgbuild.com)
4.  A chave GPG deve ser removida e um novo pacote [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) deve ser enviado para os repositórios. Crie um relatório de erro no projeto do chaveiro para remover as chaves dos Trusted Users retirados.
5.  Remova o grupo de TU de suas contas AUR.

## Veja também

*   [Diretrizes de Empacotamento](/index.php/DeveloperWiki#Packaging_Guidelines "DeveloperWiki")