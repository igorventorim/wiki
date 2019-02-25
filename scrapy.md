# SCRAPY

 ## Instalação
 
 * Criar o ambiente com virtualenv e instalar o scrapy
   `pip install scrapy`

 ## Conceitos básicos

 ### Como utilizar
   
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

*     * Método responsável por extrair uma lista de seletores baseado na query.
`response.css("<CSS PATH>").extract_all()` ou `response.css("<CSS PATH>").getall()` ou `response.xpath("<CSS PATH>").getall()`

*     * Método responsável por extrair um elemento da lista de seletores baseado na query.
  `response.css("<CSS PATH>").extract_first()` ou `response.css("<CSS PATH>").get()` ou `response.xpath("<CSS PATH>").get()`

*     * Forma de tomar uma ação baseada no resultado
`yield <action>`







   
