---
title: pdfbox
description: 
published: true
date: 2021-04-01T20:47:44.752Z
tags: 
editor: markdown
dateCreated: 2021-04-01T20:46:19.038Z
---

# PDFBox

### Components of PDFbox
- PDFBox: É a parte principal do PDFBox. Contém as classes e interfaces relacionadas ao conteúdo de entração e manipulação.

- FontBox: Contém as classes e interfaces relacionadas a fontes, usando essas classes nós podemos modificar a fonte do texto do documento PDF.

- XmpBox: Contém as classes e interfaces que manipulam meta dados XMP.

- Preflight: É utilizado para verificar os arquivos PDF.

### PDFBox URL maven - Components

1. https://mvnrepository.com/artifact/org.apache.pdfbox/pdfbox
2. https://mvnrepository.com/artifact/org.apache.pdfbox/fontbox
3. https://mvnrepository.com/artifact/org.apache.pdfbox/pdfbox-tools
4. https://mvnrepository.com/artifact/org.apache.pdfbox/preflight
5. https://mvnrepository.com/artifact/org.apache.pdfbox/xmpbox

#### USANDO POM XML

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <groupId>my_project</groupId>
   <artifactId>my_project</artifactId>
   <version>0.0.1-SNAPSHOT</version>

   <build>
      <sourceDirectory>src</sourceDirectory>
      <plugins>
         <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.3</version>
            <configuration>
               <source>1.8</source>
               <target>1.8</target>
            </configuration> 
         </plugin>
      </plugins> 
   </build> 
   
   <dependencies>  
      <dependency> 
         <groupId>org.apache.pdfbox</groupId> 
         <artifactId>pdfbox</artifactId> 
         <version>2.0.1</version> 
      </dependency>   
   
      <dependency> 
         <groupId>org.apache.pdfbox</groupId> 
         <artifactId>fontbox</artifactId> 
         <version>2.0.0</version> 
      </dependency>
      
      <dependency>  
         <groupId>org.apache.pdfbox</groupId> 
         <artifactId>jempbox</artifactId> 
         <version>1.8.11</version> 
      </dependency> 
        
      <dependency>
         <groupId>org.apache.pdfbox</groupId> 
         <artifactId>xmpbox</artifactId> 
         <version>2.0.0</version> 
      </dependency> 
     
      <dependency> 
         <groupId>org.apache.pdfbox</groupId> 
         <artifactId>preflight</artifactId> 
         <version>2.0.0</version> 
      </dependency> 
     
      <dependency> 
         <groupId>org.apache.pdfbox</groupId> 
         <artifactId>pdfbox-tools</artifactId> 
         <version>2.0.0</version> 
      </dependency>

   </dependencies>
   
</project>
```


### PDFBox - Loading a Document


#### Carregando um documento PDF existente