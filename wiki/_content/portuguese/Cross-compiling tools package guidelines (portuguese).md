**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

## Contents

*   [1 Nota importante](#Nota_importante)
*   [2 Compatibilidade de versão](#Compatibilidade_de_vers.C3.A3o)
*   [3 Compilando um compilador cruzado](#Compilando_um_compilador_cruzado)
*   [4 Nomenclatura de pacote](#Nomenclatura_de_pacote)
*   [5 Colocação de arquivos](#Coloca.C3.A7.C3.A3o_de_arquivos)
*   [6 Exemplo](#Exemplo)
*   [7 Comos e por ques](#Comos_e_por_ques)
    *   [7.1 Por que não instalar em /opt?](#Por_que_n.C3.A3o_instalar_em_.2Fopt.3F)
    *   [7.2 O que é o negócio de *out-of-path executables*?](#O_que_.C3.A9_o_neg.C3.B3cio_de_out-of-path_executables.3F)
*   [8 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [8.1 O que fazer se a compilação falhar sem uma mensagem clara?](#O_que_fazer_se_a_compila.C3.A7.C3.A3o_falhar_sem_uma_mensagem_clara.3F)
    *   [8.2 O que esse erro [error message] significa?](#O_que_esse_erro_.5Berror_message.5D_significa.3F)
    *   [8.3 Por que os arquivos são instalados em lugares errados?](#Por_que_os_arquivos_s.C3.A3o_instalados_em_lugares_errados.3F)
*   [9 Veja também](#Veja_tamb.C3.A9m)

**Dica:** Como alternativa à criação de pacotes de compiladores cruzados, você poderia usar [crosstool-ng](http://crosstool-ng.org/) e criar sua própria cadeia de ferramentas de maneira totalmente automatizada. crosstool-ng pode ser encontrado em [crosstool-ng](https://aur.archlinux.org/packages/crosstool-ng/).

## Nota importante

Esta página descreve a nova maneira de fazer as coisas, inspirada nos seguintes pacotes no `[community]`:

*   [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) e outros pacotes da série `mingw-w64-*`
*   [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc) e outros pacotes da série `arm-none-eabi-*`
*   [arm-wince-cegcc-gcc](https://aur.archlinux.org/packages/arm-wince-cegcc-gcc/) e outros pacotes da série `arm-wince-cegcc-*`

## Compatibilidade de versão

**Atenção:** O uso de versões incompatíveis de pacotes para compilação da cadeia de ferramentas leva a falhas inevitáveis. Por padrão, considere **todas** versões incompatíveis.

As seguintes estratégias permitem que você selecione versões compatíveis do gcc, binutils, kernel e biblioteca C:

*   Regras gerais:
    *   existe uma correlação entre as versões gcc e binutils, use versões lançadas simultaneamente;
    *   é melhor usar os cabeçalhos mais recentes do kernel para compilar a libc, mas use o opção `--enable-kernel` (específica da glibc, outras bibliotecas C podem usar convenções diferentes) para reforçar o funcionamento em kernels mais antigos;
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"): talvez seja necessário aplicar correções adicionais e hacks, mas as versões usadas pelo Arch Linux (ou seus forks específicos de arquitetura) provavelmente podem funcionar juntas;
*   Documentação de software: todo software GNU tem arquivos `README` e `NEWS`, documentando coisas como versões mínimas exigidas de dependências;
*   Outras distribuições: elas também fazem compilação cruzada;
*   [http://clfs.org](http://clfs.org) cobre etapas necessárias para compilação de compilador cruzado e menciona versões um pouco atualizadas de dependências.

## Compilando um compilador cruzado

A abordagem geral para construir um compilador cruzado é:

1.  binutils: Compile um *cross-binutils*, que vincula e processa para a arquitetura de destino
2.  cabeçalhos: Instale um conjunto de bibliotecas C e cabeçalhos de kernel para a arquitetura de destino
    1.  use [linux-api-headers](https://www.archlinux.org/packages/?name=linux-api-headers) como referência e pesse `ARCH=*target-architecture*` para o **make**
    2.  crie um pacote de cabeçalhos libc (o processo para Glibc é descrito [aqui](http://sources.redhat.com/ml/crossgcc/2003-06/msg00170.html))
3.  gcc-stage-1: Compile um compilador cruzado gcc básico (estágio 1). Isso será usado para compilar a biblioteca C. Ele não conseguirá compilar quase nada mais (porque ele não consegue se vincular à biblioteca C que ele não tem).
4.  libc: Compile a biblioteca C "cross-compilada" (usando o compilador cruzado do estágio 1).
5.  gcc-stage-2: Compile um compilador cruzado C completo (estágio 2)

O fonte dos cabeçalhos e libc podem variar conforme a plataforma.

**Dica:** O procedimento exato varia muito, dependendo das suas necessidades. Por exemplo, se você quiser criar um "clone" de um sistema Arch Linux com as mesmas versões de kernel e glibc, você pode pular cabeçalhos de construção e passar `--with-build-sysroot=/` para o `configure`.

## Nomenclatura de pacote

O nome do pacote **não** deve ser prefixado com a palavra `cross-` (foi proposto anteriormente, mas não foi adotado em pacotes oficiais, provavelmente devido ao comprimento adicional de nomes), e consistirá do nome do pacote, prefixado por [trio GNU](https://wiki.debian.org/Multiarch/Tuples "debian:Multiarch/Tuples") sem campo de fornecedor ou com "desconhecido" no campo do fornecedor; exemplo: `arm-linux-gnueabihf-gcc`. Se houver uma convenção de nomenclatura mais curta (por exemplo, `mips-gcc`), ela poderá ser usada, mas isso não é recomendado.

## Colocação de arquivos

As versões mais recentes do gcc e do binutils usam caminhos não conflitantes para sysroot e bibliotecas. Os executáveis devem ser colocados em `/usr/bin/`, para evitar conflitos aqui, prefixar todos eles com o nome da arquitetura.

Geralmente, `./configure` teria pelo menos os seguintes parâmetros:

```
_target=<seu-alvo> # p. ex., i686-pc-mingw32
_sysroot=/usr/lib/${_target}
...
./configure \
    --prefix=${_sysroot} --sysroot=${_sysroot} \
    --bindir=/usr/bin
```

## Exemplo

Esse é o PKGBUILD do binutils para MinGW. Coisas interessantes de se observar são:

*   especificar o diretório raiz do ambiente cruzado
*   o uso de variáveis `${_pkgname}` , `${_target}` e `${_sysroot}` para fazer o código mais legível
*   remoção de arquivos duplicados/conflitantes

```
# Maintainer: Allan McRae <allan@archlinux.org>

# cross toolchain build order: binutils, headers, gcc (pass 1), w32api, mingwrt, gcc (pass 2)

_target=i686-pc-mingw32
_sysroot=/usr/lib/${_target}

pkgname=${_target}-binutils
_pkgname=binutils
pkgver=2.19.1
pkgrel=1
pkgdesc="MinGW Windows binutils"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/binutils/"
license=('GPL')
depends=('glibc>=2.10.1' 'zlib')
options=('!libtool' '!distcc' '!ccache')
source=(http://ftp.gnu.org/gnu/${_pkgname}/${_pkgname}-${pkgver}.tar.bz2)
md5sums=('09a8c5821a2dfdbb20665bc0bd680791')

build() {
  cd ${srcdir}/${_pkgname}-${pkgver}
  mkdir binutils-build && cd binutils-build

  ../configure --prefix=${_sysroot} --bindir=/usr/bin \
    --with-sysroot=${_sysroot} \
    --build=$CHOST --host=$CHOST --target=${_target} \
    --with-gcc --with-gnu-as --with-gnu-ld \
    --enable-shared --without-included-gettext \
    --disable-nls --disable-debug --disable-win32-registry
  make
  make DESTDIR=${pkgdir}/ install

  # clean-up cross compiler root
  rm -r ${pkgdir}/${_sysroot}/{info,man}
}

```

**Nota:** Durante a compilação de cadeia de ferramentas cruzadas sempre execute os comandos `configure` e **make** a partir do diretório dedicado (chamada compilação fora da árvore) e remova todo o diretório `src` após a menor mudar em [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)").

## Comos e por ques

### Por que não instalar em `/opt`?

Dois motivos:

1.  Primeiro, de acordo com o File Hierarchy Standard, esses arquivos pertencem apenas a um lugar no `/usr`.
2.  Em segundo lugar, a instalação em `/opt` é a última medida quando não há outra opção.

### O que é o negócio de *out-of-path executables*?

Essa coisa estranha facilita a compilação cruzada. Às vezes, os Makefiles do projeto não usam `CC` e outras variáveis e, em vez disso, usam *'gcc'* diretamente. Se você quiser apenas tentar compilar esse projeto, a edição do Makefile pode ser uma operação muito demorada. No entanto, alterar o `$PATH` para usar "nossos" executáveis primeiro é uma solução muito rápida. Você então executaria `PATH=/usr/*arch*/bin/:$PATH make` em vez de `make`.

## Solução de problemas

### O que fazer se a compilação falhar sem uma mensagem clara?

Para um erro ocorrido durante a execução do `configure`, leia `$srcdir/*pkgname*-build/config.log`. Para erro ocorrido durante compilação, role o log do console ou pesquise pela palavra "error".

### O que esse erro [error message] significa?

Muito provavelmente você fez algum dos erros não óbvios:

*   Muitos ou poucos sinalizadores de configuração. Tente usar um conjunto já comprovadamente correto de sinalizadores.
*   As dependências estão corrompidas. Por exemplo, arquivos de binutils perdidos ou colocados no lugar errado podem resultar em erros ocultos durante a configuração do gcc.
*   Você não adicionou `export CFLAGS=""` à sua função `build()` (veja [bug 25672](http://gcc.gnu.org/bugzilla/show_bug.cgi?id=25672) no Bugzilla do GCC).
*   Algumas combinações `--prefix`/`--with-sysroot` podem exigir que diretórios sejam graváveis (não óbvias em guias de clfs).
*   sysroot ainda não tem cabeçalhos de kernel/libc.
*   Se google-fu não ajudar, abandone imediatamente sua configuração atual e tente uma mais estável e de funcionamento confirmado.

### Por que os arquivos são instalados em lugares errados?

Vários métodos de execução da linha genérica `make install` acabam em resultados diferentes. Por exemplo, alguns destinos de make podem não fornecer suporte a `DESTDIR` e, em vez disso, requerem o uso de `install_root`. O mesmo para `tooldir`, `prefix` e outros argumentos semelhantes. Às vezes, fornecendo parâmetros como argumentos em vez de variáveis de ambiente, p. ex.

```
./configure CC=arm-elf-gcc

```

em vez de

```
CC=arm-elf-gcc ./configure

```

e vice-versa pode resultar em resultados diferentes (geralmente causados por auto-invocação recursiva de configure/make).

## Veja também

[http://wiki.osdev.org/GCC_Cross-Compiler](http://wiki.osdev.org/GCC_Cross-Compiler)