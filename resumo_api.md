============= API RestFull ==============

URI:
	Estrutura Mínima
	https://api.mycompany.com/name-of-api/resource


RESOURCES:

	Coleção:
		/pedidos

	Elemento:
		/pedidos/id_pedido

		Sub-elementos:
			/pedidos/id_pedido/itens/id_itens

	*Padrão RPC: /getAccount 

OPERAÇÕES:

		SAFE: Não altera nada.
		UNSAFE: Altera os dados.


	GET -- Mostrar
		/pedidos - Listar pedidos
		/pedidos/id_pedido - Mostrar pedido id_pedido.
		
		SAFE
		IDEMPOTENTE: Recebe sempre o mesmo resultado se não houve alteração nos outros dados.

	POST -- Criar
		/pedidos - Criar novo pedido
		/pedidos/id_pedido - xxx

		UNSAFE
		NÃO IDEMPOTENTE
		

	PUT -- Editar
		/pedidos - xxx
		/pedidos/id_pedido - Atualizar pedido id_pedido, se não existir, cria.

		UNSAFE
		IDEMPOTENTE


	DELETE -- Apagar
		/pedidos - Apagar todos os pedidos
		/pedidos/id_pedido - Apagar pedido id_pedido

		UNSAFE
		IDEMPOTENTE

	PATCH --Método para atualização parcial
		/users/id_user - Atualiza um determinado elemento de um cliente
		/pedidos/id_pedido - Atualiza um determinado elemento de um cliente

		UNSAFE
		NÃO IDEMPOTENTE

	OPTIONS --Quais métodos são permitidos
		SAFE
		/clientes - Allow: HEAD,GET,POST,OPTIONS

	HEAD --Quero ver apenas o header
		/clientes - Igual o GET porém retorna o header em vez do body - Incomum.

VERSION:

	https://api.mycompany.com/name-of-api/v2/resource

MEDIA TYPES:
	
	Formatos Padronizados: { application/json, application/xml }

STATUS E ERROR CODES:
	
	200: OK

	400: ERRO NO CLIENT

	500: ERRO NO SERVER

FILTROS:

	Busca Global:

		GET /search?q=macbook+air

	Busca com escopo (subconjuntos):

		GET /vendas/v2/pedidos?status=concluido

	Respostas parciais:

		GET /pedidos/id_pedido?_fields=numero,data,valor


PAGINAÇÃO:

	Recomendação:

		GET /pedidos?_offset=50&_limit=25

		Likedin - ?start=50&count=25
		Instagram - ?min_id=3091&max_id=3245&count=25

		API RESTRINGE LIMITE INTERNO

CACHING:

	EVITAR TRÁFEGO DESNECESSÁRIO.
		- LATÊNCIA DE REDE
		- SOBRECARGA NOS SERVIDORES

	ATENÇÃO:
		- TEMPO DE INVALIDAÇÃO DO CACHE
		- SINCRONIZAÇÃO EM CLUSTERS

SEGURANÇA:
	
	-> ACESSO NÃO AUTORIZADO

	-> ATAQUES

	-> SOBRECARGA

	-> IMPLEMENTAÇÃO DE CLIENTS DESASTRADOS

	PADRÃO OAUTH2

CALLBACKS:

	- WEBHOOK

HYPERMEDIA APIs:
	
	GET /orders/123
	{
	  "_links": {
	    "place_order": {
	      "method": "put",
	      "href": "https://api.com/orders/123/completion"
	    }
	  },
	  "updated_at": "2017-04-10T18:30Z",
	  "id": 123,
	  "status": "open",
	  "total": 1000
	}

