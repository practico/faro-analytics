#Faro simplificado para Google Analytics

Cuando es imposible embeber el codigo JavaScript proporcionado por Google Analytics, esta aplicacion permite incrustar una simple imagen como pixel de seguimiento.

## Preparando la infraestructura

### **PASO 1:** Preparando la instancia AppEngine y el SDK
 1. Vaya a su consola de Google Cloud y cree un nuevo proyecto.  En lo posible personalice su ID para hacerlo mnemotécnico.
 2. Descargue y descomprima el Google App Engine SDK de Go correspondiente a su sistema operativo en una carpeta determinada, por ejemplo sobre **/opt/go_appengine/**   *(https://cloud.google.com/appengine/downloads?csw=1)*
 3. Asegúrese de contar con las dependencias requeridas por el SDK como Phyton.  Use **/usr/bin/env python -V**  para verificar la versión instalada.
 4. Asegúrese de tener incluída en el PATH la ruta hacia el SDK mediante **export PATH=$PATH:/opt/go_appengine/**  En caso de contar con otros SDK para AppEngine asegúrese que el único PATH incluído sea el de Go para evitar conflictos.

### **PASO 2:** Personalizando el Faro
 1. Clone este repositorio en su computadora (*si lo desea también puede hacer un Fork a su cuenta para guardar cualquier cambio en su aplicación rastreadora y clonarlo desde allí*)
 2. En caso de hacer un Fork, se recomienda que cambie el nombre del repositorio para que coincida con el nombre del proyecto creado en Google Cloud.
 3. Edite el archivo app.yaml cambiando el nombre de aplicación para que coincida con el ID del proyecto.
 4. Cambie el nombre de la carpeta que contiene el rastreador de visitas para que coincida con el ID de proyecto.
 5. Cambie el nombre del script Go del rastreador de visitas para que coincida con el ID del proyecto.
 6. Edite el archivo page.html y el script Go del rastreador de visitas cambiando todos los valores de "rastreador-visitas" para que coincida con su ID de proyecto.

### **PASO 3:** Desplegando la aplicación
 1. Vaya al directorio donde ha clonado el repositorio y ejecute **dev_appserver.py​ ​ ​nombre-del-proyecto** para probarlo.   Se supone que "nombre-del-proyecto" es la carpeta que contiene toad la aplicación clonada.  Si todo va bien en su consola verá que se genera un servidor web para ir a la aplicación y sus estadísticas.  Por ejemplo sobre http://localhost:8000
 2. Ejecute luego para desplegar sobre su AppEngine el comando **appcfg.py update nombre-del-proyecto**   Tenga en cuenta que si es primera vez que usa el SDK el navegador debería abrir una ventana para que usted autorice el acceso del SDK hasta su cuenta de AppEngine.

## Uso del faro

Ingrese a su cuenta Google Analytics y genere una nueva propiedad sobre la que desea hacer seguimiento (o busque una existente).

* Haga clic en "Obtener ID de seguimiento", copie el valor de ID `UA-XXXXX-X`

Ahora, agregue una imagen a las paginas que desea seguir:

* _https://nombre-del-proyecto.appspot.com/UA-XXXXX-X/Cualquier/Ruta/Adicional_
* `UA-XXXXX-X` corresponde al ID de seguimiento entregado por Analytics
* `/Cualquier/Ruta/Adicional` es una ruta arbitraria autodescriptiva para usted y debe ser proporcionada de manera manual.

Ejemplo para quienes usan Markdown:

```markdown
[![Analytics](https://nombre-del-proyecto.appspot.com/UA-XXXXX-X/pagina-ejemplo)](https://github.com/practico/rastreador-visitas)
```

Si lo prefiere, puede utilizar un pixel transparente. Simplemente agregue `?pixel` a la URL de una imagen y eso es todo.

Agregando esa imagen podra rastrear en su panel de Google Analytics, incluso en tiempo real, las paginas donde sea incrustada.


### Informacion adicional
* [Informacion del protocolo de medicion de Analytics para desarrolladores](https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide)

------------------------------------------------------------------------
## Desinstalación del rastreador:
 1. Elimine todos los llamados provenientes de su aplicacion hacia
    el AppEngine.
 2. Elimine la instancia sobre su AppEngine desde su panel GoogleCloud
