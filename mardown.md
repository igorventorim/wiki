### Titulos (<h1> a <h6>)
Para marcar um título, você vai usar # a quantidade de vezes que irá representar o nível do título. Exemplo:

\# Título nível 1
\## Título nível 2
\### Título nível 3
\#### Título nível 4
\##### Título nível 5
\###### Título nível 6


Título de nível 1
\==================
  
Título de nível 2
\------------------

### Parágrafos e quebras de linha (<p> e <br />)
Para gerar parágrafos, basta você escrever o texto em uma linha:

Este é um parágrafo.
  
Este é outro parágrafo.


A documentação do Markdown diz que, para quebras de linha, você precisa deixar dois espaços no final da linha:

### Ênfase (<strong> e <em>)

Para enfatizar uma palavras (<em>), usamos um * ou _:

Javascript é \_cool_!  
Javascript é \*cool*!  

O mais utilizado para ênfase (<em>) é o underline.

Para dar forte ênfase em palavras (<strong>), você usa dois ** ou __:

\**Da2k** é a pronúncia para **Daciuk**: DA-TWO-K!  
\__Da2k__ é a pronúncia para __Daciuk__: DA-TWO-K!

O mais utilizado para forte ênfase (<strong>) são dois asteriscos.

### Links (<a>)

Para gerar links, você usa [](). Dentro dos colchetes você coloca o texto do link, e dentro dos parênteses, você coloca a URL:

\[Blog do Da2k](https://blog.da2k.com.br)

Passando um texto após a URL, separando o link do texto por um espaço em branco, esse texto será usado como title:

\[Blog do Da2k](https://blog.da2k.com.br "Clique e acesse agora!")

### Links automáticos

Se o texto do seu link é o próprio link, você pode envolvê-lo entre < e >, que o link será gerado automaticamente:

\<https://www.google.com.br>

E isso funciona também para e-mails:

\<meu@email.com>

### Referências 

...

### Blocos de citação (<blockquote>)

Para criar blocos de citação, você usa o sinal de >:

\> Esse é um bloco de citação.
\> Ele pode ter várias linhas por parágrafo.
\>
\> Inclusive, dando um espaço, você tem um novo parágrafo.

### Listas (<ul> e <ol>)

Para listas não ordenadas (<ul>), você pode usar *, + ou -. Veja:

\* Item 1
\* Item 2
\* Item 3
  
\+ Item 1
\+ Item 2
\+ Item 3
  
\- Item 1
\- Item 2
\- Item 3

E para listas ordenadas, você usa o número, seguido de ponto:

1\. Item 1
2\. Item 2
3\. Item 3

### Imagens (<img />)

Geração de imagens é bem parecido com a geração de links: você só precisa adicionar uma ! no início. E o texto que você coloca entre os colchetes, é usado como alt na imagem:

\![Banana]\(http://cdn.osxdaily.com/wp-content/uploads/2013/07/dancing-banana.gif)

O title também funciona como no link:

\![Banana]\(http://cdn.osxdaily.com/wp-content/uploads/2013/07/dancing-banana.gif "Olha a banana dançando!")

### Tabelas (<table>)

Para criar tabelas, também é bem simples:

Alimentos \| Preço
\--------- \| \------:
Arroz     \| R$ 10
Feijão    \| R$ 8
Batata    \| R$ 7
Macarrão  \| R$ 8

O título da tabela é marcado com os traços - abaixo da palavra. O pipe | cria as colunas. ão é necessário alinhar com espaços, mas visualmente fica melhor. Não é necessário alinhar com espaços, mas visualmente fica melhor. 

Se usar : no lado esquerdo, o alinhamento será feito à esquerda (padrão); Se usar : no lado direito, o alinhamento será feito à direita; E para centralizar, use dos dois lados.


### Task lists

Sabe aquela issue que você abriu no Github e precisa quebrá-la em partes, mas não quer criar uma issue para cada coisa? Você pode usar as task lists!

[] Comprar arroz
[] Comprar feijão
[] Comprar batata
[x ] Comprar macarrão

### Código inline e bloco (<code> e <pre>)

Vocế ainda pode adicionar trechos de código via Markdown. Para adicionar código a nível inline, você usa \`:

O \`<blockquote>\` é uma tag HTML.

E para gerar blocos de código, você simplesmente indenta o código 4 espaços (ou 1 tab) à frente do paràgrafo:

Essa é a função sayHello():
    function sayHello() {
      return 'hi!';
    }

Isso é como está na documentação. Mas a maior parte dos parses que eu conheço não funcionam dessa forma. Eles geram blocos de código usando três crases no início da primeira e última linha, para marcar o início e o fim do bloco:

\```
function sayHello(){
    return "hi";
}
\```

### Backslash scapes

Para escapar caracteres que são parseados pelo Markdown, você pode usar a barra invertida \ (backslash), seguida do caractere, para imprimí-lo literalmente. O escape funciona para os caracteres listados abaixo:

\\   backslash (barra invertida)
\`   backtick (crase)
\*   asterisk (asterisco)
\_   underscore
\{}  curly braces (chaves)
\[]  square brackets (colchetes)
\()  parentheses (parênteses)
\#   hash mark (sustenido / hash / jogo da velha)
\+   plus sign (sinal de "mais" ou somar)
\-   minus sign (hyphen) (sinal de menos ou hífen)
\.   dot (ponto)
\!   exclamation mark (ponto de exclamação)

Documentação oficial: http://daringfireball.net/projects/markdown/

