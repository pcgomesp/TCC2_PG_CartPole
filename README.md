# template-tcc-latex-univasf [![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat-square)](https://github.com/Gabrielr2508/template-tcc-latex-univasf/issues) [![HitCount](http://hits.dwyl.io/Gabrielr2508/template-tcc-latex-univasf.svg)](http://hits.dwyl.io/Gabrielr2508/template-tcc-latex-univasf)

Template em Latex para TCC do curso de Engenharia de Computação da Univasf.

[Aqui](https://github.com/ruanmed/form-mat-tcc-cecomp) encontra-se o template em LaTeX para Formulário de Matrícula de TCC do curso de Engenharia de Computação.

Você pode consultar exemplos de TCCs elaborados com esse template em [nossa biblioteca](https://github.com/caecom/lib-tccs).

Dicas sobre como estruturar o documento e utilizar as características
do template estão comentadas ao longo do código, bem como podem ser observadas
no produto final, o [documento](https://github.com/Gabrielr2508/template-tcc-latex-univasf/blob/feature/documentation/main.pdf).

# Instruções de como executar e construir o seu documento

## GNU/Linux (linha de comando)

### Instalação do LaTeX

a execução dos comandos de _build_ do projeto dependem da prévia instalação
do LaTeX no sistema. No caso de distribuições GNU/Linux, isso geralmente se traduz
na instalação do pacode texlive, utilizando o gerenciador de pacotes da distribuição:

- Archlinux
  consulte a [documentação](https://wiki.archlinux.org/index.php/TeX_Live)
- distribuições baseadas no Debian
  consulte a [documentação](https://wiki.debian.org/Latex)
- distribuições baseadas no Red Hat
  consulte a [documentação](https://fedoraproject.org/wiki/Features/TeXLive)

Geralmente, isso se traduz em executar um comando como o mostrado abaixo, para
o caso do Archlinux:

```shell-session
$ sudo pacman -S texlive-core
```

ou

```
$ sudo apt install texlive
```

Para que a extensão minted (utilizada nos códigos fontes) possa ser utilizada
é necessário utilizar o [pygments](http://pygments.org), uma biblioteca do Python,
que pode ser instalada através do `pip` (um gerenciador de pacotes do Python), como
mostrado abaixo

```shell-session
$ pip install pygments
```

Na maior parte das principais distribuições GNU/Linux, isso também
pode ser feito utilizando-se o gerenciador de pacotes da sua distribuição,
como mostrado abaixo, para o caso do archlinux

```shell-session
$ sudo pacman -S python-pygments
```

### Compilando o documento

Para compilar o projeto, basta executar as linhas a seguir

```shell-session
$ pdflatex -shell-escape main.tex
$ bibtex main.aux
$ pdflatex -shell-escape main.tex
$ pdflatex -shell-escape main.tex
```

O argumento `-shell-escape` é necessário para que o _plugin_ utilizado [(minted)](https://github.com/gpoore/minted)
na geração dos _snippets_ de código possa ser executado.

Alternativamente, o script `build.sh` pode ser executado, ele aceita como parâmetro
opcional o nome do arquivo principal, assumido como padrão o `main.tex`

## MS-Windows (TexMaker)

### Instalando o TexMaker

A instalação do TexMaker no Windows é simples. Acesse o site [Download TexMaker](http://www.xm1math.net/texmaker/download.html) faça o _download_ do executável e proceda com a instalação.

Ao executar o TexMaker lembre-se de sempre fazê-lo com o modo Administrador.

### Configurando o TexMaker

Com o editor aberto, vamos configurá-lo:

1. Clique em **Opções > Configurar o Texmaker**
1. Na aba **Comandos** substitua texto do campo **PdfLaTeX** pelo comando:
   > pdflatex -synctex=1 -interaction=nonstopmode --shell-escape %.tex
1. Na aba **Compilar** em **Comandos de compilação rápida** selecione a **segunda** opção:
   > PdfLaTeX + Bib(la)tex + PdfLaTeX (x2) + View Pdf
1. Clique em **Ok**

Pronto! O TexMaker está configurado.

### Compilando com o TexMaker

Para compilar o projeto basta abrir o aquivo **main.tex** e clicar no botão em formato de seta ao lado do nome compilar.

`Obs.: Deve-se compilar somente utilizando o **main.tex** (independentemente das alterações terem sido feitas em outros aquivos), caso contrário dará erro.`

## MS-Windows (Visual Studio Code)

### Extensão LaTeX Workshop

Instale a extensão [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) e suas **dependências**.

Instale o pacote [minted](http://texdoc.net/texmf-dist/doc/latex/minted/minted.pdf) via seu _Package Manager_ favorito.

No objeto de configurações do VS-code insira o seguinte:

```JSON
"latex-workshop.latex.tools": [
	{
		"name": "latexmk",
		"command": "latexmk",
		"args": [
			"-synctex=1",
			"-interaction=nonstopmode",
			"-file-line-error",
			"-pdf",
			"%DOC%"
		]
	},
	{
		"name": "pdflatex",
		"command": "pdflatex",
		"args": [
			"-synctex=1",
			"-interaction=nonstopmode",
			"-file-line-error",
			"--shell-escape",
			"%DOC%"
		]
	},
	{
		"name": "bibtex",
		"command": "bibtex",
		"args": [
			"%DOCFILE%"
		]
	}
]
```

Ao compilar escolha a receita `pdflatex -> bibtex -> pdflatex*2`

![vs-code-compile](/img/vs-code-compile.png)

É possível também alterar as receitas da extensão acrecentando o seguinte ao seu objeto de configuração do VScode:

```JSON
"latex-workshop.latex.recipes": [
	{
		"name": "pdflatex -> bibtex -> pdflatex*2",
		"tools": [
			"pdflatex",
			"bibtex",
			"pdflatex",
			"pdflatex"
		]
	}
]
```

Com isso é possível compilar a partir do arquivo `main.tex` utilizando o atalho `Ctrl + Alt + B`.

Ou via comandos do VScode, pressionando, `Ctrl + Shift + P`, e procurando por `LaTex Workshop: Build LaTex Project:`

# Considerações

O presente projeto é uma colaboração entre alunos da instituição de ensino Univasf.
Ele tem como base o pacote [abntex2](https://github.com/abntex/abntex2).
Sinta-se livre para copiar, colar, modificar, etc.
