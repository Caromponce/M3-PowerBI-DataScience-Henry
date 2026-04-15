##INTRODUCCIÓN

El siguiente es el Proyecto Integrador del Módulo III: Business Intelligence y visualización, de la carrera de Data Science de Henry, cohorte DSPT01.

##CONTEXTO DEL PROYECTO Y ROL DEL ESTUDIANTE

El presente proyecto integrador consta de un “proceso de selección para el rol de Analista de Datos Junior de DataVision Analytic”. Al candidato se le ha asignado 3 fases de desarrollado para TechCore, una cadena de tiendas de tecnología, que tiene como objetivo transformar una base de datos cruda de facturación en información útil para la toma de decisiones. Las 3 fases implican: limpieza y estandarización de datos, modelado relacional y creación de un dashboard interactivo en Power BI.
La primera fase del proyecto para TechCore consiste en importar, limpiar y preparar la base de datos cruda de facturación en Power BI, dejándola lista para los siguientes análisis y modelados.
Durante la segunda fase, se espera diseñar e implementar un modelo relacional que permitirá integrar la información de ventas con las demás entidades del negocio —productos, clientes, sucursales y vendedores— asegurando coherencia, integridad y trazabilidad de los datos.
Finalmente, DataVision Analytics encomienda al candidato la tercera y última fase del proyecto para TechCore. El propósito de este avance es importar el modelo relacional generado en Python dentro de Power BI y desarrollar un dashboard interactivo que permita transformar los datos en información estratégica para la toma de decisiones.
Como mejora adicional, se espera un esquema de seguridad a nivel de fila (RLS) para restringir el acceso a la información según el rol del usuario (Gerente Nacional, Regional).


##COMPOSICIÓN DEL PROYECTO

ProyectoM3_CarolinaPonce/
│
├── DataRaw/
│   └── ventas.csv                            # Dataset original sin procesar
│
├── Documentación/  
│   └── Conclusiones e insights estratégicos.pdf  
│   └── README.pdf 
│
├── requirements.txt                   
│
│
├── Avance_1_Limpieza_Transformacion.pbix     # Archivo Power BI - Avance 1
├── Avance_2_Modelo_Relacional.ipynb          # Notebook Jupyter - Avance 2
├── Avance_3_Dashboard_Interactivo.pbix       # Archivo Power BI - Avance 3
│
├── ventasTransformed.csv                     # Dataset transformado y limpio
├── modeloVentas.db                           # Base de datos SQLite
├── modeloVentas.xlsx                         # Exportación de tablas a Excel
└── diagrama_ER_ventas.png                    # Diagrama Entidad-Relación


##DESCRIPCIÓN GENERAL

Como parte del proceso de selección para el rol de Analista de Datos Junior en DataVision Analytics, se desarrolló un proyecto para la empresa TechCore, una cadena de tiendas minoristas dedicada a la venta y distribución de computadoras y accesorios tecnológicos. El objetivo general fue convertir una base de datos cruda de facturación en un conjunto de análisis visuales e indicadores estratégicos mediante el uso de Power BI y Python, atravesando tres etapas principales: limpieza y estandarización de datos, modelado relacional y desarrollo de un dashboard interactivo.
En la primera fase, se trabajó en la importación, limpieza y preparación de la base de datos original de facturas dentro de Power BI Desktop, utilizando Power Query como herramienta principal para el proceso de transformación. 
Se realizó una estandarización de los nombres de columnas, asegurando uniformidad y claridad (por ejemplo, renombrando Prod_Name a NombreProducto), y se verificó que cada campo contara con el tipo de dato adecuado: fechas en formato Date, precios en Decimal Number e identificadores en Text. Posteriormente, se llevó a cabo la detección y el tratamiento de valores nulos, duplicados e inconsistentes. Los registros de facturas exactamente iguales fueron eliminados, y los valores faltantes se reemplazaron de acuerdo con su naturaleza: los campos vacíos del método de pago fueron completados con “No especificado”, y los valores numéricos nulos se imputaron con cero cuando correspondía.
Finalmente, se normalizaron las categorías y los campos textuales para evitar variaciones que pudieran afectar los análisis posteriores. Este proceso permitió obtener una base limpia y estandarizada, lista para ser utilizada en las siguientes etapas del proyecto.
La segunda fase tuvo como propósito diseñar e implementar el modelo relacional que integrara la información de ventas con las demás entidades del negocio, tales como productos, clientes, ciudades, sucursales y vendedores. Para ello, se cargó en Python el dataset limpio exportado desde Power Query (ventasTransformed.csv) y se identificaron las principales entidades y sus relaciones. Se definieron las claves primarias y foráneas necesarias para construir las tablas del modelo: Facturas, DetalleFacturas, Productos, Clientes, Sucursales, Ciudades y Vendedores.
Cada tabla fue diseñada con los atributos adecuados para mantener la integridad referencial de los datos, garantizando que todo FacturaID presente en DetalleFacturas existiera también en Facturas, y que cada ProductoID o SucursalID correspondiera a un registro válido. El modelo se desarrolló utilizando librerías como pandas, SQLite3 y se generó una estructura lista para ser exportada a Power BI.
Además, se realizaron verificaciones de consistencia y control de calidad de los datos, comprobando que no existieran registros huérfanos ni valores incongruentes. Con el fin de validar la estructura del modelo, se elaboraron reportes exploratorios en Python, tales como el total de ventas por marca y el top 10 de productos más vendidos. Finalmente, el modelo completo fue representado mediante un diagrama entidad–relación (DER), donde se visualizaron las tablas creadas, sus claves y cardinalidades. Como resultado, se obtuvo el diagrama_ER_ventas.png, el archivo modeloVentas.xlsx, y el notebook Avance_2_Modelo_Relacional.ipynb, que documenta todo el proceso.
En la tercera y última fase, el objetivo fue desarrollar un dashboard interactivo en Power BI para transformar los datos del modelo relacional en información estratégica. Se importó el archivo modeloVentas.xlsx y se verificó la correcta detección de relaciones y jerarquías dentro del modelo de datos. A partir de allí, se construyeron diversas medidas DAX para calcular indicadores clave del negocio, entre ellos: Ventas Totales, Ticket Promedio, Participación por ciudad, Total Facturas Realizadas, Frecuencia de Compra, Variación % mes a mes. Estas métricas sirvieron como base para analizar el desempeño comercial de TechCore y facilitar comparaciones entre regiones, marcas y períodos de tiempo.
El dashboard se diseñó con un enfoque visual claro, con una portada y 6 secciones: KPIs globales, Ventas, Clientes, Productos, Vendedores y Sucursales, donde se puede navegar entre ellas a través de un navegador. Se incluyeron segmentaciones dinámicas que permiten filtrar la información por año, mes, sucursal según ciudad, producto, método de pago y en especial en la sección de clientes, se incluyó la segmentación por edad. También se establecieron jerarquías de navegación, como Ciudad  Sucursal, para facilitar un análisis más detallado. Entre las visualizaciones incorporadas se encuentran un mapa geográfico con el porcentaje de ventas por ciudad, un gráfico de barras con la cantidad de ventas por método de pago, una línea de tiempo con la evolución mensual de las ventas del año 2025 y tarjetas de KPIs que destacan los valores globales como ventas totales, ticket promedio y cantidad de productos vendidos.
Finalmente, se implementó un esquema de seguridad a nivel de fila (Row-Level Security, RLS) para restringir el acceso a la información según el rol del usuario. Se definieron 2 perfiles principales: Gerente Nacional (acceso total) y Gerente Regional uno por cada ciudad (acceso limitado a su ciudad). Para ello, se creó una tabla de usuarios con nombre, correo electrónico simulado y ubicación asociada, estableciendo las relaciones necesarias para aplicar filtros dinámicos en función del rol. Las reglas de RLS se configuraron mediante expresiones DAX, asegurando la correcta segmentación de la información.
El archivo final, denominado Avance_3_Dashboard_Interactivo.pbix, consolidó todas las medidas, jerarquías, filtros y visualizaciones, permitiendo a TechCore disponer de una herramienta analítica integral para la toma de decisiones basada en datos.
 
 
##TECNOLOGÍAS UTILIZADAS

Herramientas
•	Power BI Desktop.
•	Python.
•	Jupyter Notebook.
•	SQLite.
•	Graphviz.

Lenguajes y librerías
•	Python 
•	Pandas.
•	SQLite3.
•	Graphviz.
•	Openpyxl.
•	M (Power Query).
•	DAX (Data Analysis Expressions).


##REQUISITOS PARA SU INSTALACIÓN Y CONFIGURACIÓN

Versión de Python recomendada: 3.13.5
Requisitos: requirements.txt
└── pip install -r requirements                   

