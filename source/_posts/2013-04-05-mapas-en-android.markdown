---
layout: post
title: "Mapas en Android"
date: 2013-04-05 18:37
published: true
comments: true
categories: [Movil]
---

Saludos alumnos de móvil.

En consideración a que los últimos tres laboratorios han contenido como parte de su desarrollo el uso de mapas en Android (sugerido no obligatorio) y especialmente para aquellos que estarán realizando el proyecto de _transporte urbano_, aquí les pongo los pasos necesarios para poder utilizar el mapa, esta publicación es complementaria al código que ya esta disponible en el [repositorio](https://github.com/j2deme/AndroidApps) de aplicaciones.

__Nota:__ Por modificaciones del API de Android, los mapas __no__ funcionan en el emulador, únicamente en dispositivos físicos.

<!-- more -->

__Dificultad:__ Intermedia

__Tiempo necesario:__ 45~60 minutos

## Paso 0: Descargar Google Play Services SDK

Este se considera el paso inicial, puesto que requiere descargar una librería nueva en Eclipse y puede (o no) tomar algo de tiempo, por lo que se recomienda hacerlo al inicio, mientras se realiza el resto de los pasos.

Contrario a su antecesor, el api de Google Maps para Android, en su versión 2, esta contenido como un servicio del Google Play, por lo que requiere que se descargue esta librería, para lograrlo, en Eclipse, damos click el icono de Android SDK Manager, o en _Window_ > _Android SDK Manager_, donde se nos mostrara la lista de paquetes de APIs y una carpeta llamada _Extras_, en la cual debemos buscar el paquete __Google Play Services__ e instalarlo.

Debemos aceptar la licencia y aceptar la descarga e instalación, en consideración a la velocidad que tengan disponibles de su red, este paso podría tomar un par de minutos o algun par de decenas de minutos, por lo que lo pondremos a descargar y seguiremos con el resto de los pasos.

## Paso 1: Obtener la firma digital SHA1

Este paso es fundamental, ya que sin el, el resto del tutorial no tiene ningún sentido, ya que será imposible hacer uso de los mapas, al menos no de manera nativa.

Para poder solicitar nuestra API key, primero debemos conocer nuestra firma digital SHA1 de _debug_ (desarrollo).

En Windows:
{% codeblock %}
keytool -list -v -keystore "C:\Users\su_usuario\.android\debug.keystore" -alias androiddebugkey -storepass android -keypass android
{% endcodeblock %}

En Linux:
{% codeblock %}
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
{% endcodeblock %}

Y deberan obtener algo similar a lo siguiente:
{% codeblock %}
Alias name: androiddebugkey
 Creation date: Jan 01, 2013
 Entry type: PrivateKeyEntry
 Certificate chain length: 1
 Certificate[1]:
 Owner: CN=Android Debug, O=Android, C=US
 Issuer: CN=Android Debug, O=Android, C=US
 Serial number: 4aa9b300
 Valid from: Mon Jan 01 08:04:04 UTC 2013 until: Mon Jan 01 18:04:04 PST 2033
 Certificate fingerprints:
      MD5:  AE:9F:95:D0:A6:86:89:BC:A8:70:BA:34:FF:6A:AC:F9
      SHA1: BB:0D:AC:74:D3:21:E1:43:07:71:9B:62:90:AF:A1:66:6E:44:5D:75
      Signature algorithm name: SHA1withRSA
      Version: 3
{% endcodeblock %}

Aquí deberan copiar la firma digital SHA1, que para este ejemplo es:
{% codeblock %}
BB:0D:AC:74:D3:21:E1:43:07:71:9B:62:90:AF:A1:66:6E:44:5D:75
{% endcodeblock %}

Recuerden que cada clave es __única__ para cada equipo.

## Paso 2: Crear un proyecto de API

Una vez que tenemos nuestra llave SHA1, el siguiente paso es acceder al __Google API Console__ disponible en [https://code.google.com/apis/console/](https://code.google.com/apis/console/).

En la dirección anterior podremos acceder a la consola de activación de servicios de APIs de Google, donde tendremos acceso a, por ejemplo, las APIs de: Gmail, Youtube, Google Maps, Google Places, Picasa, Google Charts, entre otras.

Para nuestro propósito haremos uso del api de __Google Maps Android API v2__, que configuraremos más adelante, cabe mencionar que se requiere de una cuenta de Gmail para poder hacer uso de los servicios de las APIs, así que tendremos que iniciar sesión o generar una nueva cuenta.

Al abrir la consola de APIs, existen dos opciones posibles:

1. Que nunca hayamos usado la consola de APIS (el caso de la mayoría), por lo que se les solicitará que creen un proyecto para gestionar el uso de las APIs que elijan. Para esto daremos click en __Create Project__, y obtendremos un nuevo proyecto llamado __API Project__.
2. Si ya hemos utilizado la consola de APIs, veremos una lista de los proyectos existentes y servicios disponibles. Sin embargo, es una buena idea usar un nuevo proyecto únicamente para el api de _Google Maps Android_.

En cualquier caso, nos encontraremos con una pantalla donde observaremos una barra similar a la siguiente:
{% img left /images/posts/console1.png 'Barra Lateral' 'Barra Lateral' %}

Desde la cual podremos renombrar, borrar, abrir o crear, o eliminar el borrado de algún proyecto.

Una vez que tengamos un proyecto nuevo el paso siguiente es dar click en __Services__ para configurar el acceso a los diversos servicios ofrecidos por Google, en esta ocasión nos servirá para elegir el API de Google Maps para Android, pero para aquellos que les gusta desarrollar aplicaciones en sus tiempos libres, encontrarán una gran variedad de APIs disponibles para experimentar.

## Paso 3: Activar el API

Una vez dado click en _Services_, se desplegara una lista de todas las APIs disponibles por parte de Google, de donde deberemos buscar __Google Maps Android API v2__ y activarla, tal como se ve en la imagen:
{% img left /images/posts/console2.png 'Google Maps Android API v2' 'Google Maps Android API v2' %}

Una vez hecho esto, si es la primera vez que hacemos uso de esta API, se nos mostrara la licencia de uso, la cual tendremos que aceptar, en caso contrario no podremos utilizar el API elegida, esto solo se realiza una vez.

__Nota:__ Asegurense de elegir el API correcta que corresponde a Android, de lo contrario el resto de los pasos no funcionara.

## Paso 4: Obtener el API Key

Una vez que activamos el servicio, el siguiente paso es solicitar el API key para poderla usar en nuestra aplicación, para lo cual, dentro de la misma Google API Console, daremos click en la opción __API Access__.

Ahi veremos algo más o menos similar a la siguiente imagen:
{% img left /images/posts/console3.png 'API Access' 'API Access' %}

Una vez en esta pantalla, daremos click, en el botón que marcado con __Create new Android key...__, y se nos abrira un diálogo similar a este:
{% img left /images/posts/console4.png 'Configurar API Key' 'Configurar API Key' %}

Aquí ingresaremos en el cuadro de texto, los datos de nuestra firma digital SHA1 (que obtuvimos en el paso 1), y separado con un punto y coma (;), el nombre del paquete de nuestra aplicación, de esta manera:
{% codeblock %}
BB:0D:AC:74:D3:21:E1:43:07:71:9B:62:90:AF:A1:66:6E:44:5D:75;com.j2deme.mapdemo
{% endcodeblock %}

Donde la parte de `com.j2deme.mapdemo` se refiere al nombre del paquete de nuestra aplicación al crearla, generalmente inicia con el `com.`, seguido del nombre de la empresa o alias del desarrollador(`j2deme.` en mi caso) y finalmente el nombre de la aplicación sin espacios y en minúsculas (`mapdemo` en el caso de la aplicación que esta en el repositorio).

Una vez ingresados los datos necesarios, damos click en el botón __Create__ y se nos generara nuestra llave para hacer uso de los mapas de Google en Android:
{% img left /images/posts/console5.png 'API Key para Android' 'API Key para Android' %}

Con esto ya tendremos generada nuestra llave y podremos hacer uso de ella en nuestras aplicación, si requerimos usar el mapa en otra aplicación daremos click en la opción _Edit allowed Android apps_, en donde en una nueva línea añadiremos la misma llave SHA1, y el nombre del paquete de nuestra nueva aplicación, así tantas veces necesitemos.

## Paso 5: Importar Google Play Services al Workspace

Para lograr correctamente este paso, deberemos haber realizado sin problemas los pasos anteriores, de lo contrario debemos regresarnos y resolver cualquier problema que se haya presentado. Tal como lo indique anteriormente, nuevamente lo digo, para poder verificar el correcto funcionamiento de los mapas en Android es __necesario__ el uso de un dispositivo físico, no funciona en el emulador.

Para lograr un ejemplo básico del uso de mapas en Android, lo primero es confirmar que el paquete _Google Play Services_, indicado en el paso 0, se ha finalizado de descargar, de ser así generaremos una nueva aplicación de Android, asegurandonos que el nombre del paquete sea __igual__ al que indicamos en la consola de apis.

Una vez que tengamos nuestra nueva aplicación debemos importar la librería _Google Play Services_ para poderla utilizar en nuestra aplicación, para esto, en Eclipse seleccionamos _File > Import > Android > Existing Android Code into Workspace_ y nos pedira la ruta de la librería, la cual debe estar ubicada dentro de la carpeta del SDK de Android (que viene dentro del zip del ADT) en `extras/google/google_play_services/libproject/google-play-services_lib`.

Es importante considerar que tenemos que importar la librería al workspace (carpeta) donde vayamos a generar nuestra aplicación indicando la opción de _Copy to workspace_ para que la copie y no solo la referencie, de lo contrario no funcionara. Esto quiere decir que si nuestra aplicación no estara en el workspace debemos cambiar la ruta a donde se importara para que funcione.

__Nota:__ En mi caso, yo importe la librería __dentro__ de la carpeta de mi aplicación, y logré que funcionara, porque al ponerla juntas, es decir, la carpeta de la librería y la de mi aplicación en la misma carpeta, no quiso funcionar, sin embargo pueden probar ambas formas para ver cual les funciona. Además, tuve que elegir el API 16 porque me generaba errores con la 17.

## Paso 6: Añadir Google Play Services como dependencia

Una vez que hayamos generado nuestro nuevo proyecto, y hayamos importado la librería _Google Play Services_ a nuestro workspace, el siguiente paso es añadir esta librería como dependencia de nuestro proyecto, para que podamos hacer uso de los mapas y otros servicios relacionados con este SDK.

Para lo anterior, en el explorador de proyectos (normalmente ubicado al lado derecho de la pantalla en Eclipse) damos click derecho sobre la carpeta de nuestro proyecto y configuramos sus propiedades (`Click Derecho > Properties` o `Window > Properties` con el proyecto seleccionado). En la ventana que se nos abre elegimos la pestaña _Android_ y nos desplazamos a la sección de _Library_, y damos click en __Add__.

Se nos abrira una ventana, donde si importamos correctamente la librería _Google Play Services_, nos debe aparecer una carpeta llamada _google-play-services_lib_ (o similar), la elegiremos y daremos click en _OK_.

Debera aparecer la librería añadida con una palomita verde indicado que se añadió correctamente, damos click en _Apply_ y después en _OK_.

## Paso 7: Añadir API key y permisos al manifest

En este punto ya estamos listos para hacer uso de nuestra API key en Android, para lo cual tienen dos opciones, descargar la aplicación demo que yo realize, disponible [aquí](https://github.com/j2deme/AndroidApps/blob/master/MapDemo/) o pueden seguir leyendo para entender como hacer la aplicación desde cero.

Para este paso, es necesario abrir el archivo `AndroidManifest.xml`, cambiarse al editor de XML y añadir lo siguiente antes de la etiqueta `</application>`:
{% codeblock AndroidManifest.xml lang:xml %}
<meta-data
    android:name="com.google.android.maps.v2.API_KEY"
    android:value="su_api_key"/>
{% endcodeblock %}

Dentro del mismo archivo es necesario añadir los permisos de la aplicación, estos nos serviran, entre otras cosas para acceder a la posición gps, usar el internet, guardar los _tiles_ del mapa en la memoria sd, y principalmente usar el mapa, a su vez, sera necesario añadir el uso de un _feature_ (característica) que nos requerira el uso de la libreria OpenGL de acuerdo con los requerimientos del api de Google Maps en su versión 2.

Estos permisos y el _feature_ deberan ir dentro de la etiqueta `<manifest>`, y antes de la etiqueta `<application>`:
{% codeblock AndroidManifest.xml lang:xml %}
<permission
    android:name="com.j2deme.mapdemo.permission.MAPS_RECEIVE"
    android:protectionLevel="signature"/>
    <uses-permission android:name="com.j2deme.mapdemo.permission.MAPS_RECEIVE"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="com.google.android.providers.gsf.permission.READ_GSERVICES"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-feature
        android:glEsVersion="0x00020000"
        android:required="true"/>
{% endcodeblock %}

Observen que generamos un permiso específico de nuestra aplicación (linea 2) que contiene el nombre del paquete de nuestra aplicación (`com.j2deme.mapdemo`), si ustedes estan haciendo la aplicación desde cero, debe de indicar el nombre del paquete de su aplicación, __igual__ al que indicaron al solicitar el API key.

## Paso 8: Añadir el mapa a nuestra aplicación

Una vez configurada nuestra API key y los permisos necesarios en el _manifest_, lo siguiente es modificar el _layout_ de nuestra aplicación para mostrar el mapa, quedando de la siguiente manera:
{% codeblock activity_main.xml lang:xml %}
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity" >
    <fragment xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        class="com.google.android.gms.maps.SupportMapFragment"/>
</RelativeLayout>
{% endcodeblock %}

A lo anterior se le conoce como _Map Fragment_, en el cual, como se supondra podemos añadir un mapa y configurar características como: zoom, inclinación de la cámara, latitud, longitud, tipo de mapa, así como añadir controles para brújula, rotación, desplazamiento, inclinación y zoom. Además de que todas estas opciones pueden configurarse también, directamente desde Java.

Si estamos utilizando Eclipse, ya se nos habrá generado la clase _Activity_ para nuestro mapa, la cual debe contener un método _onCreate_. Sino lo tiene debemos añadirlo:
{% codeblock MainActivity.java lang:java %}
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
}
{% endcodeblock %}

El código anterior, cargara el _layout_ de nuestro mapa como vista de nuestra aplicación. Una vez realizado estos pasos ya podremos ejecutar nuestra aplicación en nuestro dispositivo físico, y si tenemos acceso a Internet, nos debera mostrar un mapa a pantalla completa, con el cual podemos interactuar navegandolo, desplazandonos y haciendo zoom en él.

Aquellos que hayan descargado el código fuente de la aplicación __MapDemo__ observaran que es algo diferente a lo mostrado en este post, ya que incluye otras opciones como el usar el GPS, cambiar el tipo de mapa y mostrar un marcador en el mapa.

## Nota final

Primeramente agradezco de antemano a aquellos que se hayan tomado el tiempo de leer y realizar todos los pasos, ya que me tomo un buen tiempo escribir este post. Espero les sirva de ayuda y referencia para aquellos que quieren usar mapas en sus aplicaciones.

Si encuentran algún problema, haganmelo saber en los comentarios, para que todos puedan opinar.

Para mayor información o problemas específicos les recomiendo revisar las referencias donde tal vez puedan encontrar una solución a su problema o duda.

### Referencias

- [Mobile Tuts+: Android SDK Working with Google Maps – Application Setup](http://mobile.tutsplus.com/tutorials/android/android-sdk-working-with-google-maps-application-setup/)
- [Android Beginning Bunch : Google Maps Android API v2 API Key Generate Tutorial](http://www.android-ever.com/2013/02/google-maps-android-api-v2-tutorial.html)
- [Deep Dive in Android: Google Maps API V2](http://karnshah8890.blogspot.mx/2013/02/google-maps-android-api-v2-introduction.html)
- [Android ER: A simple example using Google Maps Android API v2](http://android-er.blogspot.mx/2012/12/a-simple-example-using-google-maps.html) (Recomendación Personal)
- [Quick start with the Google Maps Android API](https://github.com/googlemaps/hellomap-android) (Proyecto template provisto por Google Maps)
- [Google APIs Console](https://code.google.com/apis/console/)
- [Google Developers: Getting started with Google Maps Android API v2](https://developers.google.com/maps/documentation/android/start)
- [Vogella: Google Maps Android API v2](http://www.vogella.com/articles/AndroidGoogleMaps/article.html)
- [Knowledge by Experience: Google Maps in Android Application with new Google Maps Android API v2 using SupportMapFragment](http://wptrafficanalyzer.in/blog/google-maps-in-android-application-with-new-google-maps-android-api-v2-using-supportmapfragment/)