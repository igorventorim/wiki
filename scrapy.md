# SCRAPY

 ## Instalação
 
 * Criar o ambiente com virtualenv e instalar o scrapy
   `pip install scrapy`

 ## Conceitos básicos

 ### Como utilizar
   Exemplo de classe scrapy:
   ```
   #Importar o scrapy
   import scrapy

   #Criar classe herdando spider
   class exempleSpider(Spider):

   		#Defini o nome do spider
   		name="exempleSpider"

   		#Método default de inicialização do scrapy
   		def start_requests(self):
   		        yield Request("https://www.climatempo.com.br/brasil", callback=self.parse_start_page)

   		#Método default de resposta do scrapy
   		def parse(self,response):
   			pass
   ```

 ### Tipos de extratores
* Consultando resposta baseado em query xpath
`response.xpath()`
* Consultando resposta baseado em query css
 	`response.css()`

 ### Métodos importantes

*  Método responsável por extrair uma lista de seletores baseado na query.
`response.css("<CSS PATH>").extract_all()` ou `response.css("<CSS PATH>").getall()` ou `response.xpath("<CSS PATH>").getall()`

*  Método responsável por extrair um elemento da lista de seletores baseado na query.
  `response.css("<CSS PATH>").extract_first()` ou `response.css("<CSS PATH>").get()` ou `response.xpath("<CSS PATH>").get()`

* Forma de retornar uma ação baseada no resultado
`yield <action>`
> Um método de callback pode retornar 3 tipos de valores no scrapy, sendo estes um request, dicionário ou item.

* Capturar uma url dentro da página.
`response.urljoin(link)`

### Parâmetros do framework

* Nome da spider
`name="TESTE"`

* Domínios permitidos realizar o scrapy
`allowed_domains = ['aosfatos.org']`

* Url do primeiro request
`start_urls=['https://aosfatos.org']`

### Parâmetros de execução scrapy

* Exportar resultado como csv
`scrapy runspider file.py -o quotes.csv`

* Adicionar cache para evitar sobrecarregar servidor
`scrapy runspider file.py -s HTTPCACHE_ENABLED=1`

### Utilitários

* Debug python
`import ipdb; ipdb.set_trace()`

* Scrapy shell: Permite usar o scrapy em modo shell.
`scrapy shell https://aosfatos.org`







   
