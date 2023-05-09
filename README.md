# NGS-en-oncologia-Curso-Uchile-2023

##  TALLER: Análisis e interpretación de variantes con valor predictivo en oncología. 

A cada grupo se le asignará un VCF con 10 variantes, las cuales, deberán ser anotadas con las  herramientas vistas en el curso, éstas nos permitirán conocer el impacto funcional de cada una.
El objetivo es identificar aquellas mutaciones somáticas accionables que podrían tener un impacto en el tratamiento del paciente. A continuación describiremos los pasos a seguir utilizando un VCF de prueba [Taller\_Sample\_161.vcf](https://github.com/Lab-Genomica-Funcional-Cancer/NGS-en-oncologia-Curso-Uchile-2023/blob/main/VCFs/Taller_Sample_161.vcf). 

## Búsqueda de polimorfismos ##

En los análisis de tumores comúnmente se secuencia una muestra de tejido sano del mismo individuo, para distinguir las mutaciones de la línea germinal de las mutaciones somáticas. Comúnmente debido al costo o a la disponibilidad de muestras, en algunos centros solo la muestra tumoral es secuenciada y para filtrar las mutaciones de la línea germinal se utilizan las bases de datos de variación genética poblacional (Ej: 1000 Genomas, gnomAD, ExAC) y/o un conjunto de genomas internos para filtrar las variantes. Para realizar este objetivo, utilizaremos la herramienta VEP que permite agregar la anotación 1000 Genomas y gnomAD.

### VEP (Ensembl Variant Effect Predictor) ###

VEP es una herramienta que permite anotar los efectos funcionales de las variantes genéticas en las proteínas y los transcritos del genoma humano. Al ingresar los datos en VEP, los usuarios pueden obtener información sobre los efectos de las variantes, incluyendo información sobre la ubicación en el genoma de referencia, la función y la frecuencia en poblaciones.

* [VEP - referencia hg19 (utilizar este link)](https://grch37.ensembl.org/Homo_sapiens/Tools/VEP?db=core)
* [VEP - referencia hg38](https://www.ensembl.org/Multi/Tools/VEP?db=core)

**PASO 1**: Cargar el archivo VCF en la página web. **OJO**: Utilizar *VEP assembly GRCh37.*

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.52.13.png?raw=true)

**PASO 2**: Agregar los identificadores marcados de la lista (CCDS, Protein, UniProt y HGVS). Para ver la descripción situar el mouse sobre el identificador.

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.52.51.png?raw=true)

**PASO 3**: Seleccionar las bases de datos de 1000 Genomas y gnomAD, esta anotación nos permitirá saber la frecuencia de las variantes en diferentes poblaciones. Aquellas variaciones genéticas que se encuentran en más de un 1% de la población son consideradas polimorfismos. De esta manera las descartamos como mutaciones somáticas.

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.53.17.png?raw=true)

**PASO 4**: A los parámetros ya seleccionados, agregamos la identificación del transcrito canónico. 
Finalmente, hacemos click en el botón verde (RUN) para comenzar la anotación con VEP.

![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2019.59.10.png?raw=true)

**PASO 5**: Ejecutamos el análisis para obtener la información funcional de cada variante. Descargamos los datos en TXT e importamos la tabla en un archivo Excel para su revisión y filtrado. 
En el Excel seleccionamos *CANONICAL: YES*. Aquellas variantes con frecuencia >= 0.01 en algunas de estas columnas: `AF, AFR\_AF, AMR\_AF, EAS\_AF, EUR\_AF, SAS\_AF, gnomADe\_XX`, serán consideradas polimorfismos. 
Finalmente, para el paso posterior rescatamos las columnas; *HGVSc*, *SYMBOL* (nombre del gen) y *Amino_acids* (cambio a nivel de aminoácido) para rellenar la plantilla de reporte clínico. *Para detalles sobre qué representa cada columna del archivo de salida de VEP, revise este link: [Default VEP output](https://www.ensembl.org/info/docs/tools/vep/vep_formats.html#defaultout)*
	
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2022.12.40.png?raw=true)

**PASO 6**: La información funcional rescatada de VEP y las variantes clasificadas como polimorfismos deben ser agregadas al reporte clínico. Descargar el archivo *Plantilla_reporte_RGO.docx*, del repositorio. Ejemplo: 
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2000.50.33.png?raw=true)

## Anotación de variantes somáticas ##

Una vez que descartamos los polimorfismos (variación de la línea germinal), es necesario identificar aquellas variantes somáticas que podrían ser pasajeras, conductoras y/o accionables. Para este propósito utilizaremos las herramientas: Cancer Genome Interpreter (CGI), COSMIC y OncoKB.

### Cancer Genome Interpreter ###

Cancer Genome Interpreter (CGI) está diseñado para la identificación de las alteraciones potencialmente oncogénicas y/o que pueden ser terapéuticamente relevantes. CGI utiliza el conocimiento recopilado de dominio público para anotar las alteraciones de un tumor de acuerdo con varios niveles de evidencia. Además, utiliza métodos computacionales basados en aprendizaje automático para la predicción de mutaciones *driver* o también llamadas conductoras.

Para más información visite el siguiente [link](https://www.cancergenomeinterpreter.org/faq)

**PASO 7**: Ingresar a [CGI] (https://www.cancergenomeinterpreter.org/home). En *Add file+*, cargar el archivo VCF, seleccionar el tipo tumoral (SOLID), el genoma de referencia de nuestros datos (hg19) y finalmente ejecutar el análisis.
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-07%20a%20la(s)%2022.28.05.png?raw=true)

**PASO 8**: Se desplegarán dos pestañas con resultados, la primera: *ALTERATIONS* se observa la anotación de las variantes y se destacan aquellas mutaciones que son predichas (algoritmos OncodriveMut y boostDM) o conocidas como *drivers*. En este caso, las mutaciones en *NF1* y *ARID1A* son posiblemente conductoras, y la mutación en BRCA2, además tiene indicación terapéutica en oncoKB (circulo azul que se observa en la columna *Oncogenic annotation*). Toda esta información la podemos ir agregando al reporte clínico.
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2001.31.27.png?raw=true)

**PASO 9**: En la pestaña *PRESCRIPTIONS*, se observan los biomarcadores genómicos de respuesta a fármacos con diferentes niveles de relevancia clínica.
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2012.33.25.png?raw=true)

 Los resultados pueden ser descargados en *Downlaod results*.
 
### COSMIC ###

COSMIC (Catalogue Of Somatic Mutations In Cancer) es una base de datos en línea que recopila información sobre mutaciones somáticas en el cáncer. La base de datos COSMIC contiene información sobre más de 11 millones de mutaciones somáticas identificadas en más de 38,000 tumores de pacientes humanos. 
Las consultas a esta base de datos se puede realizar vía web [(link de acceso)](https://cancer.sanger.ac.uk/cosmic) utilizando diferentes tipos de entrada, por ejemplo:

* Nombre del gen (por ejemplo, BRAF o B-raf)
* Tejido o tipo de cáncer como 'pulmón' o 'colon'
* Descripción de la mutación, por ejemplo, la mutación KRAS "c.35G>A" (sintaxis de CDS) o "p.G12D" (sintaxis de aminoácidos)
* Descripción combinada de genes y mutaciones, por ejemplo, "KRAS p.G12D"
* Genomic mutation identifiers (COSV) 

Para realizar la búsqueda utilizaremos la información de la columna **Existing_variation** de la anotación obtenida en VEP (tabla que importamos en Excel, PASO 5), donde encontraremos en algunos casos el código COSV de la mutación. En caso de no tener ID COSV buscar utilizando la sintaxis de CDS o de aminoácidos. 

**PASO 10**: Agregamos la presencia o ausencia de la mutación en COSMIC al reporte clínico.

### OncoKB ###

Finalmente, utilizaremos oncoKB para búsqueda de mutaciones somáticas con indicación terapéutica.
OncoKB es una base de conocimiento que proporciona información sobre la importancia clínica de las alteraciones genómicas en el cáncer. Esta plataforma ofrece datos curados sobre los efectos biológicos y clínicos de estas alteraciones, así como sus asociaciones con tipos de cáncer específicos y fármacos. OncoKB es una herramienta valiosa para los clínicos, investigadores y pacientes que buscan tomar decisiones informadas sobre el diagnóstico, tratamiento y manejo del cáncer basados en datos genómicos.

Como ejercicio podemos realizar la búsqueda manual de cada mutación en OncoKB utilizando la descripción combinada de genes y mutaciones, por ejemplo, "*KRAS* p.G12D". Sin embargo, como observamos en el **PASO 8** , CGI nos indica cuando una mutación se encuentra presente en OncoKB y nos entrega directamente el link de acceso.
[Link de OncoKB](https://www.oncokb.org/)

## Reporte

El resumen de la información recolectada la agregamos al reporte clínico:
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2015.41.25.png?raw=true)

Finalmente en la sección **INDICACIÓN TERAPÉUTICA** del reporte clínico, podemos agregar información detallada de las mutaciones encontradas en OncoKB (accionables), en este caso, la mutación en *BRCA2* p.R2659K.
![](https://github.com/evelingonzalezfeliu/Tutorial-Ensamble-de-transcriptomas./blob/master/Captura%20de%20Pantalla%202023-05-08%20a%20la(s)%2015.16.41.png?raw=true)

[](https://www.oncokb.org/gene/BRCA2/R2659K)



