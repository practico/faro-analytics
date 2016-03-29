# Faro para Analytics mediante AppEngine

Cuando es imposible embeber el codigo JavaScript proporcionado por Google Analytics, esta aplicacion permite incrustar una simple imagen como pixel de seguimiento.


### Desplegando en AppEngine de Google




### Uso del Faro

Ingrese a su cuenta Google Analytics y genere una nueva propiedad sobre la que desea hacer seguimiento (o busque una existente).

* Haga clic en "Obtener ID de seguimiento", copie el valor de ID `UA-XXXXX-X`

Ahora, agregue una imagen a las paginas que desea seguir:

* _https://suaplicacion-rastreadora.appspot.com/UA-XXXXX-X/Cualquier/Ruta/Adicional_
* `UA-XXXXX-X` corresponde al ID de seguimiento entregado por Analytics
* `/Cualquier/Ruta/Adicional` es una ruta arbitraria autodescriptiva para usted y debe ser proporcionada de manera manual.

Ejemplo para quienes usan Markdown:

```markdown
[![Analytics](https://suaplicacion-rastreadora.appspot.com/UA-XXXXX-X/pagina-ejemplo)](https://github.com/practico/rastreador-visitas)
```

Si lo prefiere, puede utilizar un pixel transparente. Simplemente agregue `?pixel` a la URL de una imagen y eso es todo.

Agregando esa imagen podra rastrear en su panel de Google Analytics, incluso en tiempo real, las paginas donde sea incrustada.


### FAQ

- **How does this work?** Google Analytics provides a [measurement protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide) which allows us to POST arbitrary visit data directly to Google servers, and that's exactly what GA Beacon does: we include an image request on our pages which hits the GA Beacon service, and GA Beacon POSTs the visit data to Google Analytics to record the visit. As a result, if you can embed an image, you can beacon data to Google Analytics.

- **Why do we need to proxy?** Google Analytics supports reporting of visit data [via GET requests](https://developers.google.com/analytics/devguides/collection/protocol/v1/reference#transport), but unfortunately we can't use that directly because we need to generate and report a unique visitor ID for each hit - e.g. some pages do not allow us to run JS on the client to generate the ID. To address this, we proxy the request through ga-beacon.appspot.com, which in turn is responsible for generating the unique visitor ID (server generated UUID), setting the appropriate cookies for repeat hits, and reporting the hits to Google Analytics.

- **What about referrals and other visitor information?** Unfortunately the static tracking pixel approach limits the information we can collect about the visit. For example, referral information can't be passed to the tracking pixel because we can't execute JavaScript. As a result, the available metrics are restricted to unique visitors, pageviews, and the User-Agent and IP address of the visitor.

- **Do I have to use ga-beacon.appspot.com?** You can if you want to - it's free, but there are no capacity or availability promises. For best results, deploy your own instance directly on Google App Engine: clone this repository, change the project name, and deploy your own instance - easy as that. The project is under MIT license.


* [Using a Beacon Image for GitHub, Website and Email Analytics](http://www.sitepoint.com/using-beacon-image-github-website-email-analytics/)
* [Tracking Google Sheet views with Google Analytics using GA Beacon](http://mashe.hawksey.info/2014/02/tracking-google-sheet-views-with-google-analytics/)



=====================================================================
   Rastreador de Visitas (Faro para Analytics mediante AppEngine)
   Copyright (C) 2016  John F. Arroyave Gutiérrez
                       unix4you2@gmail.com
                       www.practico.org
========================================================================

 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.

 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.

 You should have received a copy of the GNU General Public License
 along with this program.  If not, see <http://www.gnu.org/licenses/>
                                      
------------------------------------------------------------------------
INSTALACION:



	1) Haga un Fork a este repositorio
	
	2) En su computadora descargue el repo para ser actualizado


------------------------------------------------------------------------
## Desinstalación del rastreador:

  * Elimine todos los llamados provenientes de su aplicacion hacia
    el AppEngine.
    
  * Elimine la instancia sobre su AppEngine desde su panel GoogleCloud
