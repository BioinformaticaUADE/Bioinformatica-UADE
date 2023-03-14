# TP 4: Alineamientos de secuencias II: Programacion dinámica y BLAST

## Parte I: Alineamiento Global: Algoritmo de Needleman-Wunsch – Programación dinámica

Hacer un alineamiento global de la secuencia de _Homo sapiens_ del TP anterior con la del archivo _DSCAM\_homo\_sapiens\_isoform1.fasta_ con el comando: "_needle_" (_Needleman-Wunsch global alignment of two sequences_)

> 1. ¿Como se usa _needle_? ¿Que tipo de alineamiento nos da como resultado?
> 2. ¿Hay _mismatches_ y pequeños _gaps_?
> 3. ¿Porque no vimos esto en los _dotplots_?
> 4. ¿Que pasa si modifican el _GapOpen_ y/o _GapExtend_? Por ejemplo pasen el _GapOpen_ de 10 a 100. ¿Los scores varían? ¿Qué pasa con el % de similitudes?
> 5. ¿Qué ocurre si llevan los valores de _GapOpen_ y _GapExtend_ al máximo permitido (100 y 10 respectivamente)?
> 6. Ahora cambien la matriz usada por EPAM10 y/o EPAM500.¿Qué diferencia ven en el alineamiento? ¿Scores distintos? ¿Porque ocurre?

### Parte II: BLAST Problemas

[https://blast.ncbi.nlm.nih.gov/Blast.cgi](https://blast.ncbi.nlm.nih.gov/Blast.cgi)

**Historia:**

En la historia de Jurassic Park de Michael Crichton, sobre el clonado de dinosaurios, se obtiene una secuencia putativa de DNA perteneciente a este tipo de animales.

Vamos a utilizar **BLASTn** (nucleótidos vs nucleótidos) y la base de datos **nt** (non redundant nucleotide NCBI) para identificar cual es la fuente real de la secuencia.

Para esto vamos a seleccionar la siguiente secuencia y pegarla en el formulario de búsqueda de **BLAST en NCBI.**
```
>DinoDNA from JURASSIC PARKp. 103 nt 1-1200
GCGTTGCTGGCGTTTTTCCATAGGCTCCGCCCCCCTGACGAGCATCACAAAAATCGACGCGGTGGCGAAACCCGACAGGACTATAAAGATACCAGGCGTTTCCCCCTGGAAGCTCCCTCGTGTTCCGACCCTGCCGCTTACCGGATACCTGTCCGCCTTTCTCCCTTCGGGAAGCGTGGCTGCTCACGCTGTACCTATCTCAGTTCGGTGTAGGTCGTTCGCTCCAAGCTGGGCTGTGTGCCGTTCAGCCCGACCGCTGCGCCTTATCCGGTAACTATCGTCTTGAGTCCAACCCGGTAAAGTAGGACAGGTGCCGGCAGCGCTCTGGGTCATTTTCGGCGAGGACCGCTTTCGCTGGAGATCGGCCTGTCGCTTGCGGTATTCGGAATCTTGCACGCCCTCGCTCAAGCCTTCGTCACTCCAAACGTTTCGGCGAGAAGCAGGCCATTATCGCCGGCATGGCGGCCGACGCGCTGGGCTGGCGTTCGCGACGCGAGGCTGGATGGCCTTCCCCATTATGATTCTTCTCGCTTCCGGCGGCCCGCGTTGCAGGCCATGCTGTCCAGGCAGGTAGATGACGACCATCAGGGACAGCTTCAACGGCTCTTACCAGCCTAACTTCGATCACTGGACCGCTGATCGTCACGGCGATTTATGCCGCACATGGACGCGTTGCTGGCGTTTTTCCATAGGCTCCGCCCCCCTGACGAGCATCACAAACAAGTCAGAGGTGGCGAAACCCGACAGGACTATAAAGATACCAGGCGTTTCCCCCTGGAAGCGCTCTCCTGTTCCGACCCTGCCGCTTACCGGATACCTGTCCGCCTTTCTCCCTTCGGGCTTTCTCAATGCTCACGCTGTAGGTATCTCAGTTCGGTGTAGGTCGTTCGCTCCAAGCTGACGAACCCCCCGTTCAGCCCGACCGCTGCGCCTTATCCGGTAACTATCGTCTTGAGTCCAACACGACTTAACGGGTTGGCATGGATTGTAGGCGCCGCCCTATACCTTGTCTGCCTCCCCGCGGTGCATGGAGCCGGGCCACCTCGACCTGAATGGAAGCCGGCGGCACCTCGCTAACGGCCAAGAATTGGAGCCAATCAATTCTTGCGGAGAACTGTGAATGCGCAAACCAACCCTTGGCCATCGCGTCCGCCATCTCCAGCAGCCGCACGCGGCGCATCTCGGGCAGCGTTGGGTCCT
```
1. El científico de NCBI Mark Boguski se dio cuenta de una "contaminación obvia" ¿Cuál era la contaminación?

Entonces Crichton, le dio una nueva secuencia para que siga trabajando. Acá está, es para la película que le sigue "The Lost World":
```
>DinoDNA from THE LOST WORLDp. 135
GAATTCCGGAAGCGAGCAAGAGATAAGTCCTGGCATCAGATACAGTTGGAGATAAGGACGGACGTGTGGCAGCTCCCGCAGAGGATTCACTGGAAGTGCATTACCTATCCCATGGGAGCCATGGAGTTCGTGGCGCTGGGGGGGCCGGATGCGGGCTCCCCCACTCCGTTCCCTGATGAAGCCGGAGCCTTCCTGGGGCTGGGGGGGGGCGAGAGGACGGAGGCGGGGGGGCTGCTGGCCTCCTACCCCCCCTCAGGCCGCGTGTCCCTGGTGCCGTGGGCAGACACGGGTACTTTGGGGACCCCCCAGTGGGTGCCGCCCGCCACCCAAATGGAGCCCCCCCACTACCTGGAGCTGCTGCAACCCCCCCGGGGCAGCCCCCCCCATCCCTCCTCCGGGCCCCTACTGCCACTCAGCAGCGGGCCCCCACCCTGCGAGGCCCGTGAGTGCGTCATGGCCAGGAAGAACTGCGGAGCGACGGCAACGCCGCTGTGGCGCCGGGACGGCACCGGGCATTACCTGTGCAACTGGGCCTCAGCCTGCGGGCTCTACCACCGCCTCAACGGCCAGAACCGCCCGCTCATCCGCCCCAAAAAGCGCCTGCTGGTGAGTAAGCGCGCAGGCACAGTGTGCAGCCACGAGCGTGAAAACTGCCAGACATCCACCACCACTCTGTGGCGTCGCAGCCCCATGGGGGACCCCGTCTGCAACAACATTCACGCCTGCGGCCTCTACTACAAACTGCACCAAGTGAACCGCCCCCTCACGATGCGCAAAGACGGAATCCAAACCCGAAACCGCAAAGTTTCCTCCAAGGGTAAAAAGCGGCGCCCCCCGGGGGGGGGAAACCCCTCCGCCACCGCGGGAGGGGGCGCTCCTATGGGGGGAGGGGGGGACCCCTCTATGCCCCCCCCGCCGCCCCCCCCGGCCGCCGCCCCCCCTCAAAGCGACGCTCTGTACGCTCTCGGCCCCGTGGTCCTTTCGGGCCATTTTCTGCCCTTTGGAAACTCCGGAGGGTTTTTTGGGGGGGGGGCGGGGGGTTACACGGCCCCCCCGGGGCTGAGCCCGCAGATTTAAATAATAACTCTGACGTGGGCAAGTGGGCCTTGCTGAGAAGACAGTGTAACATAATAATTTGCACCTCGGCAATTGCAGAGGGTCGATCTCCACTTTGGACACAACAGGGCTACTCGGTAGGACCAGATAAGCACTTTGCTCCCTGGACTGAAAAAGAAAGGATTTATCTGTTTGCTTCTTGCTGACAAATCCCTGTGAAAGGTAAAAGTCGGACACAGCAATCGATTATTTCTCGCCTGTGTGAAATTACTGTGAATATTGTAAATATATATATATATATATATATATCTGTATAGAACAGCCTCGGAGGCGGCATGGACCCAGCGTAGATCATGCTGGATTTGTACTGCCGGAATTC
```
Identificar la fuente de esta secuencia usando BLASTn.

> 7. ¿Cuál es la contaminación?
> 8. Si usamos BLASTx. ¿Cuál es el resultado? ¿Qué diferencias observa? Explicar qué e-value se obtiene y si se puede confiar en los resultados.
> 9. ¿Hay zonas de baja complejidad? ¿Dónde?

### Parte III: Olfatory receptor family

La familia de genes relacionada con "olfactory receptor activity" es la mayor familia génica en humanos.

Vamos a usar Gquery y BLAST para evaluar qué tan grande es esta familia.

> 1. ¿Cuál responde mejor la pregunta?

**Primero con Gquery:** Usar en _gquery_ los " " para que busque la frase entera.

Realizar una búsqueda en internet con gquery ncbi.

> 2. ¿Cuántos genes hay?

**Ayuda** : Usar Gquery ncbi en la base de datos **Gene** : solo organismo **Human** y buscar "olfactory receptor activity" usando el campo "gene ontology"

Segundo, guarden alguna de las proteínas pertenecientes a la familia que encontraron, para realizar el BLAST:

Ahora haremos un blastp usando esta proteína y lo vamos a BLASTEAR contra la base RefSeq solo del genoma humano.

Antes de hacer click en BLAST, vayan al final de la página, hagan click en "+Algorithm Parameters" y en la Opción "Max Target Sequences" elijan 1000

> 3. ¿Qué e-value usarían como cutoff?
> 4. ¿Cuántos hits y secuencias obtienen?

**Ayuda** : Pueden hacer un_ **download** _ del archivo _hit table (txt)_ y luego en la terminal contar _hits_.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/download_hits.jpg)

Contar en terminal usando:
```
wc -l y grep
```
Recordar el uso del pipe "pipe"

Solución:
```
cut -f 2 T2UCVF00014-Alignment.txt | fgrep -v "#" | sort -u | wc -l
```
**Preguntas** :

> 5. ¿Cuán parecidas son las secuencias entre los miembros de esta familia? Dar un ejemplo entre dos miembros.
> 6. ¿Cuándo buscamos por Gquery ncbi cuántas proteínas/genes de esta familia hay en el genoma humano?
> 7. ¿Cuándo hacemos un blastp usando como query una proteína perteneciente a la familia, contra la base de datos de proteínas refseq de human, cuántas proteínas encontramos? (con un e-value cutoff)
> 8. ¿Da el mismo número o no? ¿Por qué?

### Parte IV: Gquery y BLAST local

Utilice GQuery para realizar la búsqueda de las proteínas llamadas _Adenylosuccinate synthetase_ relacionadas con el metabolismo de purinas (_purine metabolism_) de _Drosophila_. Recuerde acotar los campos de búsqueda

> 1. ¿Cuántas proteínas aparecen en la búsqueda? (Escriba como realizó la búsqueda en Gquery remarcando cuales son los campos)
> 2. Identifique la proteína de mayor tamaño y responda:
> 	 - ¿Cuál es el tamaño de la proteína?
> 	 - ¿Cuál es su identificador único y su número de acceso?


Descargue la secuencia de aminoácidos del paso anterior mediante la línea de comandos de su máquina virtual y realice un BLAST contra la base de datos de proteínas humanas. Ayuda: puede utilizar **efetch.**

> 3. ¿Cuál es el largo de la proteína en aminoácidos?

Primero formateamos/Indexamos la base de datos:

Generaremos una "base de datos" a partir del archivo multifasta protein.fa para luego ejecutar un BLAST y buscar dentro de ese archivo con una secuencia "query"?

Es decir, debemos usar todas las secuencias del archivo como base de datos para la búsqueda. Para ello usaremos el archivo protein.fa de docs\_bioinformatica.

Para crear la DB vamos a usar el comando **"makeblastdb"**

Si queremos ver la ayuda para saber cómo se ejecuta el comando:
```
makeblastdb -help
```
Para indexar (crear la "base de datos") el archivo mutifasta que se llama human\_proteome.faa (o protein.fa) ejecuten:
```
makeblastdb -in archivo multifasta -dbtype prot -parse_seqids
```
**Nota:** Cambien el nombre según el archivo que ustedes tengan

Alineamos la secuencia query:

Vamos a alinear usando el comando **"blast"** y tomaremos como salida el formato tabular, después trabajaremos sobre esa salida para concluir cuáles de los hits obtenidos corresponden a homologos y cuáles no.

Fijemos el cutoff de un **e-value** \< 1.0E-6

**NOTA:** Para hacer el TP en clase usaremos solamente la secuencia del perro. Pueden practicar con las demás secuencias en su casa.

Para ver la ayuda recuerde que puede usar el parametro "-help"

Para hacer la búsqueda con BLAST ejecutar el comando:
```
blast*_?_* -db protein.fa -query <Archivo proteina query> -out blast_results_especie.tab -evalue 1.0E-6 -outfmt 6 -max_target_seqs 1000
```
> 4. ¿Cuántos Hits obtiene?
> 5. ¿Identifique las proteínas homólogas a su query y explique el criterio utilizado?

<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
