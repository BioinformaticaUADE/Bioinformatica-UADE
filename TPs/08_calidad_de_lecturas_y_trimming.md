# TP 8: Análisis de calidad en NGS

En el TP7 utilizaremos datos de NGS. Por lo tanto, necesitaremos instalar las herramientas bioinformáticas adecuadas para la manipulación y el análisis de los datos de NGS.

Comenzaremos creando el enviroment ngs\_env.

Para ello ejecutaremos conda:
```
conda create -n ngs_env samtools bamtools bedtools cap3 quast fastqc spades emboss exonerate chromosomer blast entrez-direct sra-tools emboss bwa bowtie2 busco cutadapt
```

Para activar el nuevo environment ejecutar:
```
conda activate ngs_env
```
**NOTA:** El enviroment ya esta instalado en sus VMs

### Parte I: Archivos con formato "fastq"

Formato _fastq_:

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/fastq_format.jpg)

En la carpeta de **Onedrive** o en "docs\_Bioinformatica" encontrará los archivos necesarios para la realización del TP.

Cree la carpeta TP7 en Documentos, copie el archivo comprimido desde docs\_Bioinformatica a TP7 y descomprímalo
```
mkdir /home/bioinformatica/Documentos/TP7
```
```
cp /home/bioinformatica/Documentos/docs_Bioinformatica/archivos_TP8.tar.gz /home/bioinformatica/Documentos/TP7
```
Para descomprimir desde TP7 ejecutamos:
```
tar -xzvf archivos_TP8.tar.gz
```
En la carpeta **datos\_01** encontraremos los archivo **fastq** que vamos a usar. Este archivo fastq es una corrida de secuenciación (no cadena específica) de un plásmido de una bacteria:
```
reads_sample.fastq
```
En esta parte inicial vamos a trabajar con el formato de los archivos, para esto utilizaremos comandos de Linux para responder las preguntas.

> 1. ¿Cuántas lecturas tenemos en cada uno de los archivos fastq? ¿Cuántas líneas ocupa una secuencia en formato "fastq"? Resuelvan este problema de dos formas, una usando el comando _"grep"_ y otra usando el comando _"wc"_.

> 2. ¿Cuántas lecturas tienen el patrón **"ACCATCACCTGGAA"**?

> 3. ¿Como se llaman las lecturas con ese patron? Es decir, obtener identificador de esas lecturas

> 4. ¿Cuál es la calidad de esas mismas lecturas? (Impriman por pantalla esas calidades)

**Ayuda:** Para los puntos 3 y 4 prueben usando los parámetros -A y -B del comando "grep".

### Parte II: Control de calidad con "fastqc"

**"fastqc"** es un programa que nos permite ver estadísticas sobre la calidad de las lecturas, sin modificar en absoluto los archivos fastq.

URL doc: [http://www.bioinformatics.babraham.ac.uk/projects/fastqc/](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/)

Ver link para mas info de graficas de fastqc:

[http://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/)

Un ejemplo de datos de Illumina de baja calidad:

[http://www.bioinformatics.babraham.ac.uk/projects/fastqc/bad\_sequence\_fastqc.html](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/bad_sequence_fastqc.html)

Para ejecutar el programa "fastqc" tenemos que escribir en la terminal:
```
fastqc
```
Y abrir cada archivo

Al dar Enter en la terminal, se abrirá la interfaz gráfica de fastqc, con este programa vamos a procesar el archivo fastq (el mismo que usamos antes), para ver las figuras del resultado del análisis de calidad.

También puede ejecutar:
```
fastqc nombre_del_archivo.fastq
```
Puede utilizar comodines para correr fastqc a todos los archivos de secuenciación.

En este caso se generará el archivo html que puede abrir con Firefox

**Responda:**

> 1. Según "fastqc", ¿Cuantas lecturas tenemos? ¿Coincide con los valores obtenidos en la Parte I?

> 2. ¿Cual es el tamaño de las lecturas?. ¿Todas son iguales en tamaño?

> 3. ¿Como se distribuyen las calidades a lo largo de las secuencias? ¿Porque se produce una caída en la calidad al final?

> 4. ¿Como es la distribución de calidad promedio por lectura? ¿Son secuencias de buena calidad?

> 5. ¿Como es el contenido de bases a lo largo de las lecturas? ¿Notan algo extraño en la muestra?. Si es así ¿Cuál puede ser la razón?

> 6. ¿Es correcto que el contenido de G y de C por un lado y de A y T por otro, sean similares a lo largo de las lecturas? ¿Porqué?

> 7. ¿Pueden observar algún indicio de contaminación? ¿Porque?

### _Parte III:_ Trimming y filtrado por calidad de las lecturas

Ahora analice las calidad de los archivos fastq que están en la carpeta datos\_02. Las libraries fueron preparadas usando la tecnica de "tagmentation" en la cual una enzima transposasa corta y liga adaptadores a distancias equidistantes en posiciones "supuestamente al azar". Observe que hay 2 corridas de secuenciación, L1 y L2.

> 1. ¿De que tipo de libraries se trata?

> 2. ¿Cual es el tamaño promedio de las lecturas?

> 3. ¿Que puede decir respecto al contenido de GC?

> 4. ¿Que puede decir respecto a la calidad de las libraries L1 y L2?

> 5. ¿Realizaria un trimming de las secuencias de las libraries? ¿Cual de ellas?

Utilice cutadapt para realizar el trimming. Obtenga la ayuda del programa:
```
cutadapt -h
```
Revise el parametro "-l" y "-u"

Realice el recorte que considera necesario y vuelva a correr fastqc.


<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
