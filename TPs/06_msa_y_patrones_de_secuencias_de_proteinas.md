# TP6 - Alineamientos Múltiples (MSA) y Patrones

## Parte 1

Utilice GQuery para realizar la búsqueda de las proteínas, factores de transcripción "transcription factor 19" de Ornitorrinco "Ornithorhynchus anatinus" como realizó en el TP anterior.

Descargue la secuencia:
```
efetch -db sequences -format fasta -id "numero de acceso de la secuencia de la especie" > ornitorrinco.fasta
```
Realice la búsqueda de Dominios usando INTERPRO ([https://www.ebi.ac.uk/interpro/](https://www.ebi.ac.uk/interpro/)) el cual hace uso de varias bases de datos secundarias en simultaneo.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/interpro.jpg)

Copie y pegue la secuencia de la proteína en el cuadro de secuencia. Luego clickee en los resultados observe la información que le da el resumen (overview):

> 1. ¿Qué información le brinda?

Clickee Entries y seleccione la de PFAM.

> 2. ¿Qué Dominio encontró? ¿De qué proteína se trata? Indique la función.
> 3. ¿Cuál es la posición en la que se encuentra el Dominio?
Ingrese a la familia en summary: 
> 4. ¿Qué información relevante puede extraer?
> 5. Los clanes son agrupaciones de familias de proteínas relacionadas que comparten un solo origen evolutivo, confirmado por comparaciones estructurales, funcionales, de secuencia y HMM.
> 6. ¿A qué clan pertenece esta proteína y cuantas familias contiene?
> 7. ¿Qué organismos contienen este tipo de Dominios?

Ahora realice la búsqueda en la base de datos PROSITE ([https://prosite.expasy.org/](https://prosite.expasy.org/)).

> 8. ¿Qué proteína tuvo hit? ¿Coincide con PFAM?

Ingrese al código PROSITE y conteste:

> 9. ¿En qué organismos se encuentra? ¿Cuál es la expresión regular del Dominio?
> 10. Identifique el LOGO del dominio.
> 11. Identifique la matriz del perfil que hay detrás del dominio encontrado

## Parte 2

La búsqueda de Dominios usando PFAM, también puede realizarse de manera local. Para ello debemos descagar la base de datos PFAM.
[Pfam-A.hmm.gz](https://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz)

```
wget --no-check-certificate https://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz
```
Una vez descargada la descomprimimos de la siguiente manera:
```
gzip -d Pfam-A.hmm.gz
```
El paso hmmpress es necesario para que hmmscan funcione.

Se crean cuatro archivos: hmmfile.h3m, hmmfile.h3i, hmmfile.h3f y hmmfile.h3p. El archivo hmmfile.h3m contiene los HMM de perfil y su anotación en formato binario. El archivo hmmfile.h3i es un índice SSI para el archivo hmmfile.h3m. El archivo hmmfile.h3f contiene estructuras de datos precalculadas para el filtro heurístico rápido (el filtro MSV). El archivo hmmfile.h3p contiene estructuras de datos precalculadas para el resto de cada perfil.
```
hmmpress Pfam-A.hmm
```

```
hmmscan --pfamtblout results_pfam.txt --domtblout results_domains.txt --tblout results_hmmer_table.txt Pfam-A.hmm ornitorrinco.faa > results_hmmer.txt
```
> 1. ¿Qué interpreta del output en cada archivo?
> 2. ¿En qué posición se encuentra el patrón encontrado? ¿Coincide con el encontrado en PFAM? ¿Por qué?
> 3. ¿Cuáles residuos están mejor ponderados?

## Parte 3

_A partir del alineamiento multiple realizado en el TP anterior construiremos un modelo HMM para encontrar un patron en la secuencia de la proteína del ornitorrinco._

Abra el alineamiento de proteínas realizado en el TP anterior con jalview y edite el alineamiento conservando solo las regiones que mejor alinean. Remueva las regiones 288-374 y 1-33. Puede eliminarlas presionando CTRL+X. Empiece de atrás hacia adelante así no cambian las coordenadas.

Guarde el nuevo alineamiento como edited\_msa.fasta y cierre jalview.

Ahora generará el modelo HMM que usará para encontrar patrones en la secuencia del ornitorrinco. Para ello ejecute:
````
hmmbuild tp6.hmm edited_msa.fasta
````
indexe el modelo:
```
hmmpress tp6.hmm
```
Ahora puede realizar la búsqueda usando hmmscan:
```
hmmscan --pfamtblout results_msa_pfam.txt --domtblout results_msa_domains.txt --tblout results_msa_hmmer_table.txt tp6.hmm ornitorrinco.faa > results_msa_hmmer.txt
```
> 1. ¿Qué interpreta del output?
> 2. ¿En qué posición se encuentra el patrón encontrado? ¿Coincide con el encontrado en PFAM? ¿Por qué?
> 3. ¿Cuáles residuos están mejor ponderados?

<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
