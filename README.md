# Modelo em Latex para Projeto Final com Glossários Automáticos e Macros

*Disclaimer: a maneira de fazer o glossário automático funcionar mostrado aqui é apenas uma das maneiras possíveis, cada um faz do jeito que acha melhor e todo mundo pode ser feliz. Também só testei no Windows usando TeXstudio, não sei se em Linux é mais fácil ou mais difícil.*


O modelo aqui presente é inspirado no que está no site do [DEL](https://www.del.ufrj.br/atividades/graduacao/eletronica-e-computacao/projetos-finais/modelos-de-documentos/).


## O que temos a acrescentar?

 1. `myMacros.sty`
 
 Que permite a escrita de símbolos matemáticos de maneira bem mais simples. O uso das macros é bem intuitivo. Exemplo do uso das macros está presente na seção **1.1 Notation**. Modificações no próprio arquivo podem ser feitas para melhor atender as necessidades de cada um. 

Certifique-se que **\usepackage{myMacros}** está adicionado ao **TesePack.tex** e que o arquivo **myMacros.sty** está no repositório do projeto.

2. `Glossários`

Os glossários permitem a confecção de listas de abrevituras/acrônimos e lista de símbolos de maneira muito mais prática.

**Como fazer os glossários funcionarem?**

 - Instalar a versão completa do [Perl](https://www.perl.org/get.html).
 - Configurar os comandos do TeXstudio.
Option -> Configure TeXstudio -> Commands:


**Makeindex** 
"C:/Users/user/AppData/Local/Programs/MiKTeX 2.9/miktex/bin/x64/makeindex.exe" %.idx


**Texindy**
"C:/Users/user/AppData/Local/Programs/MiKTeX 2.9/miktex/bin/x64/texindy.exe" %.idx


**Makeglossaries**
"C:/Users/user/AppData/Local/Programs/MiKTeX 2.9/miktex/bin/x64/makeglossaries.exe" %

(agora não tenho certeza se essa última parte é realmente necessária, mas acho que sim. E cada computador vai ter um **caminho diferente** pro MiKTeX [tô assumindo que tá todo mundo usando o MiKTeX]).

 - Colocar os pacotes necessários no TesePack.tex

Aqui vamos fazer dois glossários: List of Symbols e List of Abbreviations.

Pacote no **TesePack.tex**
\usepackage[toc,acronym]{glossaries}

Também incluir:
\newglossary[syg]{symbols}{syb}{sbs}{Symbols} 
\makeglossaries

Para o List of Abbreviations, temos no Principal.tex

\cleardoublepage
\printglossary[type=\acronymtype,nonumberlist,title=List of Abbreviations]

Para o List of Symbols
\glsaddall
\printglossary[type=symbols,nonumberlist,title=List of Symbols]

Estas são as declarações necessárias no `Principal.tex` para que eles sejam exibidos em forma de lista. 

O \glsaddall é usado para adicionar todos os símbolos que eu adicionar no `abbreviations.tex` (lugar que eu usei para declarar os acrônimos e os símbolos, você pode criar arquivos separados para cada um, mas lembre-se de dar include do arquivo no Principal.tex) e não necessariamente eu preciso usar o símbolo durante o texto para que ele apareça na lista de símbolos.

 - Adicionar os acrônimos e símbolos.
 
 Para os acrônimos aparecerem na lista, eles tem que ser usados no texto (isso é regra minha, você pode usar o \glsaddall para aparecem de qualquer forma). 

No exemplo temos em `abbreviations.tex`:

% ACRONYM
\newacronym{awgn}{AWGN}{\textit{additive white Gaussian noise}}

% SYMBOLS
\newglossaryentry{not:alphaac}{type=symbols,name={$\alpha_{\textrm{ac}}$},description={Absorption coefficient},sort={a}}

 - Compilar, comando do glossário, compilar novamente.
 
 Essa parte pode parecer um pouco chata, mas para os glossários aparecerem você geralmente tem que compilar, depois ir no comando Tools -> Commands -> Makeglossaries e depois compilar novamente.

**Com certeza tem alguma maneira de fazer isso automaticamente, mas eu não consegui fazer funcionar ainda. Se alguém souber, me fala.**

Pronto, temos:

![List of Abbreviations](https://i.imgur.com/lJ1wO2f.jpg)

![List of Symbols](https://i.imgur.com/q6CJ1Ad.jpg)
