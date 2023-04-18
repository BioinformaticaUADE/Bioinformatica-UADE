# TP 9: Ensamblado de genomas y calidad del ensamblado

En el TP9 utilizaremos datos de NGS. Por lo tanto, necesitaremos instalar las herramientas bioinformáticas adecuadas para la manipulación y el análisis de los datos de NGS.

Comenzaremos creando el enviroment _**ngs\_env.**_

Para ello ejecutaremos conda:
```
conda create -n ngs_env samtools bamtools bedtools cap3 quast fastqc spades emboss exonerate chromosomer blast entrez-direct sra-tools emboss bwa bowtie2 busco
```
Para activar el nuevo environment ejecutar:
```
conda activate ngs_env
```
**NOTA:** El enviroment ya esta instalado en sus VMs

### _Parte I:_ Ensamblado de genomas

En la carpeta datos\_02 encontrará los archivos de lecturas para realizar el ensamblado _de novo_ usando Spades ([_https://cab.spbu.ru/software/spades/_](https://cab.spbu.ru/software/spades/)). Realizaremos el ensamblado con y sin lecturas de long reads provenientes de PacBio.

¿Qué tipo de lecturas identifica?
```
spades.py --pe1-1 L1_map_map_R1.fq --pe1-2 L1_map_map_R2.fq --pe2-1 L2_map_map_R1.fq --pe2-2 L2_map_map_R2.fq --s1 L1_single.fq --s2 L2_single.fq --careful -t 2 -k 21,33,55,77,99 -o short_assembly
```

```
spades.py --pe1-1 L1_map_map_R1.fq --pe1-2 L1_map_map_R2.fq --pe2-1 L2_map_map_R1.fq --pe2-2 L2_map_map_R2.fq --s1 L1_single.fq --s2 L2_single.fq --pacbio long_reads.fasta --careful -t 2 -k 21,33,55,77,99 -o long_assembly
```
1. ¿Qué significan cada uno de los parámetros?

Observar que se crearon las carpetas **short\_assembly y long\_assembly**. En dicha carpeta encontraremos el producto del ensamblado en un archivo llamado **contigs.fasta.**

Verificar el número de contigs de los ensamblados. Para ello ejecutar el siguiente comando para cada archivo fasta:
```
grep -c ">" assembly*/contigs.fasta
```
2. ¿Cuántos contigs contiene cada uno de los ensamblados?, ¿cuál de ellos tiene menor número de contigs? ¿Cuál es la diferencia con el archivo scaffolds.fasta?

Ahora analizaremos el ensamblado estadísticamente evaluando el número de contigs y tamaño de contigs de forma manual:
```
infoseq contigs.fasta | awk '{OFS="\t"; print $3, $6, $7}' | sort -k2hr | grep "NODE"
```
Puede usar head al final de la línea para ver las primeras líneas

3. ¿Qué información brinda la salida de este comando?
4. ¿Cómo están ordenados y para que serviría esta información?
5. ¿Cuál es el contigs más largo?

Existen softwares especializados para calcular las métricas necesarias y evaluar la calidad de los ensamblados. En esta práctica utilizaremos el software Quality Assessment Tool for Genome Assemblies (QUAST: [http://bioinf.spbau.ru/quast](http://bioinf.spbau.ru/quast))

Desde la carpeta " **01\_ensamblado"** , ejecutamos la siguiente línea de comando:
```
quast.py short_assembly/contigs.fasta -o quast_short
```

```
quast.py long_assembly/contigs.fasta -o quast_long
```
o bien puede correr Quast sobre los 2 archivos en simultaneo.

En la carpeta quast\_short y quast\_long encontraremos los resultados de la evaluación.

Podemos abrir el resultado haciendo:

firefox report.html

Responda:

6. ¿Qué parámetros se muestran en el reporte?
7. ¿Cuál es el N50 del ensamblado?
8. ¿Cuál es el tamaño del contig más largo?
9. ¿Cuál es el porcentaje de GC?
10. ¿Cómo interpreta el grafico de Cumulative length?
11. Basado en el N50, ¿Cuál es el mejor ensamblado?
12. Basado en el tamaño de contigs, ¿Cuál es el mejor ensamblado?
13. Completar la siguiente tabla:


| N50 | N75 | Nº de Contigs | Tamaño de contig más largo |
| --- | --- | --- | --- |
| Short assembly | | | | |
| Long assembly | | | | |



14. Basado en estos análisis ¿Cuál es el mejor ensamblado?
15. ¿Qué otros análisis restarían realizar para completar la evaluación del ensamblado?


<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
