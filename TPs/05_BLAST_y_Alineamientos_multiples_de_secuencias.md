# TP 5: BLAST y alineamientos múltiples de secuencias

## Parte 1: Explorar el proteoma Humano utilizando Blast (de forma local)

Para realizar el TP5 crearemos la carpeta TP5 en:
```
/home/bioinformatica/Documentos/
```
Y trabajaremos con el proteoma humano y proteínas de distintas especies que descargaremos desde la DB genbank.

**Nota:** Recuerden que los archivos se encuentran en la máquina virtual, dentro del directorio:
```
/home/bioinformatica/Documentos/docs_Bioinformatica
```
Pueden utilizar los archivos: _**protein.fa**_ (proteoma humano completo que usaron las clases anteriores.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/docs_bioinfo.jpg)

El BLAST ahora NO se realizará vía internet como en el TP anterior, sino de forma local en su propia máquina virtual!!!!!

Utilice GQuery para realizar la búsqueda de los mRNA que codifican para los factores de transcripción "transcription factor 19" de

Chimpancé (Pan troglodytes), Sus scrofa (cerdo), Bos taurus (vaca), Mus musculus (raton), Canis lupus familiaris (perro) y Bufo bufo (sapo). En caso de que haya más de 1 elija el perteneciente a la **base de datos más curada**. En el caso de humano elija la variante 1.

Recuerde acotar los campos de búsqueda y colocar palabras compuestas entre comillas. Si no conoce los campos de búsqueda puede ayudarse yendo a "advance".

> 1. ¿Cuántas proteínas aparecen en la búsqueda? (Escriba como realizó la búsqueda en Gquery remarcando cuales son los campos)

Identifique la proteína de la base de datos de RefSeq y responda:

> 2. ¿Cuál es el tamaño de la proteína?
> 3. ¿Cuál es su identificador único y su número de acceso?

| **Especie** | **Codigo de acceso del mRNA** | **Identificador único del mRNA** | **Codigo de acceso de la Proteina** | **Identificador único de la Proteina** | **Tamaño en aminoacidos** |
| --- | --- | --- | --- | --- | --- |
| chimpancé | | | | | |
| cerdo | | | | | |
| vaca | | | | | |
| ratón | | | | | |
| perro | | | | | |
| sapo | | | | | |
| Humano | | | | | |

Una vez identificadas las secuencias descárguelas usando efetch:
```
efetch -db sequences -format fasta_cds_na -id "numero de acceso de la secuencia de la especie" > query_especie.fasta
```
**Nota:** Cambiar la palabra especie por la que corresponda

Primero crearemos la base de datos:

Generaremos una "base de datos" a partir de un archivo multifasta para luego ejecutar un Blast y buscar dentro de ese archivo con una secuencia "query". Es decir, que debemos usar todas las secuencias del archivo como base de datos para la búsqueda. Para ello usaremos el archivo protein.fa de docs\_bioinformatica.

Para crear la DB vamos a usar el comando **"makeblastdb"**

Si queremos ver la ayuda para saber cómo se ejecuta el comando:
```
makeblastdb -help
```
Para indexar (crear la "base de datos") el archivo mutifasta que se llama human\_proteome.faa (o protein.fa) ejecuten:
```
makeblastdb -in <archivo multifasta> -dbtype prot -parse_seqids
```
**Nota:** Cambien el nombre según el archivo que ustedes tengan

Alineamos la secuencia query:

Vamos a alinear usando el comando **"blast"** y tomaremos como salida el formato tabular, después trabajaremos sobre esa salida para concluir cuáles de los hits obtenidos corresponden a homologos y cuáles no.

Fijemos el cutoff de un **e-value** < 1.0E-6

**NOTA:** Para hacer el TP en clase usaremos solamente la secuencia del perro. Pueden practicar con las demás secuencias en su casa.

Para ver la ayuda recuerde que puede usar el parametro "-help"

Ahora corremos BLAST de forma local:
```
Blast? -db human_proteome.faa -query <Archivo proteina query> -out blast_results_especies.tab -evalue 1.0E-6 -outfmt 6 -max_target_seqs 1000
```
**Nota:** Nuevamente, cambien al nombre y la palabra especie del archivo según corresponda

> 4. ¿Qué blast debe usar en este caso?
> 5. ¿Para qué sirve el parámetro max\_target\_seqs? (Miren la ayuda del comando)
> 6. ¿Cuántos hits se obtuvieron? ¿ **Qué es un** _ **hit** _ **para BLAST** en el archivo tabular?
> 7. ¿Cuántas secuencias únicas obtenemos con ese e-value menor a 1?0E-6?
> 8. ¿Cómo contamos secuencias únicas de esa salida?
> 9. Si eliminamos el cutoff para el e-value, ¿Cambia el resultado?

**Ayuda** :
```
cut -f 2 blast_results_especie_.tab | fgrep -v "#" | sort -u | wc -l
```
**Extraer secuencias de archivo multifasta:** Ahora vamos a identificar las proteinas homologas a nuestra sequencia query y las vamos extraer de la "base de datos" las secuencias correspondientes a todas las proteínas que alinearon localmente y contienen %id, long del alineamiento y score altos, etc (serían los putativos homologos). Primero tenemos que generar una lista con los nombres de las secuencias (puede ser el encabezado completo o solo el gi) a partir de la salida tabular de BLAST y luego a extraer con el comando **"blastdbcmd"**

**Ayuda** : ordenar la tabla usando:
```
sort -k4 -h -r
```
> 10. ¿Cómo hacen para obtener una lista de una sola columna que contenga solo el dato "gi"? Escribir comando usado.

**Nota:** Pueden usar los comandos _cut_ y _sort, uniq_ y head miren el siguiente link como una guía o ejemplo:

[https://stackoverflow.com/questions/21584727/using-linux-cut-sort-and-uniq](https://stackoverflow.com/questions/21584727/using-linux-cut-sort-and-uniq)
```
cat results_blastx.tab | sort -k4 -h -r | head -n21 | cut -f2 | sort | uniq > ids.txt
```
Luego, con esa lista, proceder a extraer esas secuencias de la base de datos usando el siguiente comando (reemplazar el nombre de la base de datos y del archivo con la lista de gis que crearon recien según cada uno):
```
blastdbcmd -db human\_proteome.faa -dbtype prot -entry_batch <Archivo con lista de gis nombres de paralogos > -out homologos_prot.fasta
```
> 11. ¿Que contiene el archivo **"**** homologos\_prot.fasta"?**

## Parte 2: Alineamientos múltiples

Los objetivos de este trabajo son familiarizarse con el uso de programas de alineamiento múltiple, asociar los diferentes resultados con los respectivos algoritmos o estrategias de alineamiento y aprender a utilizar sets de referencia para evaluar métodos.

Primero prepararemos el enviroment que necesitamos para realizar el TP. Para ello usaremos Conda para generar el enviroment msa\_tools:

**NOTA** : el enviroment msa\_tools ya está creado en la VM por lo que no debe ejecutarse los comandos de creación del enviroment.
```
conda create -n msa_tools extract_fasta_seq muscle clustalo jalview figtree
```
Puede verificar que el nuevo enviroment fue creado haciendo:
```
conda info –envs
```
Para activar el nuevo enviroment ejecute:
```
conda activate msa_tools
```
Como aprendimos en la teoría los alineamientos múltiples se realizan entre proteínas que están relacionadas filogenéticamente o bien que son ortólogas u homologas ya que poseen un alto grado de similitud. Es decir, que tienen posiciones de aminoácidos altamente conservadas debido a que provienen de un ancestro en común. Todas aquellas regiones que estén altamente conservadas se supone que están asociadas a alguna función o estructura importante para el correcto funcionamiento y estructura nativa de la proteína.

Ahora si, estamos listos para realizar el alineamiento múltiple. Para ello usaremos Muscle (https://www.drive5.com/muscle/) o CustalO (http://www.clustal.org/) bajo la siguiente sintaxis:

**Muscle:**
```
muscle -in homologos\_prot.fasta -out msa.muscle
```
**ClustalO:**
```
clustalo -i homologos\_prot.fasta -o msa.clustal
```
> 1. ¿Qué tipo de método utiliza el alineador múltiple que usó? ¿Cuántas veces recalculó el alineamiento?

Para visualizar el lineamiento usaremos el programa JalView (https://www.jalview.org/).

Para ello escribimos en la terminal:
```
jalview -open msa.muscle
```
> 2. ¿Alinearon bien las secuencias? ¿Qué regiones alinearon mejor?
> 3. ¿En qué región supone que pueden encontrarse Dominios proteicos y por qué?
> 4. ¿Qué significa el consenso?
> 5. Puede obtener el logo de la secuencia haciendo click derecho sobre consenso y tildar LOGO. ¿Qué sucede con el Logo hacia el final del alineamiento y que significa?

Puede colorear el alineamiento según la matriz de sustitución BLOSUM62. Para ello el color elija BLOSUM62 y diga que observa.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/blossum62_color.jpg)

Ahora coloree el alineamiento según Zappo:

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/zappo.jpg)
> 6. ¿Qué observa en el alineamiento?

Ahora realice la descarga _ **de las secuencias de proteínas** _ de la tabla de especies usando efetch:
```
efetch -db sequences -format fasta_cds_aa -id "numero de acceso de la secuencia de la especie" > query_especie.faa
```
> 7. ¿Cuál es la diferencia con la línea de comandos para la descarga de secuencias de nucleótidos?

Ahora repita el procedimiento de alineamiento múltiple con las proteínas que descargó.

> 8. ¿Alinearon bien las secuencias? ¿Qué regiones alinearon mejor?
> 9. ¿En qué región supone que pueden encontrarse Dominios proteicos y por qué?

Realice un árbol filogenético y describa lo que observa.

> 10. ¿Cómo describiría el resultado obtenido?

## Parte 3: Preguntas repaso

> 1. ¿Qué valor de E (expect value) considerarías significativo en BLAST? 1, 0.05, o 10E–5? ¿Depende de algún otro factor? ¿Importa si es blastp o blastn?

> 2. ¿Por qué BLAST balancea sensibilidad vs especificidad? ¿Qué asume BLAST en su algoritmo?

> 3. Si tenés una secuencia de ADN proveniente de mRNA y quiero usar la base de datos de proteínas "nr" ("nr", the nonredundant database) para identificar la proteína más similar, ¿Qué programa uso?
> 	 - a. blastn
> 	 - b. blastp
> 	 - c. blastx
> 	 - d. tblastn
> 	 - e. tblastx

> 4. ¿Qué resultado de blast (estadísticos) te dan un estimado de cuántos falsos positivos tienes entre tus "hits"?
> 	 - a. E value
> 	 - b. Bit score
> 	 - c. Percent identity
> 	 - d. Percent positives

> 5. Indicar que ocurriria con la cantidad de resultados positivos ("hits"), en cada uno de los casos, al cambiar los parámetros:
> 	 - a. No utilizar el filtro de baja complejidad (low-complexity filter)
> 	 - b. Cambiando el e-valor de 0.1 a 1
> 	 - c. Cambiando la matriz de sustitución de una PAM30 a una PAM70

> 6. ¿Por qué creen que NO hay una "Basic Global Alignment Search Tool" (BGAST) como complemento a BLAST? ¿Sería util BGAST? ¿Qué ven como difícil a nivel computacional de un programa de alineamiento global pero del estilo BLAST?

<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
