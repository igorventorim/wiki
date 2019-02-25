
					*** ____ ESTUDOS ECMASCRIPT 6 ____ ***

========================================> [ MÉTODOS E TÉCNICAS ] <===================================================

  ===> MÉTODOS AUXILIARES PARA ARRAY <===

  - FOREACH

	  	var nomes = ['maria', 'josé', 'joão'];
		nomes.forEach(function(nome) {
			console.log(nome);
		});

		var nomes = ['maria', 'josé', 'joão'];
		function imprimeNome(nome) {
			console.log(nome);
		}
		nomes.forEach(imprimeNome);

		# Os elementos que forem adicionados depois da chamada do método não serão vistos.

  - MAP

	  	O método map é muito útil quando precisamos não somente passar por todos os elementos de um Array , mas também
		modificá-los.

	  	var numeros = [1,2,3];
		var dobro = numeros.map(function(numero) {
			return numero * 2;
		});
		console.log(numeros); // [1,2,3]
		console.log(dobro); // [2,4,6]

  - FILTER

	  	Como o próprio nome já pode induzir, este método é deve ser utilizado quando temos a necessidade de filtrar nossa lista de acordo com algum critério.

	  	var alunos = [
		{nome:'joão', idade:15},
		{nome:'josé', idade:18},
		{nome:'maria', idade:20}
		];
		var alunosDeMaior = alunos.filter(function(aluno) {
			return aluno.idade >= 18;
		});
		console.log(alunosDeMaior);
		// [{nome:'josé', idade:18}, {nome:'maria', idade:20}]

		Dentro da função, utilizamos um critério de avaliação para devolver um valor booleano para o filter : true ou false . Se for retornado verdadeiro, o valor é inserido no novo Array retornado; caso contrário, é simplesmente ignorado e não é incluído.

  - FIND 

	  	Esta função auxiliar é particularmente interessante quando o objetivo é encontrar um item específico dentro de um Array.

	  	var alunos = [
		{nome:'joão'},
		{nome:'josé'},
		{nome:'maria'}
		];

		var aluno = alunos.find(function(aluno) {
			return aluno.nome === 'josé';
		});
		console.log(aluno); // {"nome":"josé"}

		Caso na lista existissem dois alunos com o nome “josé”, somente o primeiro seria retornado. Para contornar este caso, precisaríamos usar um critério de busca mais específico.

  - EVERY

	  	Esta é uma função auxiliar bem interessante. Ao contrário das outras que vimos até então, esta não retorna uma cópia do Array, mas sim um valor booleano.

	  	var alunos = [
		{nome:'joão', idade: 18},
		{nome:'maria' idade: 20},
		{nome:'pedro', idade: 24}
		];
		var todosAlunosDeMaior = alunos.every(function(aluno){
			return aluno.idade > 18;
		});
		console.log(todosAlunosDeMaior); // true

  - SOME

	  	Se a tarefa é validar se, pelo menos, um dos elementos de um Array satisfaz uma dada condição, o some é o método perfeito para o trabalho.

	  	var pesoDasMalas = [12,32,21,29];
		var temMalaAcimaDoPeso = pesoDasMalas.some(function(pesoDaMala) {
		return pesoDaMala > 30;
		});
		console.log(temMalaAcimaDoPeso); // true

  - REDUCE

	  	A ideia por trás dela é pegar todos os valores de um Array e condensá-los em um único.

	  	var alunos = [
		{nome:'joão', idade: 10},
		{nome:'josé', idade: 20},
		{nome:'marcos', idade: 30}
		];
		var nomes = alunos.reduce(function(arrayNomes, aluno) {
		arrayNomes.push(aluno.nome);
			return arrayNomes;
		}, []);
		console.log(nomes); // ['joão', 'josé', 'marcos']


===> ITERAÇÃO COM ITERADORES E ITERÁVEIS <===

		iteravel.next() // {value: undefined, done: true}

		No javascript, alguns tipos já são iteráveis por padrão:

		- Arrays
		- Strings
		- Maps
		- Sets

		//Obtém o iterador
		var iterator = bruxos[Symbol.interator]();


		Por natureza, iteradores são Lazy. Isso significa que ele não sabe de antemão quantos valores vai iterar. É preciso ter muito cuidado, pois ele pode iterar algo infinitamente.


===> ITERAÇÃO COM O LAÇO FOR ... OF <===

	O laço de iteração for...in , disponível no JavaScript já há bastante tempo, funciona de forma diferente. Enquanto ele percorre os nomes dos atributos de um objeto, o laço for...of itera somente objetos iteráveis, percorrendo os valores dos atributos.


===> MAP e WeakMap <===

 - MAP

 	var map = new Map();
 	function funcao(){};
 	var objeto = {};

 	map.set("string","teste");
 	map.set(funcao,"sou uma funcao");
 	map.set(objeto,"sou um objeto");

 	map.get("string");

	console.log("tamanho: " + map.size); // tamanho: 3

	console.log(map.has("string")); // true

	map.delete("string");

	map.clear();

	#ITERÁVEL
	for(var chave of mapa.keys()){
		console.log(chave); // um dois três
	}

 - WeakMap

 	Um WeakMap é uma coleção de pares de chave/valor na qual as	chaves só podem ser objetos.

 	Ao usar um WeakMap , conseguimos esconder a propriedade que guarda o valor e oferecer somente um método para recuperá-lo.

	var Pessoa = (function() {
	var dadosPrivados = new WeakMap();
	function Pessoa(nome) {
		dadosPrivados.set(this,{ nome: nome });
	}
	Pessoa.prototype.getNome = function() {
		return dadosPrivados.get(this).nome;
	};
	return Pessoa;
	}());
	var rafael = new Pessoa('Rafael');
	console.log(rafael.getNome()); // Rafael
	console.log(rafael.nome); // undefined


===> SET ES <===
 -  No ecmascript 5 não existe o tipo SET, por isso é necessário criá-lo.

 # Script mostrando a classe Set minimamente funcional.
 function Set() {
     var array[];
     this.add = function(valor) {
         if(array.indexOf(valor) === -1){
		array.push(valor);
	 }
     },

     this.mostrarValores = function() {
	console.log(array);
     }
  }
 
  var set = new Set();
  set.add(2);
  set.mostrarValores(); // [2]

  - No ecmascript 6 temos a estrutura Set implementada nativamente.

	var set = new Set();
	set.add(2);
	set.add(1);
	set.add(2);
	for (const valor of set) {
		console.log(valor); // 2, 1
	}

	*Não possui o método mostrar valores implementado nativamente.

   var set = new Set([2,1,2]);
   # O construtor do Set nos permite passar vários valores.
   set.add(element);	# ADICIONA ELEMENTO NO SET.
   set.delete(element); # REMOVE ELEMENTO DO SET.
   set.clear();	#LIMPA TODO O SET.
   set.has(element); #CONFERE SE O SET TEM UM DETERMINADO ELEMENTO.
   set.size;	#CONFERE TAMANHO DO SET.

===> WEAKSET <===

 - O WeakSet é um set que não previne os seus elementos de serem coletados pelo Garbage Collector. Uma vez que o elemento não existe mais e seja identificado pelo coletor para ser coletado, ele também é automaticamente removido do WeakSet.
 [RESTRIÇÕES]
  * Só é possível adicionar objetos de tipos primitivos.
  * O WeakSet não é iterável.
  * Não há como remover todos os elementos de uma vez.
  (Utilizado sempre que você tiver preocupação com vazamento de memória)


===> DECLARAÇÃO DE VARIÁVEIS COM CONST E LET <===

 - Para definir qualquer tipo de variável no JavaScript, utilizamos a palavra reservada var . Elas podem ser objetos literais, números,
caracteres, strings, listas ou funções:

// exemplos
var objeto = {}; // objeto
var numero = 1; // numero
var nome = "Chaves"; // string
var lista = [1,2,3]; // lista

  	
  - Usaremos o const nas variáveis que não esperamos que mudem de valor com o decorrer do tempo/execução do programa dentro de um escopo. Todavia, é necessário ter em mente que um const não se trata de uma variável constante, mas uma referência constante.

 const pessoa = {nome: 'joão'};
 pessoa.idade = 12;
 console.log(pessoa); // {"nome":"joão", "idade": 12}
  

  - Podemos considerar o let como o verdadeiro substituto do var . Idealmente ele deve ser usado para declarar variáveis que esperamos que mudem com o valor e com o tempo/execução do programa.

  - Entretanto, ao contrário do que acontecia com o var , se uma mesma variável, dentro de um mesmo escopo, é declarada duas vezes, tomamos erro de sintaxe. Isso acontece tanto para o let quanto para o const .

const arrayVar = [];
for(var i = 1; i < 5; i++) {
	arrayVar.push(function () {
	console.log(i);
});
}

const arrayLet = [];
for(let i = 1; i < 5; i++) {
	arrayLet.push(function () {
	console.log(i);
});
}


arrayVar.forEach(function (funcao) {
	funcao(); // 5 5 5 5 5
});

arrayLet.forEach(function (funcao) {
	funcao(); // 1 2 3 4 5
});


=====> TEMPLATES STRINGS <=====

 - TEMPLATE STRINGS SIMPLES
Com o ES6, podemos concatenar strings de um jeito mais eficiente. Quer ver? É assim que fica o código anterior com ES6:

const nome = 'Diego';
console.log(`Bem-vindo, ${nome}`);

O primeiro item importante que precisamos reparar neste código é que não estamos mais usando aspas simples ( ‘ ) na String , mas sim a crase (`).

 - TEMPLATE STRINGS MARCADO

const mensagem = defineMensagem`${""}${horas} horas`;

Agora trabalhamos na lógica da função defineMensagem para atender ao requisito:

function defineMensagem(strings, ...values){
	const hora = values[1];
	if(hora >= 6 && hora <= 12) {
		values[0] = "Bom dia";
	} else if (hora > 12 && hora <= 18) {
		values[0] = "Boa tarde";
	} else {
		values[0] = "Boa noite";
	}
	values[0] = `${values[0]}, são`;
	return `${values[0]}${strings[0]}${hora}${strings[2]}`
}


=====> ARROW FUNCTIONS <=====


		