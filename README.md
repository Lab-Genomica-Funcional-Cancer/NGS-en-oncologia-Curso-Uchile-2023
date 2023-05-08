# NGS-en-oncologia-Curso-Uchile-2023

##  TALLER: Análisis e interpretación de variantes con valor predictivo en oncología. 

Cada grupo se le asignará un VCF con 10 variantes, las cuales, deberan ser anotadas con las  herramientas vistas en clases, que nos permitiran conocer el impacto funcional de cada una.
El obetivo es identificar aquellas variantes somaticas accionables que podrian tener un impacto en el tratamiento del paciente. A continuación describiremos los pasos a seguir utilizando un VCF de prueba [Taller\_Sample\_161.vcf](https://github.com/Lab-Genomica-Funcional-Cancer/NGS-en-oncologia-Curso-Uchile-2023/blob/main/VCFs/Taller_Sample_161.vcf). 

## Búsqueda de polimorfirmos ##

Los análisis de tumores comúnmente emplean una corrección con un normal emparejado (MN), una muestra de tejido sano del mismo individuo, para distinguir las mutaciones de la línea germinal de las mutaciones somáticas. Dado que se cree que la mayoría de las variantes encontradas en un individuo son comunes dentro de la población,

Por lo tanto, cada vez que no se disponía de una muestra normal compatible (MN) (más comúnmente debido a la falta de fondos o disponibilidad de muestras), los investigadores generalmente confiaban en las bases de datos de mutaciones públicas y/o en un conjunto de genomas internos para filtrar las variantes de la línea germinal.

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4561496/#:~:text=Tumor%20analyses%20commonly%20employ%20a,germline%20mutations%20from%20somatic%20mutations.

### VEP (Ensembl Variant Effect Predictor) ###

El VEP es una herramienta que predice los efectos funcionales de las variantes genéticas en las proteínas y los transcriptos del genoma humano. Al ingresar los datos en VEP, los usuarios pueden obtener información sobre los efectos de las variantes, incluyendo información sobre la ubicación en el genoma de referencia, la función y la frecuencia de las variantes en poblaciones.

* VEP - referencia hg19 (utilizar este link)
[https://grch37.ensembl.org/Homo_sapiens/Tools/VEP?db=core](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.59.10.png?raw=true)
* VEP - referencia hg38
[https://www.ensembl.org/Multi/Tools/VEP?db=core](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.59.10.png?raw=true)

**PASO 1**: Cargar el archivo VCF en la página web. OJO: Utilizar VEP assembly GRCh37

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.52.13.png?raw=true)

**PASO 2**: Agregar los identificadores de la lista. Para ver la descripcion de cada uno, situar el mouse sbre el identificador.

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.52.51.png?raw=true)

**PASO 3**: Selecionar las bases de datos de 1000 Genomas y gnomAD que se encuentran en la lista, esta anotación nos permitirá saber la frecuencia de las variantes en poblaciones. Aquellas varianciones genéticas que se encuentran en mas de un 1% de la población son polimorfismos.

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.53.17.png?raw=true)

**PASO 4**: A los parámetros ya selecionados, agregamos la identifcación del transcrito canónico. 

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.59.10.png?raw=true)

**PASO 5**: Ejecutamos el análsis y obtenerdremos informacion funcional de cada variante. Esta puede ser descargada en TXT e importamos la tabla en un archivo Excel para su revisión. 
CANONICAL 
AF, AFR\_AF, AMR\_AF,	EAS\_AF, EUR\_AF, SAS\_AF, gnomADe\_XX
Utilizamos la columnas HGVSc (anotacion ) SYMBOL (nombre del ggen)  y Amino_acids (cambio a nivel de aminoácido) para rellenar la plantilla de reporte clínico.	
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2022.12.40.png?raw=true)

**PASO 6**: Aquellas variantes con frecuencia sobre 0.01 en las columnas de 1000 Genomas o gnomAD son clasificadas como polimorfirmos, esta informacion debe ser agregada al reporte clínico.
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2000.50.33.png?raw=true)

## Anotación de variantes somáticas ##

Una ves que descartamos los polimorismos, es necesario identificar aquqllas variantes somaticas que son pasajeras, conductoras o accionables. Para este propósito utilizaremos las herramientas: Cancer Genome Interpreter (CGI), COSMIC y OncoKB.

### Cancer Genome Interpreter ###

Cancer Genome Interpreter (CGI) está diseñado para la identificación de las alteraciones potencialmente oncogénicas y/o que pueden ser terapéuticamente relevantes. CGI utiliza el conocimiento recopilado de dominio público para anotar las alteraciones de un tumor de acuerdo con varios niveles de evidencia. Ademas, utiliza métodos computacionales basados en aprendizaje automático para la prediccion de mutaciones *driver* o conductoras.

* Para más información visite el siguiente [Link](https://www.cancergenomeinterpreter.org/faq)

**PASO 7**: Ingresar a CGI con el siguiente [Link](https://www.cancergenomeinterpreter.org/home). En *Add file +*, cargar el archivo VCF, seleccionar el tipo tumoral (SOLID), el genoma de referencia de nuestros datos (hg19) y finalmente ejecutar el análisis.
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2022.28.05.png?raw=true)

**PASO 8**: Se desplegaran dos pestañas con resultados, la primera: *ALTERATIONS* se observa la anotacion de las variantes y se destacan aquellas mutaciones que son predichas (algoritmos OncodriveMut y boostDM) o conocidas como  *drivers*. En caso, las mutaciones en NF1 y ARID1A son posiblemente conductoras, y la mutacion en BRCA2 tiene anotacion en oncoKB, debido al circulo azul que se observa en la columna "*Oncogenic annotation*"
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2001.31.27.png?raw=true)

**PASO 9**: Pestaña *PRESCRIPTIONS*
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2012.33.25.png?raw=true)

 Los resulatdos pueden ser descargados en *Downlaod results*.
 
### COSMIC ###

COSMIC (Catalogue Of Somatic Mutations In Cancer) es una base de datos en línea que recopila información sobre mutaciones somáticas en el cáncer.  es ampliamente utilizada por investigadores y médicos en todo el mundo para comprender la genética del cáncer y desarrollar tratamientos personalizados. La base de datos COSMIC contiene información sobre más de 11 millones de mutaciones somáticas identificadas en más de 38,000 tumores de pacientes humanos.

https://cancer.sanger.ac.uk/cosmic

### OncoKB ###

## Reporte

El resumen de la informacion recolectada la agregamos al reporte clinico:
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2015.41.25.png?raw=true)

Finalmente en la sección **INDICACIÓN TERAPÉUTICA** del reporte clínico, podemos agregar información detallada de onocKB la mutacione acionable en BRCA2 p.R2659K.

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2015.16.41.png?raw=true)


[](https://www.oncokb.org/gene/BRCA2/R2659K)



