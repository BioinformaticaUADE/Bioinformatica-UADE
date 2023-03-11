# TP 2: Base de datos

**Este trabajo práctico se realiza desde un navegador web, por lo tanto no es necesario utilizar la máquina virtual.**

_URLs que utilizaremos hoy:_

**Gquery**, es el "_google_" de todas las bases de datos de NCBI (National Center for Biotechnology Information).

Permite buscar de manera **MUY** rápida, sencilla y/o compleja, a través de todas las bases de datos de NCBI (más de 40 DBs).

(_Gquery_ antes se llamaba _Entrez_)

**Ojo: No todas las bases tienen las mismas tablas ni campos.**

[http://www.ncbi.nlm.nih.gov/gquery/](http://www.ncbi.nlm.nih.gov/gquery/)

**Ejemplo / Sintaxis de busqueda:**

_Podemos hacer una búsqueda ingresando el código de acceso. Por ejemplo el del TP anterior:_ **"NC\_045512"** en all databases o en una base de datos específica. _

_O bien usando palabras especificando campos y conectores lógicos._

_**"Severe acute respiratory syndrome coronavirus 2" AND SARS-CoV-2[organism]**_

_ **Conectores lógicos** _

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/conditionals.jpg)

## Parte I: Uso de Entrez o GQuery. Buscar proteínas con un dominio que nos interesa.

Para llegar hasta el gen DSCAM (Down syndrome cell adhesion molecule) del genoma humano en el cromosoma 21, nos interesa el dominio Immunoglobulin:

1. Utilizando Entrez o GQuery, encuentra cuántos genes humanos tienen un dominio _Immunoglobulin_. ¿Cómo sabemos si está bien eso? ¿Uso la base nucleótidos o genes? ¿Donde ingreso la búsqueda, que me conviene? Tip: Usar ENTREZ de NCBI.
  1. ¿Que es lo que ven?
  2. Tipear: human [organism] AND Immunoglobulin domain
  3. ¿En todas las distintas bases de datos se utilizan esos "campos"?
2. Y si probamos con delimitar el campo "domain" para buscar "Immunoglobulin". ¿Qué cambia? ¿A qué búsqueda le creo mas? ¿Por qué?
3. Tipear: Immunoglobulin [domain name] AND human [organism]
4. Acotar la búsqueda para encontrar cuántos genes con este tipo de dominio existen en el cromosoma 21. Usar el buscador en la página principal de entrez.
5. Tipear: human [organism] AND 21 [chromosome] AND Immunoglobulin [domain name]
  1. ¿En todas las distintas bases de datos se utilizan los mismos "campos"?
  2. Ver dentro de genes, ESTs, etc.

![](RackMultipart20230310-1-7kwfa1_html_45f35879539980f1.png)

![](RackMultipart20230310-1-7kwfa1_html_1eb390ac83eeb949.png)

## Parte II: Ahora vamos a trabajar con el cDNA AF217525. Utilizar Gquery para obtener la secuencia FASTA y encontrar la siguiente información

![](RackMultipart20230310-1-7kwfa1_html_b3c88ac2de8eeb56.png)

**(recordar qué la base de datos GENE es la qué contiene más información)**

1. ¿A qué gen pertenece este cDNA? Dar nombre del Gen.
2. ¿Cuántos aminoácidos tiene el producto de la traducción de este cDNA?
3. ¿Cuáles son los IDs de cada posible transcripto de este gen? Confirmar si fueron manual o automáticamente curados (NM o XM). ¿Qué variante contiene el cDNA AF217525? ¿En qué cromosoma está el gen?
4. ¿Qué dominios Pfam contiene la proteína?
5. ¿Tiene alguna publicación asociada?

## Parte III: Usar NCBI Gquery para realizar búsquedas de proteínas

Busque la proteína receptora de angiotensina "angiotensin II receptor".

1. ¿Cuántos resultados observa?
2. ¿En cuántas especies/Reinos está presente?
3. ¿En qué organismos está presente?
4. ¿Cuántas tienen estructura?
5. ¿Cuántas existen en bases de datos de proteínas curadas?

Haga más específica su búsqueda especificando el campo "protein name".

1. ¿Cuántos resultados observa ahora?

Ahora agregue además el campo organismo para hacer una búsqueda en humanos y otra búsqueda en gallo y encuentre en cada caso los códigos de acceso y los identificadores únicos (GI).

<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___

