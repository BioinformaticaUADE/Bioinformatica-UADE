# TP7 - Modelado por Homología

La clase pasada realizamos los alineamientos múltiples de varias proteínas de gusanos parásitos y mamíferos (Humano y ratón) donde verificamos el grado de similitud e identificamos regiones conservadas, dominios y predicciones de estructura secundaria de las proteínas.

En el TP de hoy analizaremos la estructura completa de una proteína de parásito mediante un modelado por homología usando dos métodos diferentes. Modelado por homología mediante el uso de un Template y mediante Threading.

Para la realización del TP usaremos un programa de visualización llamado Pymol que puede encontrar aquí según su sistema operativo Host.

Descargue la versión del programa que corresponda y el archivo de licencia. Una vez que haya instalado el programa inícielo y cargue el archivo de licencia cuando se lo solicite.

**PyMOL Executable Builds for Educational Use Only:**

The Educational-use-only PyMOL builds are provided "AS IS" with no obligation to grant download access, fix bugs, furnish updates, provide documentation, or meet any other need related to the educational-use PyMOL builds. Purchased [PyMOL Academic Subscriptions](https://pymol.org/academic) with up to three years of maintenance are available to meet your longer-term educational use needs.

PyMOL 2.0 (September 2017)

_License File:_[_pymol-edu-license.lic_](https://pymol.org/ep/download-edu-lic-file.php)

_Installers:_[_PyMOL Download Page_](https://pymol.org/2/#download)

_DOWNLOAD URL:_ [_https://pymol.org/ep_](https://pymol.org/ep)

_USERNAME: jun2021_

_PASSWORD: betabarrel_

## Parte 1) Modelado por Homología con template único

En la primera parte del TP analizaremos la estructura completa de una proteína del parásito _H. contornus_ mediante un modelado por homología usando modelado por homología mediante el uso de un Template con la herramienta online Sswissmodel ([https://swissmodel.expasy.org/](https://swissmodel.expasy.org/)).

Debido a que los resultados tardan en ser computados estos ya han sido previamente calculados.

Para realizar el modelado por homología usando swissmodel, ud. Debe ingresar a la pagina [https://swissmodel.expasy.org/](https://swissmodel.expasy.org/) y clickear en start modelling y pegar la secuencia de la proteína query.
```
**>Hcontortus_HCON_00189600_1**
MKTVFLLGFLFLYSIGVFSEEDKKDVKYGTIIGIDLGTTYSCVGVYKNGRVEIIANDQGNRITPSYVAFSGDSGERLIGDAAKNQLTINPENTVFDAKRLIGRDYMDKTVQDDIKLWPFKVDNKNNKPMVSLKVGQEMKQFAPEEISAMVLTKMKEIAESYLGKEVKHAVVTVPAYFNDAQRQATKDAGTIAGLNVVRIINEPTAAAIAYGLDKKEGERNILVFDLGGGTFDVSMLTIDNGVFEVLATNGDTHLGGEDFDQRVMEYFIKIYKKKTGKDIRKDNRAVQKLRREVEKAKRALSTQHQVKVEVESLFDGEDFSESLTRAKFEELNMDLFRATLKPVQKVLEDSDLKKEDVHEIVLVGGSTRIPKVQQLIKDFFNGKEPSRGINPDEAVAYGAAVQAGVISGEESTGDIVLLDVNPLTLGIETVGGVMTKLITRNTVIPTKKSQVFSTAADNQPTVTIQVFEGERPMTKDNHQLGKFDLTNIPPAPRGVPQIEVTFEIDVNGILHVTAEDKGTGNKNKITITNDQNRLSPEDIERMINDAEKFAEDDKKVKEQVEARNELESYAYSLKNQIGDNEKLGGKLDADDKKTIETAVEETISWLESNREASVDDLKEHKKDLESKVQPIISKLYKDAGGGAGGDEGVPPTEEKDEL
```
Pegue la secuencia, complete los campos requeridos y haga click en Build Model.

![](img1_tp7)

Ud. Puede acceder a los resultados pre-calculados de SwissModel en:

[https://swissmodel.expasy.org/interactive/2BPQ8L/models/](https://swissmodel.expasy.org/interactive/2BPQ8L/models/)

La evaluación de la calidad del modelo es algo muy importante. El SWISS-MODEL realiza una **evaluación global** que permite establecer scores comparables entre modelos alternativos para la misma proteína y una evaluación de la estereoquímica a nivel local a través de gráficos por residuo. SWISS-MODEL presenta diferentes scores y gráficos de evaluación del modelo. **QMEAN4** es una función de scoring compuesta que usa 4 potenciales estadísticos: un potencial que evalúa ángulos de torsión a lo largo de tres residuos consecutivos (local), un potencial de interacción coarse grain basado en los CB de cada residuo, un potencial de interacción all-atom y un potencial de solvataciń que evalúa el grado de ocultamiento de los residuos. El score va de 0 a 1, siendo mejor el modelo cuanto mayor score presente. Los valores de Z-score de QMEAN permiten comparar el modelo con estructuras de referencia de tamaño similar resueltas experimentalmente con alta resolución. Da cuenta de contactos nativos en el modelo. Modelos de baja calidad tienen valores de Z-score muy negativos.

**Evaluación local** – Sección "Local Model Quality Estimation" En esta sección se muestran gráficos en función de cada residuo. Anolea (atomic non-local environment assesment) evalúa el ambiente relativamente distante de cada átomo pesado de la proteína usando un potencial de fuerza atómico promedio empírico (interacciones entre átomos que se hallan a más de 7 Å de distancia y que pertencen a residuos separados por más de de 11 residuos en la secuencia). Evalúa la calidad del plegamiento del modelo representando la energía para cada aminoácido. Valores pequeños indican energía favorable del entorno.

**QMEAN** usa un potencial similar al descripto más arriba más un agregado que tiene en cuenta que los loops expuestos al solvente que en general se predicen con menor precisión que las regiones con estructura secundaria definida. Valores bajos para el score local de QMEAN por resiudo (cercanos a 0) corresponden a zonas confiables del modelo.

> 1. ¿Cuántos modelos se obtuvieron, cuáles son los mejores modelos y en que se basa?
> 2. ¿Qué template se usaron para los dos mejores modelos? ¿Cuál de los dos considera que es mejor y por qué?
> 3. Identifique las regiones de menor calidad. ¿A qué se debe lo que observa?
> 4. ¿Qué porcentaje de identidad y cobertura se encontró con el template que considera otorgó el mejor modelo?
> 5. ¿Está alineada de principio a fin? ¿Por qué?
> 6. Debajo de la imagen de la estructura de la proteína en la rueda de configuración en Colour Scheme seleccione structure. ¿Qué estructuras secundarias identifica?
> 7. Ahora coloree por INDELs, ¿Dónde se localiza este elemento y a que aminoácidos afecta?
> 8. Clickee en Structure Assesment y describa lo que observa.
> 9. Ahora haga click en el código PDB y describa el método usado para la obtención de su estructura y resolución. ¿Qué otras propiedades puede describir?

Descargue el proyecto como Zip. Este contiene todos los modelos y los templates utilizados

## Parte 2) Modelado por homología por threading

En la segunda parte del TP analizaremos la estructura completa de una proteína del parásito _H. contornus_ mediante un modelado por threading usando modelado por homología con la herramienta online Phyre2 ([http://www.sbg.bio.ic.ac.uk/phyre2/html/page.cgi?id=index](http://www.sbg.bio.ic.ac.uk/phyre2/html/page.cgi?id=index)).

Debido a que los resultados tardan en ser computados estos ya han sido previamente calculados.

Para realizar el modelado usando Phyre2, ud. Debe ingresar a la pagina [http://www.sbg.bio.ic.ac.uk/phyre2/html/page.cgi?id=index](http://www.sbg.bio.ic.ac.uk/phyre2/html/page.cgi?id=index), completar los campos, pegar la secuencia de la proteína y clickear en Phyre search.

Ud. Puede acceder a los resultados pre-calculados de Phyre en:

[http://www.sbg.bio.ic.ac.uk/phyre2/webscripts/jobmonitor.cgi?jobid=a4f01717d76bf321](http://www.sbg.bio.ic.ac.uk/phyre2/webscripts/jobmonitor.cgi?jobid=a4f01717d76bf321)

Descargue el archivo comprimido para con todos los datos:

![](img2_tp7)

En la pagina de los resultados de Phyre2 explore y conteste:

> 1. ¿Cuantos templates se usaron? ¿Cuál fue el mejor template?
> > 2. ¿De qué proteína se trata? ¿Cuál fue la confianza, el % de identidad y cobertura del modelado? ¿Qué región del template fue utilizada?

Para analizar el modelo clickee en _View investigator results_

![](img3_tp7)

ProQ2 predice el llamado puntaje S para cada residuo individual (obtendrá un gráfico sobre este puntaje cuando haga clic en el enlace de cada puntaje). También cuenta con su propio servidor para evaluar las estructuras: [http://duffman.it.liu.se/ProQ2/](http://duffman.it.liu.se/ProQ2/)

> 1. Coloree por ProQ2. ¿Qué opina del modelo?
> 2. ¿Qué indica el análisis de Ramachandran?
> 3. Observe la sección _Sequence profile y Mutations._ ¿Qué interpreta de esos gráficos?
> 4. Localícese en la posición 480. ¿Qué amino ácido observa? ¿En qué estructura se localiza? ¿Qué observa en los gráficos de mutación y por qué?
> 5. Coloree por Function à Mutational Sensitivity. ¿Qué regiones serían las más afectadas por mutaciones?
> 6. Localice la región de unión a Ligando. ¿Dónde se encuentra y cuantos aminoácidos están involucrados y donde se encuentran?

**Nota** : The propensities of these amino acids to adopt β-sheet structures was widely known from their statistical occurrence in protein secondary structures (commonly referred to as the "Chou-Fasman parameters")[13](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2728010/#R13) and from empirical studies.[14](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2728010/#R14) Our studies showed that the propensities of valine and leucine to adopt β-sheet structure is greater than that of alanine, which in turn is greater than that of glycine (V, L \> A \> G). These results largely match the established propensities (V \> L \> A \> G) and demonstrate that even relatively simple model systems can provide information relevant to the folding and interactions of larger proteins.

## Parte 3) Visualización de estructuras en Pymol

PyMOL es un sistema de visualización molecular patrocinado por el usuario sobre una base de código abierto, mantenido y distribuido por Schrödinger. Existen muchos otros visualizadores que cumplen las mismas funciones o similares. Para fines prácticos solo utilizaremos el modelo generado por SWISS-MODEL. Si lo desea también puede realizar el mismo procedimiento co los modelos generados con Phyre2.

Ahora realizaremos una evaluación final de los modelos generados y sus templates mediante alineamiento de estructuras. Para comenzar ejecute el programa Pymol.

![](img4_tp7)

Para abrir los archivos de los modelos diríjase a File à open

Allí busque los modelos generados anteriormente por ambos métodos y sus respectivos templates.

![](img5_tp7)

De los modelos generados por SWISS-MODEL abra el modelo 1 y 2 y sus respectivos templates.

**NOTA:** Todos los modelos por default de asigna el nombre model. Para no sobrescribir el modelo abierto anteriormente cambie los nombres según corresponda model1, model2, etc

**Model\_01 + template** [5e84.3.A](https://swissmodel.expasy.org/templates/5e84.3)

**Model\_02 + template** [4fl9.1.A](https://swissmodel.expasy.org/templates/4fl9.1)

Observará que las estructuras aparecen superpuestas.

Puede cambiar el color de las moléculas clickeando en "C"

![](img6_tp7)

A: Actions
S: Show
H: Hide
L: Label
C: Colour

También puede colorear por estructura secundaria.

> 1. ¿Qué estructuras identifica? ¿Observa ligandos o cofactores? ¿De qué molécula de trata?

Puede mostrar la secuencia de la proteína seleccionando "S" en:

![](img7_tp7)

Puede acercar o alejar la imagen con el botón derecho del mouse y desplazando el mouse hacia arriba o hacia abajo.

**Una función importante es el RMSD que permite evaluar el modelo en referencia al template.** El resultado de un alineamiento estructural es una superposición de los conjuntos de coordenadas atómicas, así como una distancia media cuadrática mínima (o  **RMSD** , de Root Mean Square Deviation, o desviación de la media cuadrática) entre las estructuras básicas de las proteínas superpuestas. Cuanto mejor es el alineamiento menor es el valor de RMSD.
```
align model_, 5e84.3
```
Para el alineamiento de multiple estructuras puede utilizar el comando:
```
extra_fit all
```
![](img8_tp7) Ahora identificaremos todos aquellos residuos importantes en estabilizar el cofactor en el interior de la proteína. Aquellos residuos localizados a 5 o 10 Aº cumplen un rol importante en este sentido.

Localizado el cofactor lo seleccionamos y lo nombramos como selección. Para eso debemos clickear en el átomo, luego en Action à rename selection le damos el nombre "cofactor".

Ahora desde la consola seleccionamos todos los atomos que están a menos de 5 y 10 Aº.
```
select br. all within 5 of cofactor
```
Renombramos la nueva selección en **A** ction à rename selection. Resi\_in5A y Resi\_in10A según corresponda.

Deseleccione el átomo cofactor y visualice con **S** how los residuos más cercanos como sticks. También puede cambiarles de color para visualizarlos mejor.

> 2. ¿Cuáles son los amino ácido que se encuentran a menos de 5 Aº?? ¿Y a menos de 10 Aº?
> 3. ¿De qué estructura forman parte dichos amino ácidos?

Mediremos la distancia entre el anillo de prolina y el cofactor:

```
get_distance /model_01//_/ZN`4/ZN, /model_01//A/PRO`174/CG
```
Para visualizar y calcular la distancia al anillo ir a Wizard à Measurement a Distances  Distance to rings y seleccionar las moléculas cuya distancia se desea medir.

![](img9_tp7)

Ahora observaremos la estructura tridimensional y superficie de la proteína.

Para ello antes duplicaremos el modelo, para no perder la visualización de la estructura secundaria de la misma. Para eso en model1 vamos a **Action**  **a**  **copy to object**  **a**  **New** y asignamos un nuevo nombre al objeto: " **model1\_sup**": **A**ction a rename an **object**

Luego en el nuevo objecto seleccione **S** how as\_surface

Puede otorgar transparencia a la superficie de la proteína en settings de manera que le permitirá observar la estructura secunda dentro de la superficie:

![](img10_tp7)

Desde la consola puede colorear la superficie según los residuos polares y no polares:
```
from pymol import cmd
```
````
cmd.select ('nonpolar','resn met or resn phe or resn pro or resn trp or resn val or resn leu or resn ile or resn ala')
```

```
cmd.select ('polar','resn ser or resn thr or resn asn or resn gln or resn tyr')
```
En color de la nueva selección otorgue dos colores que permitan discernir las distintas regiones según su polaridad:

Por ejemplo:

![](img11_tp7)

> 4. ¿Qué observa en la superficie de la proteína?

Puede guardar la sesión en File a Save Session as


<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___
