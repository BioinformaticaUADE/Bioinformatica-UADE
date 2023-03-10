# TP 1: Introduccion a Linux e interprete BASH

## Comandos en Linux y Secuencias

Primero algunas aclaraciones sobre cómo vamos a trabajar en los TPs!!!!!!!

Contestar las preguntas con las respuestas concretas obtenidas de la "terminal" más alguna oracion en tus palabras.

_\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*_

_Hacer "capturas de pantalla" y copiar comandos utilizados en un Documento de Texto así será más fácil cuando tengan que entregar TP final al finalizar cursada._

_(ver comando 'history' en terminal)_

_\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*_

**Hoy (y resto de materia) utilizaremos la máquina virtual**

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/VM.jpg)

**Usuario: bioinformatica**

**password: bioinformatica**

En esta máquina virtual están instalado el sistema operativo Lubuntu que es el entorno que se utilizará en la materia para realizar todos los TPs. Los alumnos irán instalando los programas necesarios para cada TP y descargando los archivos con el fin que se familiaricen con el entorno, la línea de comandos y el modo de trabajar en bioinformática en un entorno Linux. Los archivos necesarios para los TPs se podrán descargar desde la carpeta Bioinformática\_UADE\_2020 compartida en OneDrive o desde sus repositorios originales.

Nota: Un **repositorio** es un espacio centralizado donde se almacena, organiza, mantiene y difunde información digital, habitualmente archivos informáticos, que pueden contener trabajos científicos, conjuntos de datos o software

Ahora sí, una vez adentro de la máquina virtual verán un entorno gráfico de Lubuntu similar al de cualquier sistema operativo. El en los TP susaremos una interfaz [Unix](https://en.wikipedia.org/wiki/Unix) para interactuar con el mismo, esta interfaz es un intérprete de comandos de texto, llamada BASH ([Bourne Again Shell](https://en.wikipedia.org/wiki/Bash_(Unix_shell)))_._

En otras palabras, una terminal BASH es una interfaz que espera comandos de texto a ser escritos por el usuario mediante el teclado, cuando se ejecutan los comandos escritos estos son enviados a la computadora en lenguaje binario, que es el lenguaje que la computadora comprende, es por eso que a la terminal también se la conoce como intérprete de comandos. Nosotros escribimos dentro de la terminal en lenguaje Bash y el intérprete traduce nuestros comandos y se los envía a la computadora para ser ejecutados. Dentro de la terminal el mouse no se utiliza para ejecutar comandos o programas, solo sirve, por ejemplo, para seleccionar texto, copiarlo y pegarlo o para mover la barra lateral para subir y bajar la página en la que estamos. Sin embargo, para navegar el sistema de archivos, abrir carpetas y ejecutar programas los comandos deben ser escritos de manera literal en el intérprete. Cada vez que escribimos un comando, lo ejecutamos presionando la tecla Enter⏎. Hay otros lenguajes además de Bash, cada uno con su objetivo puntual, con sus pros y cons, por ejemplo: python, perl, java y R. Pero para la mayoría de las tareas usaremos Bash.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/bash.png)

Bash contiene decenas de comandos que pueden escribirse para ejecutarse en la terminal y junto con algunas convenciones de semántica y sintaxis componen un robusto lenguaje de programación enfocado al [_scripting_](https://en.wikipedia.org/wiki/Scripting_language) con él cual pueden implementarse complejos algoritmos. En este tutorial solamente veremos algunos [comandos populares](https://linuxconfig.org/linux-commands-cheat-sheet), e iremos aprendiendo y utilizando más comandos a medida que avanzamos en la materia.

| **Comando** | **Acción** | **Comando** | **Acción** |
| --- | --- | --- | --- |
|  **ls**  | Listar contenidos | **head**  | Ver 10 primeras líneas |
|  **cd**  | Change directorio | **tail**  | Ver 10 últimas líneas |
|  **mkdir**  | Make directorio | **nano ó vim**  | editores de texto |
|  **pwd**  | Path to Working Directory |  **cp**  | Copiar |
|  **cat**  | Concatenate & show | **mv**  | Mover o renombrar |
|  **more**  | Muestra página por página | **|** | Un pipe, para pipelines |
|  **grep**  | Buscar strings en textos |  **wc**  | Word Count |
|  **wget**  | Descarga de la web | **gunzip**  | Descomprime archivos.gz |


Entrar a la terminal y ejecutar el comando:
```
tree -d -L 1
```
Este comando nos permite ver la organización de los directorios

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/tree.jpg)

Todos los TPs los realizaremos en "/home/bioinformatica/Documentos"

Descargaremos desde OneDrive el archivo docs\_Bioinformatica.tar.gz en caso de que no lo tengan y lo guardaremos en la carpeta "Documentos"

Y vamos a descomprimir el archivo haciendo:
```
tar -xzvf docs_Bioinformatica.tar.gz
```
Veremos entonces en el directorio:

**/home/bioinformatica/Documentos/docs\_Bioinformatica**

encontrarán todos los archivos necesarios.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/documentos_data.jpg)

## Parte 1: Trabajamos con archivos de texto en la línea de comandos

Lo primero que vamos hacer _verificar donde estamos_ y _proteger_ los archivos de posibles accidentes en que los borremos!!! :(

Ejecuten este comando con cuidado y atención (ingresar contraseña "bioinformatica" ):
```
sudo chown root:root /home/bioinformatica/Documentos/docs_Bioinformatica/*
```
Vean un manual/tutorial de "chown" en: [http://www.computerhope.com/unix/uchown.htm](http://www.computerhope.com/unix/uchown.htm)

Con este comando hacemos que el usuario _"root"_ sea dueño de estos archivos, igual van a poder copiarlos a otro directorio, pero si intentan borrarlos no lo van a tener permitido.

Si quieren ver como son los permisos de esos archivos, ejecutar:
```
ls -l
```
Ahora si empezamos con el TP1, para eso crearemos la carpeta TP1 en el directorio Documentos. Hoy vamos a trabajar con el archivo _"protein.fa.gz"_, primero _copien_ el archivo _protein.fa.gz_ desde /home/bioinformatica/Documentos/docs\_Bioinformatica a su directorio "_/home/bioinformatica/Documentos/docs\_Bioinformatica/TP1_"

Cuidado, utilicen bien la sintaxis y ruta completa de archivo, para copiar ejecuten:

#Crear directorio TP1 en Documentos#
```
mkdir /home/bioinformatica/Documentos/TP1
```
#copiar el archivo
```
cp /home/bioinformatica/Documentos/docs_Bioinformatica/protein.fa.gz /home/bioinformatica/Documentos/TP1
```
Descomprimimos el archivo y luego, vamos a renombrar el archivo _"protein.fa"_ que copiamos recién, con el nuevo nombre: _"human\_proteome.faa"_ , para renombrar usamos el comando **"mv" (el mismo que para mover archivos):**

**Syntaxis:**

mv \<archivo a renombrar\> \<nombre nuevo\>

**Ver ayuda en:** [**http://www.computerhope.com/unix/umv.htm**](http://www.computerhope.com/unix/umv.htm)

**Para renombrar:**
```
mv protein.fa human_proteome.faa
```
Para ver los archivos que tenemos en el directorio y confirmar que renombraron correctamente el archivo, pueden usar el comando **"ls"** :
```
ls
```
> 1. **¿Cuántas líneas tiene el archivo?**

El comando " **wc**" (wc = word count) muestra las líneas, palabras y caracteres del archivo especificado. Si usamos la opción **"-l"** obtenemos solo la cantidad de líneas.
```
wc human_proteome.faa
```
> 2. **¿Cuántas proteínas hay en el archivo?**

Para esta operación se puede usar el comando **"grep":**

El comando grep selecciona y muestra en la pantalla, las líneas de los archivos que coincidan con la cadena o patrón que nos interese buscar.

Para ver ayuda y ejemplos en URL: [http://www.computerhope.com/unix/ugrep.htm](http://www.computerhope.com/unix/ugrep.htm)

**Sintaxis**

grep [opciones] patrón \<nombre archivo\>

**Entonces, para contar las secuencias ejecutamos:**
```
grep -c ">" human_proteome.faa
```
o
```
grep -c '^>' human_proteome.faa
```
Donde "-c" es la opción del comando " **grep"** que muestra la cantidad de líneas coincidentes y "^" indica: **"Empieza con".** De esta manera el comando busca una expresión regular o patrón (_regular expression_) que en este caso indica que estamos buscando "\>" al principio de la línea solamente.

> 3. **¿Por qué contamos cuántos caracteres "\>" hay en el archivo para saber la cantidad de proteínas?**

> 4. **¿Cuántas ATP-binding proteins hay en el archivo? ¿Cómo realiza esto? ¿Que hace "grep"?**

Podemos usar **"grep"** nuevamente, ejecutamos:
```
grep "ATP-binding" human_proteome.faa
```
Para contarlas:
```
grep -c "ATP-binding" human_proteome.faa
```
> 5. **¿Como hariamos para que lo que se ve por pantalla sea escrito a un nuevo archivo?**

**Ver ayuda en URL:** [**http://linuxcommand.org/lc3\_lts0070.php**](http://linuxcommand.org/lc3_lts0070.php)

Para enviar todos los encabezados de las proteínas que contienen _"ATP-binding"_ a un nuevo archivo que se llame _"atp\_binding.headers"_ ejecutamos:
```
grep "ATP-binding" human_proteome.faa > atp_binding.headers
```
Nota: El carácter **"\>"** indica el archivo de salida donde se redirige el resultado de la operación ejecutada por el comando_ **"grep"** _

> 6. **¿Cómo hacemos para que la salida de pantalla pase a ser la entrada a un nuevo comando?**

El _**"|" (pipe)**_ toma la salida del comando ejecutado a su izquierda y la direcciona como entrada del comando a su derecha (concatenación de comandos).

Para obtener sólo los "gi" de cada proteína que contiene _"ATP-binding"_ y mandarlos a un nuevo archivo que se llame _"atp\_binding.gis"_ ejecutamos:
```
grep "ATP-binding" human_proteome.faa | cut -f 2 -d "|" > atp_binding.gis
```
Para ver las 10 primeras líneas del archivo de salida ejecutamos:
```
head atp_binding.gis
```
## Parte 2: Instalación de programas en Linux y manipulación de "Enviroments" para bioinformática.

Un repositorio básicamente es un servidor que aloja los programas específicos para uno o varios Sistemas Operativos Linux, y por lo general están construidos para que se puedan acceder vía gestor de paquetes de consola (terminal) o gráfico, aunque en otros casos incluye el acceso vía Navegador Web. Usar Repositorios para nuestros Linux nos da como ventaja que los programas que se encuentran en estos repositorios están verificados por la Comunidad de Software Libre y de las respectivas Distribuciones que los crea y respalda, por lo que se garantiza un mínimo de problemas para usarlos.

Para instalar programas en Linux necesitamos tener acceso de administrador o root, que significa que tenemos permisos para hacer lo que queramos. Pero por protección Linux funciona bajo en acceso por contraseña. Por eso siempre que queramos instalar un programa desde los repositorios Linux lo realizaremos escribiendo:
```
sudo apt install "nombre del programa"
```
Por ejemplo, si escribimos:
```
sudo apt install ncbi-
```
y apretamos la tecla tab, el sistema nos ofrece los nombres de los programas que empiezan con la palabra ncbi. ¿Cuántas opciones aparecen?

La instalación de programas requiere la carga previa de los repositorios, pre-programas o requerimientos, librerías, módulos que se realiza instalando diferentes paquetes de software y mediante continuos _"updates" y "upgrades"_.

Como cada sistema operativo posee distintos repositorios y como cada programa necesita diferentes módulos, versiones de módulos y softwares se crearon los llamados "Enviroments".

Los Enviroments son entornos virtuales que ayudan a mantener separadas las dependencias requeridas por diferentes proyectos al crear espacios aislados que contienen dependencias específicas para cada proyecto o tarea o grupo de programas.

Los usuarios pueden crear entornos virtuales utilizando una de varias herramientas como Pipenv o Poetry, Docker o un **entorno virtual conda**. Pipenv y Poetry se basan en la biblioteca venv incorporada de Python, mientras que conda tiene su propia noción de entornos virtuales de nivel inferior (Python en sí es una dependencia proporcionada en entornos conda). En este TP instalaremos el enviroment conda (Anaconda) que nos permitirá instalar y administrar todas las herramientas que usaremos en bioinformática durante la materia ([https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)).

**NOTA:** La instalación de Anaconda y los _enviroments_ ya fueron previamente instalados por lo que no deben ser ejecutados en esta instancia.

Para instalar el Enviroment Anaconda ud. Ud. encontrará el archivo **Anaconda3-XXXXX-Linux-x86\_64.sh** en [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual).

Para instalarlo desde una terminal localizamos el archivo y ejecutamos lo siguiente:
```
sh Anaconda3-2020.07-Linux-x86_64.sh
```
![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/conda1.jpg)

Presionar Enter hasta que aparezca:

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/conda2.jpg)

Tipear yes y dar Enter

Y Luego nuevamente Enter y comenzará la instalación de Anaconda.

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/conda3.jpg)

Finalmente:

![](https://github.com/BioinformaticaUADE/Bioinformatica-UADE/blob/main/img/conda4.jpg)

Ahora cada vez que inicie una terminal observará la palabra "base" al principio de la línea.

Esto significa que el entorno base de anaconda esta funcionando en su terminal.

Ahora crearemos un enviroment llamado **analisis\_de\_secuencias** e instalaremos herramientas que nos serán de utilidad.

Para ello primero configuraremos los canales de anaconda donde se buscarán los paquetes:
```
conda config --add channels defaults

conda config --add channels bioconda

conda config --add channels conda-forge
```
Para generar el enviroment ejecutaremos lo siguiente:
```
conda create -n analisis_de_secuencias blast ncbi-vdb entrez-direct diamond sra-tools emboss exonerate python perl
```
Este paso puede demorar unos minutos. Luego seleccionamos Y (yes) y comenzará la instalación.

**NOTA:** Ahora continuamos desde aquí.

**Para observar los enviroments instalados ejecutar:**
```
conda info –envs
```
> 7. **¿Que enviroments encuentra instalados?**

Para activar el enviroment analisis\_de\_secuencias ejecutamos:
```
conda activate analisis_de_secuencias
```
Con el enviroment activado instalaremosinstalaremos el set de herramientas "fastx\_toolkit".
```
conda install fastx_toolkit
```
## Parte 3: Búsqueda de Patrones

Para encontrar si alguna de las proteínas del archivo _human\_proteome.faa_ contienen el patrón de aminoácidos **"LLXND"** , (el patrón se describe como: LL seguido por cualquier aminoácido (X) y luego ND) podemos utilizar:
```
grep "LL.ND" human_proteome.faa
```
Nota: El carácter "." Significa wildcard: puede ser cualquier carácter

> 8. **¿Cuántas secuencias tienen ese patrón?**

> 9. **El comando "** _ **grep"** _ **contesta la pregunta de cuantas secuencias tienen ese patrón? ¿o no? ¿De qué depende? (Como interpreta el resultado)**
```
fasta_formatter -i human_proteome.faa -w 0 > mod_human_proteome.faa
```
¿Qué cambios se generaron en el archive? ¿Puede ahora usar el comando grep para contestar la pregunta anterior?

> 10. **Ahora ejecutamos la búsqueda usando el comando** _ **"fuzzpro"** _ **de emboss**

El comando _ **"fuzzpro"** _ pertenece al paquete emboss (ya instalado) y sirve para buscar patrones en secuencias de aminoácidos

Ver ayuda en: [http://emboss.sourceforge.net/apps/release/6.6/emboss/apps/fuzzpro.html](http://emboss.sourceforge.net/apps/release/6.6/emboss/apps/fuzzpro.html)

**Para ver ayuda en la línea de comandos ejecuten:**  **fuzzpro -h**

**Sintaxis:**
```
fuzzpro -sequence <nombre archivo entrada> -pattern <patrón> -outfile <archivo de salida>
```
Para realizar la búsqueda con el comando _fuzzpro_ y generar un archivo de salida llamado _"llxnd\_human\_proteome.fuzzpro"_ ejecutamos:
```
fuzzpro -sequence human_proteome.faa -pattern LLxND -outfile llxnd_human_proteome.fuzzpro
```
Ojo: en el comando fuzzpro, el caracter "x" es usado como wildcard.

> 11. **¿Son iguales los resultados obtenidos por ambos comandos (**_ **grep** _ **y** _ **fuzzpro** _**)? ¿Por qué? ¿Por qué cree que importante la búsqueda de patrones?**

Nota: Para ver el resultado general de _fuzzpro_ (cantidad de secuencias con el patrón, cantidad de veces que aparece el patrón, etc), tienen que ver al final del archivo de salida, para eso pueden usar el comando _ **"tail"** _

**Sintaxis:**
```
tail llxnd_human_proteome.fuzzpro
```
> 12. **¿Cómo podemos editar los archivos creados?**

Para editar cualquiera de los archivos podemos usar el comando_ **"nano"** _(para salir Ctrl+x) o _"__ **vim"** _.
```
nano llxnd_human_proteome.fuzzpro
```
> 13. **¿Cómo podemos ordenar la lista de gi numbers obtenida anteriormente?**

Usando el comando_ **"sort"** _, probar que ocurre si usamos las opciones_ **"-n"** _ y/o_ **"-r"** _:
```
sort atp_binding.gis
```
## Parte 4: Búsqueda y descarga de archivos desde Bases de datos. Extracción de información de las secuencias.

Sabemos que en estos momentos un virus coronavirus esta causando una pandemia mundial. Muchos laboratorios han obtenido el genoma del virus y ahora está disponible en bases de datos. Sabemos que el identificador del virus es NC\_045512.

Para descargar la secuencia usaremos la herramienta **efetch** de Entrez:
```
efetch -db nucleotide -id NC_045512 -format fasta > coronavirus.fasta
```
Observar el archivo generado con les y determinar cuántas secuencias hay. ¿Cual es el tamaño del genoma viral?

Ayuda: **infoseq** o **fastalength** pueden brindarle esa información.

> 14. **¿Qué información puede extraer?**

Ahora vamos a descargar los CDS, es decir los transcriptos que dan lugar a las proteínas.
```
efetch -db nucleotide -id MT066156 -format fasta_cds_na > coronavirus_CDS.fasta
```
ejecutar:
```
efetch -help
```
> 15. **¿Según esta información que debería cambiar en el comando para obtener las proteínas?**

Ejecute el comando que cree que funcionará y guarde la secuencia en el archivo coronavirus\_aa.fasta.
```
efetch -db nucleotide -id MT066156 -format fasta_cds_aa > coronavirus_aa.fasta
```
> 16. **¿Cuál es la proteína más larga? ¿Y cuál es la más corta?**

**Nota** : puede ayudarse con un comando usado en ejercicios anteriores

**Ejecute el comando:**
```
fastacomposition -f coronavirus_aa.fasta -s > composition.txt
```
> 17. **Qué información le brinda?**   
<br />
<br />

___
   ###### *Dr. Lucas L. Maldonado*
   ###### *Bioinformática, Licenciatura en Biotecnología, Universidad Argentina de la Empresa, 2023*
___

