## TRABAJO PRACTICO Nº 11

## Introducción A La Genómica Comparativa

### Parte I: Mapeo De Lecturas

Supongamos que queremos comparar dos genomas filogenéticamente no tan distantes y queremos observar diferencias en la secuencia o estructura de los genomas. Por ejemplo dos especies de _Echinococcus._ Contamos entonces con un genoma de referencia y con lecturas de secuenciación de una nueva especie de _Echinococcus_. Las estructuras o elementos que pueden identificarse mediante esta técnica son denominadas variantes y pueden ser de cambios de un único nucleótido (Single Nucleotide Polymorphism; SNP ), pequeñas inserciones o deleciones (Insertions, Deletions; INDELs ) o variantes estructurales (Structural Variants; SV ) como las variantes del número de copias (Copy Number Variations; CNVs ).

En esta sección realizaremos el alineamiento de las lecturas de secuenciación sobre una referencia " **ref.fa"** usando BOWTIE2 ([http://bowtie-bio.sourceforge.net/bowtie2/index.shtml](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml). Este programa es un alineador de secuencias que se usa con lecturas cortas las cuales son comparadas y alineadas sobre un genoma de referencia para análisis de genoma completos, ensamblado, análisis de variantes genéticas y genómicas. Es un alineador rápido y eficiente ya que consume poca memoria a nivel computacional. Su eficiencia se debe en parte a la implementación de la transformación Burrows – Wheeler. Otros programas que usan el mismo algoritmo con métodos similares son BWA y SOAP2.

En primer lugar realizaremos un mapeo de secuencias sobre la referencia utilizando BOWTIE2 que tomará como entrada las lecturas en formato fastq. Luego usaremos herramientas para la manipulación de datos de mapeo tals como SAMtools ([http://samtools.sourceforge.net/](http://samtools.sourceforge.net/)), BAMtools ([https://github.com/pezmaster31/bamtools](https://github.com/pezmaster31/bamtools)), PicardTools ([https://broadinstitute.github.io/picard/](https://broadinstitute.github.io/picard/)) .

**Mapeo:**

En **files\_TP10.zip** en OneDrive encontrarán los archivos necesarios para realizar el TP en C**lase\_13. (O en la maquina virtual bajo el nombre "files\_TP11.tar.gz")**

Para comenzar crearemos la carpeta " **TP9** en **Documentos**" y copiarán las secuencias fastq y el archivo de referencia fasta.

Antes de empezar en la maquina virtual activar el enviroment ngs\_env e instalar las herramientas necesarias:
```
conda activate ngs_env
```
```
conda install picard bcftools igv
```
Ahora indexamos el genoma de referencia " **ref.fa**"
```
bowtie2-build -f ref.fa ref
```
Y alineamos las lecturas sobre el genoma de referencia el cual dará por resultado un archivo en formato SAM. El formato SAM ( http://samtools.github.io/hts-specs/SAMv1.pdf ) consiste en texto delimitado por tabs el cual tiene un encabezado (líneas que comienzan con @) con información general del secuenciamiento y del alineamiento, más una sección de alineamientos con 11 campos obligatorios y otros campos opcionales. Cada renglón de la sección de alineamientos corresponde a una lectura del secuenciador.
```
bowtie2 -I 300 -X 600 -x ref --fr -1 L1_map_map_R1.fq -2 L1_map_map_R2.fq -1 L2_map_map_R1.fq -2 L2_map_map_R2.fq -U L1_single.fq -U L2_single.fq -S mapped.sam
```
Luego de haber obtenido el SAM, el mismo el mismo es transformado en un archivo de formato BAM, el cual es la representación binaria de la misma información (está comprimido y ya no lo podemos leer con un editor de texto).
```
samtools view -b -S mapped.sam > mapped.bam
```
Ordenamos las lecturas con el siguiente comando:
```
samtools sort -o mapped.sorted.bam mapped.bam
```
Mediante el siguiente comando podemos calcular estadísticas de mapeo y propiedades de las lecturas y bibliotecas de secuenciación.
```
bamtools stats -in mapped.sorted.bam -insert \> stats.txt
```
Para observar el archivo stats.txt usar "less". Para salir presione la letra "q"

Luego se marcan las duplicaciones de secuencia producto de artefactos de la PCR.
```
picard SortSam INPUT=mapped.sorted.bam OUTPUT=mapped.sbc.bam SORT\_ORDER=coordinate VALIDATION\_STRINGENCY=LENIENT
```
```
picard MarkDuplicates INPUT=mapped.sbc.bam OUTPUT=mapped.mkd.bam METRICS\_FILE=merged.sbc.metrics VALIDATION\_STRINGENCY=SILENT
```
Ahora podemos calcular la cobertura y profundidad del mapeo de secuencias:
```
bedtools genomecov -bga -ibam mapped.mkd.bam \> coverage\_a.txt
```
```
bedtools genomecov -d -ibam mapped.mkd.bam \> coverage\_b.txt
```
Inspeccione los archivos stats.txt, coverage\_a.txt y coverage\_b.txt:

> 1. ¿Qué observa? ¿Cómo lo interpreta? ¿Cuál es el promedio de profundidad? ¿Cubrió toda la secuencia?

Ingrese a R o Rstudio, cargue el archivo coverage\_b.txt y grafique V4 vs V3:

> 2. ¿Que observa? ¿Qué significan los picos? ¿Cómo lo interpreta? ¿A qué cree que se deban los picos observados? ¿Qué información biológica puede extraer de esta observación?

_ **Nota** __: El punto 2 lo realizaremos la próxima clase que aprenderemos R._

Ahora realizaremos el llamado de variantes genéticas usando bcftools. BCFtools es un programa para llamar variantes y manipular archivos en el formato de variant calling (VCF) y su contraparte binaria BCF. Todos los comandos funcionan de forma transparente tanto con VCF como con BCF, tanto sin comprimir como con BGZF.

Realizaremos el llamado de variantes crudas sin filtrar con el siguiente comando:

bcftools mpileup -d 20000 -f ref.fa mapped.mkd.bam | bcftools call -Amv -Ob | bcftools +fill-tags \> raw\_variants.vcf

Posteriormente aplicaremos filtros básicos para quedarnos con las variantes que cumplen ciertos criterios y de esta forma otorgan mayor confianza a los datos:

**Soft Filtering:**

cat raw\_variants.vcf | bcftools filter -s "lowQual" -i 'DP\>=20 && MQ\>=20 && QUAL\>=20' \> SF\_varcalls.vcf

**Hard Filtering:**

cat raw\_variants.vcf | bcftools filter -i 'DP\>=20 && MQ\>=20 && QUAL\>=20' \> HF\_varcalls.vcf

1. Inspeccione los archivos VCF generados:
2. ¿Qué diferencias encuentra entre ellos? ¿Qué criterios de filtrado se usaron? ¿Dónde observa esa información en el VCF?
3. ¿Qué tipo de variantes reconoce?
4. ¿Cuántas posiciones quedaron luego de aplicar el filtro?

### Parte II: Visualización De Los Datos

A continuación exploraremos de un modo gráfico el contig con los reads mapeados sobre la referencia y la anotación génica asociada. Para ello utilizaremos el programa "Integrative Genomics Viewer" (IGV [http://software.broadinstitute.org/software/igv/](http://software.broadinstitute.org/software/igv/)) que permite ingresar secuencias en formato fasta y cargarle información de la localización génica y alinemiento de lecturas, etc. Para una mejor interpretación de la visualización puede consultar la guía del programa IGV ([http://software.broadinstitute.org/software/igv/DefaultDisplay](http://software.broadinstitute.org/software/igv/DefaultDisplay)).

Primero creamos el índice del archivo bam necesario para la visualizacion con IGV:

samtools index mapped.mkd.bam

Para eso escribimos en la consola "igv". En Genome clickeamos en "load from file" y seleccionamos nuestro archivo " **ref.fa**". Luego cargamos el archivo con las anotaciones "file.gff". Para ello en File clickeamos en "load from file" seleccionamos el archivo de anotación. Luego en la ventana anotación hacemos click derecho y elegimos "expanded". Podemos hacer zoom en la parte superior derecha.

A continuación, cargamos el archivo " **mapped.mkd.bam**". De igual manera clickeamos en "load from file" y seleccionamos el archivo bam. Explore las secuencias, genes y coverage. No olvide hacer zoom.

1. Muévase a la posición 20000 y describa lo que observa. ¿Qué tipo de variante genética encuentra? ¿Se está afectando alguna unidad génica?

Ahora cargue los archivos VCF generados.

1. ¿Qué observa? Qué variantes son las más confiables ahora?
2. Vaya a la posición "E.canG7\_contigs\_6081:307,520-307,865". Identifique las variantes que pasaron los filtros y responda:
3. ¿Cuál es su heterocigocidad?
4. ¿Qué tipo de variantes presenta?
5. ¿Qué otra información relevante encuentra?

Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023
