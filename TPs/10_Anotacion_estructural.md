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

1. ¿Cuál de las primeras opciones considera adecuada para un output de proteínas para este organismo?

El nombre de las secuencias ORF se construye a partir del nombre de la secuencia de entrada con un carácter de subrayado ('\_') y un número único del ORF que se encuentra adjunto. La descripción de la secuencia del ORF de salida se construye a partir de la descripción de la secuencia de entrada con las posiciones inicial y final del ORF antepuestas. El número único adjunto al nombre se utiliza simplemente para crear nuevos nombres de secuencia únicos, no implica ninguna información adicional que indique ningún orden, posición o hebra de sentido de los ORF. Si el ORF se ha encontrado en el sentido inverso, entonces la posición inicial será menor que la posición final y la descripción también contendrá '( **REVERSE SENSE** )'.
```
getorf -minsize ? -sequence scaffold\_4.fasta -find ? -outseq orfs.fa
```
1. ¿Cuántos ORF en sentido forward tienen?
2. ¿Y en sentido reverse?
3. ¿Cuál de todos los marco de lectura (ORF) es el que más chances tiene de ser correcto? ¿Por qué?

(Nota: Pueden filtrar por tamaño de ORF usando el parámetro _minsize_)

## Parte 2. Métodos Ab initio para la búsqueda de ORF/Genes

Ahora utilizaremos el programa Augustus ([http://augustus.gobics.de/](http://augustus.gobics.de/)).

AUGUSTUS es un programa de predicción génica para eucariotas. Se puede utilizar como programa ab initio, lo que significa que basa su predicción únicamente en la secuencia. AUGUSTUS también puede incorporar informacion sobre la estructura genética que provienen de fuentes extrínsecas como EST, , alineamientos de proteínas y alineamientos de genomas.

Actualmente, AUGUSTUS ha sido entrenado para predecir genes en distintas especies de organismos:

augustus --species=help

1. ¿Cuáles de las especies le parece la mas indicada para usar en la predicción?

augustus --cds=on --species=fly --genemodel=complete --gff3=on draft\_assembly.fasta --UTR=on \> augustus\_pred.out

El archivo **augustus\_pred.out** contiene la salida del programa augustus.

1. ¿Qué componentes identifica en el archivo?
2. ¿Cuántos genes fueron predichos?

Verifique el parámetro "--genemodel=complete".

1. ¿Qué ocurriría si usa otra opcion?

Puede obtener las secuencias de los genes usando herramientas provistas por el programa augustus

getAnnoFasta.pl augustus\_pred.out --seqfile=scaffold\_4.fasta

1. ¿Qué tipo de secuencias identifica? ¿Cua es la diferencia entre cada uno de estos archivos que se generaron?

La localizacion de islas CpG es muy útil como patrón para la identificación de genes ya que usualmente las Islas CpG se localizan upstream o solapando muchos genes ya que contienen sitios de unión a factores de transcripción. Usaremos el programa _ **cpgplot** _ para identificar su localización.

Identificar las islas CpG usando el programa _ **cpgplot** _.

cpgplot -sequence scaffold\_4.fasta -window 70 -outfeat CpG.gff

1. ¿Cuántas islas identifica?

Ahora visualizaremos el scaffold anotado en Artemis ([https://www.sanger.ac.uk/tool/artemis/](https://www.sanger.ac.uk/tool/artemis/)) que permite como entrada los archivos de anotación generados.

Para abrirlo ejecutar en la terminal:

art

cargar el archivo fasta scaffold\_4.fasta

![](RackMultipart20230614-1-t27iob_html_7c2033270d0c3011.png)

Al cargar el archivo, este programa automáticamente analiza los 6 posibles marcos de lectura y los presenta en la pantalla:

![](RackMultipart20230614-1-t27iob_html_78f2469cda2e49af.png)

Ahora cargaremos los archivos de anotación generados por **augustus** y por _ **cpgplot.** _

![](RackMultipart20230614-1-t27iob_html_1b16b8e44fa83f2b.png)

En **File** seleccionamos **read Entry** y cargamos el archivo **augustus\_pred.out** y **CpG.gff.**

Identifique los elementos que componen a los genes. ¿Qué elementos observa?

Vaya a la posición:

1. 926571
2. 1557373

Visualice las estructuras genómicas:

1. ¿Cómo está conformado el gen? ¿Cuántos CDS lo componen? ¿Qué significan las líneas que unes los rectángulos?

1. ¿Poseen Islas CpG asociadas?

1. ¿Cuál podría ser su función?

Puede hacer una búsqueda directa en Pfam para contestar esta pregunta:

![](RackMultipart20230614-1-t27iob_html_b4483d514f655ae6.png)

Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023
