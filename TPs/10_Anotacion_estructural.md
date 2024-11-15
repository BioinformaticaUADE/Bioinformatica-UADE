# TP 10: Anotación estructural

**En este trabajo Práctico realizaremos la anotación estructural de un scaffold correspondiente al genoma de una mosca.**

Los archivos necesarios para la realización del TP se encuentran en OneDrive.

Vamos a trabajar con la secuencia del scaffold\_4.fasta y tratar de encontrar los genes dentro de ella. Para esto vamos a determinar métodos ab initio para la localización de marcos abiertos de lectura potenciales donde estaría localizados los genes.

Crear la carpeta TP9 en la carpeta Documentos y copiar los archivos necesarios.

Instalaremos además el enviroment de anotación augustus
```
conda create -n augustus augustus artemis
```
```
conda activate augustus
```
## Parte 1. Fuerza bruta para la búsqueda de ORF

Para buscar genes usaremos el programa _ **getorf** _ _de emboss_ que permite buscar ORF en una secuencia query. Este programa tiene distintos parámetros para su uso uno de ellos consiste en la forma de buscar ORF:

Las primeras cuatro opciones son seleccionar la traducción de la proteína o la secuencia de ácido nucleico original del marco de lectura abierto. Hay dos definiciones posibles de un marco de lectura abierto: puede ser una región libre de codones STOP o una región que comienza con un codón START y termina con un codón STOP. Las últimas tres opciones probablemente solo interesen a las personas que deseen investigar las propiedades estadísticas de las regiones alrededor de los posibles codones START o STOP. La última opción supone que las longitudes de ORF se calculan entre dos codones de PARADA.

Valores:

 0 - ( **Translation** of regions between STOP codons)
 
 1 - ( **Translation** of regions between START and STOP codons)
 
 2 - ( **Nucleic** sequences between STOP codons)
 
 3 - ( **Nucleic** sequences between START and STOP codons)
 
 4 - (Nucleotides flanking START codons)
 
 5 - (Nucleotides flanking initial STOP codons)
 
 6 - (Nucleotides flanking ending STOP codons)


> 1. ¿Cuál de las primeras opciones considera adecuada para un output de proteínas para este organismo?

El nombre de las secuencias ORF se construye a partir del nombre de la secuencia de entrada con un carácter de subrayado ('\_') y un número único del ORF que se encuentra adjunto. La descripción de la secuencia del ORF de salida se construye a partir de la descripción de la secuencia de entrada con las posiciones inicial y final del ORF antepuestas. El número único adjunto al nombre se utiliza simplemente para crear nuevos nombres de secuencia únicos, no implica ninguna información adicional que indique ningún orden, posición o hebra de sentido de los ORF. Si el ORF se ha encontrado en el sentido inverso, entonces la posición inicial será menor que la posición final y la descripción también contendrá '( **REVERSE SENSE** )'.
```
getorf -minsize ? -sequence scaffold\_4.fasta -find ? -outseq orfs.fa
```
> 2. ¿Cuántos ORF en sentido forward tienen?
> 3. ¿Y en sentido reverse?
> 4. ¿Cuál de todos los marco de lectura (ORF) es el que más chances tiene de ser correcto? ¿Por qué?

(Nota: Pueden filtrar por tamaño de ORF usando el parámetro _minsize_)

## Parte 2. Métodos Ab initio para la búsqueda de ORF/Genes

Ahora utilizaremos el programa Augustus ([http://augustus.gobics.de/](http://augustus.gobics.de/)).

AUGUSTUS es un programa de predicción génica para eucariotas. Se puede utilizar como programa ab initio, lo que significa que basa su predicción únicamente en la secuencia. AUGUSTUS también puede incorporar informacion sobre la estructura genética que provienen de fuentes extrínsecas como EST, , alineamientos de proteínas y alineamientos de genomas.

Actualmente, AUGUSTUS ha sido entrenado para predecir genes en distintas especies de organismos:
```
augustus --species=help
```
> 1. ¿Cuáles de las especies le parece la mas indicada para usar en la predicción?
```
augustus --cds=on --species=fly --genemodel=complete --gff3=on draft_assembly.fasta --UTR=on > augustus_pred.out
```
El archivo **augustus\_pred.out** contiene la salida del programa augustus.

> 2. ¿Qué componentes identifica en el archivo?
> 3. ¿Cuántos genes fueron predichos?

Verifique el parámetro "--genemodel=complete".

> 4. ¿Qué ocurriría si usa otra opcion?

Puede obtener las secuencias de los genes usando herramientas provistas por el programa augustus
```
getAnnoFasta.pl augustus_pred.out --seqfile=scaffold_4.fasta
```
> 5. ¿Qué tipo de secuencias identifica? ¿Cua es la diferencia entre cada uno de estos archivos que se generaron?

La localizacion de islas CpG es muy útil como patrón para la identificación de genes ya que usualmente las Islas CpG se localizan upstream o solapando muchos genes ya que contienen sitios de unión a factores de transcripción. Usaremos el programa _ **cpgplot** _ para identificar su localización.

Identificar las islas CpG usando el programa _ **cpgplot** _.
```
cpgplot -sequence scaffold_4.fasta -window 70 -outfeat CpG.gff
```
> 6. ¿Cuántas islas identifica?

Ahora visualizaremos el scaffold anotado en Artemis ([https://www.sanger.ac.uk/tool/artemis/](https://www.sanger.ac.uk/tool/artemis/)) que permite como entrada los archivos de anotación generados.

Para abrirlo ejecutar en la terminal:
```
art
```
cargar el archivo fasta scaffold\_4.fasta

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/img1_tp10.jpg)

Al cargar el archivo, este programa automáticamente analiza los 6 posibles marcos de lectura y los presenta en la pantalla:

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/img2_tp10.jpg)

Ahora cargaremos los archivos de anotación generados por **augustus** y por _ **cpgplot.** _

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/img3_tp10.png)

En **File** seleccionamos **read Entry** y cargamos el archivo **augustus\_pred.out** y **CpG.gff.**

Identifique los elementos que componen a los genes. ¿Qué elementos observa?

Vaya a la posición:

1. 926571
2. 1557373

Visualice las estructuras genómicas:

> 7. ¿Cómo está conformado el gen? ¿Cuántos CDS lo componen? ¿Qué significan las líneas que unes los rectángulos?

> 8. ¿Poseen Islas CpG asociadas?

> 9. ¿Cuál podría ser su función?


<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
