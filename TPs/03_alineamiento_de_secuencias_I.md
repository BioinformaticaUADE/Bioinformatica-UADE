# Trabajo Práctico 3 - Alineamientos de secuencias I

**Nota:** Para la práctica TP3 utilizaremos la maquina virtual creada y configurada en los TPs 1 y 2. Para ello abra VirtualBox y la maquina virtual.

Trabajaremos con los datos de:
```
/home/bioinformatica/Documentos/docs_Bioinformatica
```
Si tiene restringidos los permisos utilice chown para poder acceder a los archivos de la siguiente manera:

Desde el directorio:
```
/home/bioinformatica/Documentos
```
Ejecute:
```
sudo chown -R 755 docs_Bioinformatica
```
e ingrese la contraseña cuando se lo solicite. Recuerde que la contraseña es:

_pass: **bioinformatica**_

___

## Parte I: Parte I: Búsqueda de secuencias y alineamientos por dotplots

Buscamos secuencias para trabajar. Usar el firefox dentro de la MV, asi sera mas facil encontrar el archivo que descargaron.
La idea es trabajar con algunas secuencias homólogas, qué buscaremos en NCBI, para luego realizar algunos alineamientos.

Crear un directorio TP3, dentro de su directorio _ **"Documentos"** _, donde trabajaremos para este TP.
```
mkdir TP3
```
Para buscar las secuencias que vamos a usar para alinear, vayan al sitio URL: http://www.ncbi.nlm.nih.gov/gquery/

Usaremos la secuencia de la proteína **DSCAM** del cromosoma 21 de humanos y su homóloga en ratón (_Mus musculus_).

Con esas dos proteínas realizaremos algunos alineamientos.

_**Encontrar la secuencia de la proteína codificada por el gen DSCAM del cromosoma 21 (Isoforma CHD2-42) en Humanos usando "gquery" de pagina web ncbi.**_
> 1. ¿Cual es la sintaxis usada para realizar la busqueda?

Entrar a la base de datos "_**gene**_" e identificar el código que la identifica dentro de esa base de datos.

**Ayuda:** para visualizar todo el contenido de la página DSCAM dentro de la base "_gene_", primero condensar (achicar) todas las secciones de información de esa página. La base de datos "_gene_" contiene mucha información.

> 2. ¿Cual es su codigo NP (Código de secuencia de la base RefSeq)?
 
Guardar en formato "fasta" la secuencia. (por defecto se guarda en directorio "Downloads")

**Ayuda:**
- Usar los _links_ para llegar a su versión RefSeq de NCBI.
- Ir a la _webpage_ de cada secuencia y usar _link "Send to"_ en formato fasta.

O bien una vez identificado el código de acceso puede descargar la secuencia desde la terminal con el siguiente comando **_(recomendado)_**:
```
efetch -db sequences -id NP_001380 -format fasta > DSCAM_humana.fasta
```
**Nota:** recordar previamente activar el enviroment "análisis\_de\_secuencias

> 3. ¿Hay otros organismos que tengan ese gen? Nombrar alguno de estos organismos y el identificador de la proteína

**Ayuda** : Pueden usar los vínculos del panel de la derecha en la página web dentro de base "gene", por ejemplo, el link: HomoloGene, que contiene el resultado de una búsqueda de homólogos del gen en otras especies, que ya fue realizado y se muestra en ese link como un lista.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/link_help_1.jpg)

Encuentren y guarden la secuencia de proteína del gen DSCAM de **Mus musculus** **(usando la lista de HomoloGene) en formato "fasta"**

**Ayuda:** Ir a la _webpage_ de cada secuencia y usar _link "Send to"_ en formato fasta.

Copie ambos archivos con las secuencias descargadas al directorio TP3 y cambien los nombres por unos acorde a su contenido

_O ben una vez identificado l odigo de acceso puede directamente descargarlo a la terminal:_
```
efetch -db sequences -id NP_112451 -format fasta > DSCAM_raton.fasta
```
## Parte II: Alineamiento de a pares de proteínas

Primero vamos a alinear la secuencia proteica de_ **Homo sapiens** _ contra la de_ **Mus musculus** _

> 4. ¿Por que querriamos hacer este tipo de alineamiento?

**Ayuda:** Para conocer la "sintaxis" correcta para ejecutar el programa pueden usar el parámetro "-h" (Ejemplo"dottup -h")

Hacemos un "dot-plot" de estas dos secuencias

Para esto vamos a usar dos comandos del paquete _emboss_:

- _**dottup** (Displays a wordmatch dotplot of two sequences)_
- _**dotmatcher** (Draw a threshold dotplot of two sequences)_

**Ayuda:** Ejemplo de línea de comandos para ejecución:
- lo qué está **\<nombre\_archivo\_1\>** debe ser reemplazado por nombre de archivo como lo tienen ustedes.
```
dottup -graph png -asequence nombre_archivo_1 -bsequence nombre_archivo_2
```
**Nota:** Recuerde ejecutar ls o ll para observar los archivos creados. El archivo de extensión .png puede ser abierto con el programa eog. Para ello instálelo:
```
sudo apt install eog
```
y luego puede ejecutarlo haciendo:
```
eog nombre_de_archivo.png
```
  Primero alineamos usando _**dottup**_
  > 5. ¿Qué ocurre si variamos el parámetro _wordsize_?
  Ahora alineamos usando _**dotmatcher**_ variando los parámetros _windowsize_ y _threshold_
  > 6. ¿Cuales son los valores por defecto?
  > 7. ¿Que ocurre al variar el _windowsize_ o _threshold_? Informar diferencias observadas. (**Ayuda:** Pasen de un _windowsize_ de 10 a uno de 200)
  > 8. Supongan que usan un valor de _windowsize_ igual a 5 y el _threshold_ por defecto. ¿La figura muestra todos los alineamientos posibles? ¿Porque? Si la respuesta es NO, ¿como harian para verlos todos?
  > 9. ¿Que hace cada uno de estos programas?

Ahora alineamos la secuencia de _**Homo Sapiens**_ con las secuencias de los archivos que YA se encuentran en la VM:

Los archivos están en el directorio:
```
/home/bioinformatica/Documentos/docs_Bioinformatica
```
**Archivos:**

- DSCAM\_homo\_sapiens\_isoform1.fasta

- DSCAM\_homo\_sapiens\_isoform2.fasta

**Nota:** Hagan una copia de estos archivos en el directorio que crearon al principio del TP (directorio TP3). Asi evitan borrar archivos originales sin querer!!!!

Utilizando _**dotmatcher**_ y _**dottup**_ alineamos cada una de las dos isoformas con la proteína de humanos y luego las dos isoformas entre sí:

**Ayuda:** Tenemos que hacer 3 alineamientos:

- DSCAM\_homo\_sapiens\_isoform1.fasta vs NP\_001380
- DSCAM\_homo\_sapiens\_isoform2.fasta vs NP\_001380
- DSCAM\_homo\_sapiens\_isoform1.fasta vs DSCAM\_homo\_sapiens\_isoform2.fasta

> 10. ¿Que interpretan de los resultados?
> 11. ¿Cuales son las diferencias entre las secuencias?

## Parte III: Alineamiento de a pares de ácidos nucleicos

Descargue las secuencias de los genomas de SARS-CoV-2 y SARS y compárelas usando _**dotmatcher.**_

Utilice -threshold 23 -windowsize 10, -threshold 23 -windowsize 77 y -threshold 37 -windowsize 77

Para descargar las secuencias ejecute:
```
efetch -db nucleotide -id NC_004718.3 -format fasta > sars.fasta
```
```
efetch -db nucleotide -id NC_045512 -format fasta > sars-cov2.fasta
```
Use distintos nombre para poder comparar los resultados usando la opción -goutfile:
```
dotmatcher -graph png -asequence sars-cov2.fasta -bsequence sars.fasta -threshold XX -windowsize XX -goutfile names
```
Cambie **names** por el tipo de comparación que se está haciendo dependiendo del Windows size y el threshold usado.

Ahora utilice dottup:
```
dottup -graph png -asequence sars-cov2.fasta -bsequence sars.fasta -goutfile dottup_corona
```
> 12. ¿Que tipo de secuencias está usando?
> 13. ¿Que diferencias observa entre los distintos plots y a que adjudica esas diferencias?
> 14. ¿Qué sucede al aumentar el threshold?
> 15. ¿Qué regiones encuentra más similares? ¿Por qué cree que sucede esto?
> 16. ¿Cuáles serían los pasos a seguir para probar su hipótesis?

<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
