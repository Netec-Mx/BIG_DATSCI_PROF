# Práctica 10. Configuración y despliegue de un proyecto de Big Data en Google Cloud Dataproc

## Objetivo de la práctica:

Al finalizar la práctica, serás capaz de:

- Configurar un clúster de procesamiento de datos con Google Cloud Dataproc.
- Ejecutar tareas de análisis de datos utilizando Hadoop y Hive en el clúster.

## Duración aproximada:
- 40 minutos.

---

**[⬅️ Atrás](../Capítulo9/lab9.2.md)** | **[Lista General](../README.md)** | **[Siguiente ➡️](../Capítulo2/lab2.1.md)**

---

### Instrucciones 

### Tarea 1. Crear un proyecto en Google Cloud Platform.

En esta tarea, configurarás un proyecto en **Google Cloud** para gestionar recursos y permisos necesarios para **Dataproc**.

Paso 1. Si no tienes una cuenta de **Google Cloud Platform**, regístrate [**AQUÍ**](https://cloud.google.com/free/). El proceso incluye una prueba gratuita con crédito inicial, ideal para esta práctica.

Paso 2. Una vez que inicies sesión, entrarás a la consola principal de Google Cloud.

![gcp1](../images/c93/img1.png)

Paso 3. Ahora, en la barra de herramientas superior, hacer clic en el menú desplegable **Select a project**.

![gcp1](../images/c93/img2.png)

Paso 4. En la ventana emergente, dar clic en la opción de **NEW PROJECT**.

![gcp1](../images/c93/img3.png)

Paso 5. Escribir el siguiente nombre del proyecto **`dataprocessing-project`**, y hacer clic en el botón **CREATE**.

![gcp1](../images/c93/img4.png)

Paso 6. Volver a dar clic en la opción **Select a project**.

![gcp1](../images/c93/img2.png)

Paso 7. Dar clic en el nombre del proyecto.

![gcp1](../images/c93/img5.png)

**NOTA:** En el menú de la izquierda, seleccionar **Facturación**. Si es la primera vez que usas Google Cloud, seguir las instrucciones para activar la facturación en el proyecto. Esto permite el acceso a servicios como **Dataproc**, aunque podrás usar el crédito gratuito para esta práctica.

**NOTA:** Si ya tienes configurada tu facturación, avanzar a la siguiente tarea.

**¡TAREA FINALIZADA!**

Haz completado la creación o inicio de sesión de la cuenta de GCP y la creación del proyecto.

### Tarea 2. Habilitar las APIs necesarias

En esta tarea, activarás las APIs de GCP que Dataproc y otros servicios necesitan para funcionar.

**NOTA:** Si es la primera vez que tienes una cuenta de GCP, deberás activar todas las APIs. Si ya tienes una cuenta, solo verifica que no falte alguna por activar.

Paso 1. En el buscador de Google Cloud Platform, escribir **`API & Services`** y dar clic.

![gcp1](../images/c93/img6.png)

Paso 2. Ahora, en el menú lateral izquierdo, dar clic en **Library**.

![gcp1](../images/c93/img7.png)

Paso 3. En la caja de búsqueda central, escribir **Dataproc**.

Paso 4. Seleccionar **Dataproc Resource Manager API**.

![gcp1](../images/c93/img8.png)

Paso 5. Ahora dar clic en la opción de **Dataproc**.

![gcp1](../images/c93/img9.png)

Paso 6. Finalmente, dar clic en la opción **Enable** para activar el servicio.

![gcp1](../images/c93/img10.png)

Paso 7. Una vez habilitado, verás la siguiente interfaz.

![gcp1](../images/c93/img11.png)

Paso 8. Repetir desde el paso 3, pero con la API **Compute Engine API**.

![gcp1](../images/c93/img15.png)
![gcp1](../images/c93/img16.png)
![gcp1](../images/c93/img17.png)

Paso 9. Nuevamente, pero ahora con la API **Dataproc Metastore API**.

![gcp1](../images/c93/img21.png)
![gcp1](../images/c93/img22.png)
![gcp1](../images/c93/img23.png)

Paso 10. Siguiente, la API de **Cloud Dataproc API**.

![gcp1](../images/c93/img24.png)
![gcp1](../images/c93/img25.png)
![gcp1](../images/c93/img26.png)

Paso 11. Siguiente, la API de **Cloud Resource Manager API**.

![gcp1](../images/c93/img28.png)
![gcp1](../images/c93/img29.png)
![gcp1](../images/c93/img30.png)

**NOTA:** Esperar a que se activen las API.

**¡TAREA FINALIZADA!**

Haz completado la activación del servicio de GCP Dataproc y Compute Engine.

### Tarea 3. Configuraciones previas al clúster

En esta tarea, configurarás los permisos necesarios y redes para la creación del clúster de Dataproc.

Paso 1. En el buscador de GCP, escribir **IAM** y dar clic en la opción **IAM**.

![gcp1](../images/c93/img31.png)

Paso 2. En la lista de los usuarios, deberás tener un service principal, con el ícono de una llave; dar clic en el **lápiz** a la derecha para editar los permisos.

**NOTA:** Si no te aparece el usuario service principal, puedes avanzar al paso 5 de esta tarea.

![gcp1](../images/c93/img32.png)

Paso 3. En la ventana lateral derecha, seleccionar de la lista **Role** y cambiar a **Owner**.

![gcp1](../images/c93/img33.png)

Paso 4. Dar clic en la opción **ADD ANOTHER ROLE**.

Paso 5. De la lista, seleccionar **Storage Admin**.

![gcp1](../images/c93/img55.png)

Paso 6. Dar clic en el botón **Save**.

Paso 7. En el buscador de GCP, escribir **VPC** y dar clic en la opción **VPC networks**.

![gcp1](../images/c93/img34.png)

Paso 8. Dar clic en la opción **SUBNETS IN CURRENT PROJECT**.

![gcp1](../images/c93/img35.png)

Paso 9. Filtrar por la **Region: us-central1** y dar clic en el nombre de la subred filtrada llamada **default**.

![gcp1](../images/c93/img36.png)

Paso 10. En los detalles de la subred, dar clic en el botón **EDIT**.

![gcp1](../images/c93/img37.png)

Paso 11. Cambiar la propiedad **Private Google Access** a **On** y dar clic en el botón **Save**.

![gcp1](../images/c93/img38.png)

Paso 12. Regresar a la lista de los VPCs y hacer clic en el menú lateral izquierdo **VPC networks**.

Paso 13. Seleccionar la única VPC que se muestra en la lista y dar clic en el nombre.

Paso 14. Dentro de los detalles de la VPC, dar clic en la opción **DNS CONFIGURATION**.

Paso 15. Dar clic en el botón **ENABLE API**.

![gcp1](../images/c93/img46.png)

**¡TAREA FINALIZADA!**

Haz completado las preconfiguraciones necesarias para crear el clúster de GCP Dataproc.

### Tarea 4. Crear un clúster de Dataproc

En esta tarea, configurarás un clúster Dataproc con las herramientas Hadoop y Hive instaladas para el análisis de datos.

Paso 1. En el menú de búsqueda, escribir **Dataproc** y dar clic.

![gcp1](../images/c93/img12.png)

Paso 2. Ahora dar clic en la opción **+ Create Cluster**.

![gcp1](../images/c93/img13.png)

Paso 3. En la ventana emergente, dar clic en la opción **CREATE** de **Cluster on Compute Engine**.

![gcp1](../images/c93/img14.png)

Paso 4. Configurar los siguientes datos de la tabla para la creación del clúster de Dataproc.

| Parametro | Valor |
| --------- | ----- |
|  Cluster Name | bdhadoop-XXXX-### (Cambia las **X** por las letras iniciales de tu nombre y los **#** por números aleatorios) |
| Subnetwork | default |
| Optional components  | - [x] Hive WebHCat |

![gcp1](../images/c93/img18.png)
![gcp1](../images/c93/img39.png)
![gcp1](../images/c93/img19.png)

**NOTA:** El resto de los valores se quedarán por defecto.

Paso 5. Dar clic en el botón **CREATE**.

![gcp1](../images/c93/img20.png)

**NOTA:** Si al momento de crear el clúster te aparece un mensaje de capacidad de disco duro SSD, debes reducir el tamaño de los discos de los nodos.

![gcp1](../images/c93/img27.png)

**NOTA:** Si te sale un mensaje sobre las API, verificar los pasos de la tarea uno que se hayan habilitado cada una de las APIs.

**NOTA:** El clúster tardará de **2 a 3 minutos** aproximadamente.

Paso 6. Cuando el clúster ya tenga el estatus **Running**, dar clic en el nombre del clúster.

![gcp1](../images/c93/img40.png)

Paso 7. Dar clic en la opción **VM INSTANCES**.

![gcp1](../images/c93/img41.png)

Paso 8. En el nodo con el nombre **Master**, dar clic en la propiedad **SSH** para abrir la conexión al clúster.

![gcp1](../images/c93/img42.png)

Paso 9. Se abrirá una ventana nueva para la **Autorización**; dar clic en **Authorize**.

![gcp1](../images/c93/img43.png)

**NOTA:** Debes permitir las ventanas emergentes para que se realice la conexión exitosamente.

Paso 10. Una vez realizada la conexión, verás la terminal del servidor maestro.

![gcp1](../images/c93/img44.png)

**¡TAREA FINALIZADA!**

Haz completado la creación del clúster de Dataproc exitosamente.

### Tarea 5. Cargar datos en Cloud Storage

En esta tarea, subirás un archivo de datos a Cloud Storage para que el clúster pueda acceder a él.

Paso 1. Descargar el archivo desde la siguiente URL, cópiala y pégala en una pestaña del navegador.

**NOTA:** Si ya lo descargaste en laboratorios anteriores, puedes omitir este paso y avanzar al paso 2.

```
curl https://s3.us-west-2.amazonaws.com/labs.netec.com/courses/BigDataSciencePro/V0.0.1/ventasejemplo.csv
```

Paso 2. Dentro de la máquina virtual del nodo **Master**, dar clic en la opción **UPLOAD FILE**.

![gcp1](../images/c93/img47.png)

Paso 3. Sigue los pasos para cargar el archivo **ventasejemplo.csv** a la máquina virtual del nodo Master.

Paso 4. Una vez cargado, escribir el comando **ls** para verificar que se haya cargado.

![gcp1](../images/c93/img48.png)

Paso 5. Dentro de la máquina virtual del nodo **Master**, ejecutar el siguiente comando para ver los buckets creados por el clúster.

```
gsutil ls
```

![gcp1](../images/c93/img45.png)

Paso 6. Editar el siguiente comando y sustituir la palabra **TU_BUCKET_STAGING** por el valor del bucket staging del paso anterior, una vez editado, pegarlo en la terminal del nodo.

```
gsutil cp ventasejemplo.csv gs://TU_BUCKET_STAGING/data/ventasejemplo.csv
```

![gcp1](../images/c93/img49.png)

Paso 7. Verificar que se haya cargado correctamente, copiar el siguiente comando.

```
gsutil ls gs://TU_BUCKET_STAGING/data/
```

![gcp1](../images/c93/img50.png)

**¡TAREA FINALIZADA!**

Haz completado la carga de los datos al bucket de Cloud Storage.

### Tarea 6. Ejecutar consultas de Hive en el clúster.

En esta tarea, cargarás el archivo de datos en una tabla de Hive y ejecutarás consultas para analizar los datos.

Paso 1. Primero, debes conectarte a **Hive**; escribir el siguiente comando en la terminal.

```
hive
```

Paso 2. Ya conectado a **Hive**, crear la tabla externa que guardará los datos. Copiar el siguiente código en un bloc de notas, editar la variable **TU_BUCKET_STAGING** y después pegar en la terminal de **Hive**.

```
CREATE EXTERNAL TABLE ventas (
  id INT,
  nombre_cliente STRING,
  producto STRING,
  cantidad INT,
  precio_unitario FLOAT,
  fecha_venta STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 'gs://TU_BUCKET_STAGING/data/'
TBLPROPERTIES ("skip.header.line.count"="1");
```

![gcp1](../images/c93/img51.png)

Paso 3. Verificar que los datos se hayan cargado correctamente, copiando el siguiente comando.
```
SELECT * FROM ventas LIMIT 10;
```

![gcp1](../images/c93/img52.png)

Paso 4. Realizar una prueba más para interactuar con la información, copiando y pegando la siguiente consulta.

```
SELECT producto, SUM(cantidad * precio_unitario) AS total_ventas
FROM ventas
GROUP BY producto;
```

![gcp1](../images/c93/img53.png)

Paso 5. Esta prueba es un poco más avanzada, **¿Puedes deducir el resultado antes de ejecutarla?**.

```
SELECT 
    producto,
    COUNT(*) AS total_transacciones,
    SUM(cantidad) AS total_cantidad,
    ROUND(SUM(cantidad * precio_unitario), 2) AS total_ventas,
    ROUND(AVG(cantidad * precio_unitario), 2) AS venta_promedio,
    MAX(cantidad * precio_unitario) AS venta_maxima,
    MIN(cantidad * precio_unitario) AS venta_minima
FROM 
    ventas
WHERE 
    fecha_venta BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY 
    producto
HAVING 
    ROUND(SUM(cantidad * precio_unitario), 2) > 1000
ORDER BY 
    total_ventas DESC
LIMIT 10;
```

![gcp1](../images/c93/img54.png)

**¡TAREA FINALIZADA!**

Haz completado la ejecución de consultas de Hive en el clúster de GCP Dataproc.

**LABORATORIO FINALIZADO!**

### Resultado esperado

El resultado final del laboratorio es la ejecución correcta de todas las tareas y la verificación de la última consulta.

![gcp1](../images/c93/img54.png)

---

**[⬅️ Atrás](../Capítulo9/lab9.2.md)** | **[Lista General](../README.md)** | **[Siguiente ➡️](../Capítulo2/lab2.1.md)**

---
