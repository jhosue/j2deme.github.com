---
layout: post
title: "Solución al problema de iostream"
date: 2013-02-21 18:00
published: true
comments: false
categories: [POO]
---

Para los alumnos de POO.

Algunos me mencionaron que no podían compilar los códigos que les puse en el repositorio, esto es porque como ya le mencione en clase, la libreria __iostream__, no esta diponible por default en Windows (en ninguna de sus versiones), me puse a investigar el día de ayer, y la hice funcionar sobre Windows 7 Ultimate, pero en teoría los pasos que les voy a poner deberían de funcionar para cualquier versión de Windows.

<!--more-->

Los pasos los tome de un tutorial en inglés, disponible en <a title="Installing Cygwin" href="http://cs.calvin.edu/curriculum/cs/112/resources/installingEclipse/cygwin/" target="_blank">aqui</a>, si saben leer en inglés y lo entienden pueden revisarlo ustedes mismos, sino les traduzco las instrucciones a continuación (si tienen dudas revisen las imágenes del tutoral original):
<ol>
	<li>Vayan a la página de Cygwin (<a title="Cygwin" href="http://www.cygwin.com/" target="_blank">http://www.cygwin.com/</a>)</li>
	<li>Busquen la sección de "Install Cygwin" y descarguen el archivo <strong>Setup.exe</strong> y descarguenlo, o directamente <a title="Cygwin Setup" href="http://cygwin.com/setup.exe" target="_blank">aquí</a>.</li>
	<li>Guarden el ejecutable, una vez descargado, denle click para instalarlo.</li>
	<li>En la primera pantalla del instalador, den click en <strong>Siguiente</strong>.</li>
	<li>En la segunda pantalla pregunta desde donde queremos instalarlo, en este caso por sera por Internet, por lo que tenemos que marcar la <strong>primera</strong> opción.</li>
	<li>En la tercera pantalla nos pregunta donde queremos instalarlo y para que usuarios, les recomiendo no mover nada ahí, y solo dar <strong>Siguiente</strong>.</li>
	<li>En la cuarta pantalla nos pregunta donde queremos descargar los paquetes, debe ser en la misma carpeta donde esta el instalador, ya sea en su escritorio, o en la carpeta de descargas, y damos <strong>Siguiente</strong>.</li>
	<li>En la quinta pantalla solicita información sobre el tipo de conexión a usar, debe estar marcada la <strong>primera</strong>, conexión directa, y damos <strong>Siguiente</strong>.</li>
	<li>En la sexta pantalla nos pide seleccionar un sitio para descargar los paquetes, seleccionen cualquiera que les guste, la diferencia solo seran unos minutos más o menos de descarga, y damos <strong>Siguiente</strong>.</li>
	<li>Tardara un momento, y nos saldra un dialogo para escoger lo que queremos instalar, algunos paquetes ya vienen seleccionados por default, esos los deben dejar así, y buscaremos los siguientes: <strong>g++</strong>, <strong>make</strong> y <strong>gdb</strong>.</li>
	<li>Para instalar <strong>g++</strong> damos click en el símbolo <strong>+</strong> al lado de donde dice <strong>Devel</strong>,  buscamos donde dice <strong>gcc-g++ C++ Compiler</strong> y damos donde dice <strong>Skip</strong>, para seleccionarlo para descargar, también se seleccionara automáticamente <strong>gcc-core C compiler</strong>.</li>
	<li>Para instalar <strong>gdb</strong>, buscamos dentro de la misma carpeta <strong>Devel</strong> donde diga <strong>gdb GNU Debugger</strong>, y damos click en <strong>Skip</strong> para seleccionarlo para descarga.</li>
	<li>Para instalar <strong>make</strong>, nuevamente dentro de <strong>Devel</strong>, buscamos donde diga <strong>make</strong> y damos click en <strong>Skip</strong> también para instalarlo.</li>
	<li>Una vez seleccionados los paquetes damos click en <strong>Siguiente</strong> (Next) y se comenzará la descarga, que tomara dependiendo de la conexión entre 10 y 20 minutos, una vez finalizada daremos click en <strong>Finish</strong> y nos avisara con un diálogo de Installation Complete, donde damos <strong>OK</strong>.</li>
	<li>Con esto ya tendremos g++, make y gdb instalados.</li>
</ol>
Una vez instalado Cygwin, y las respectivas g++, make y gdb, los siguiente es añadirlas al denominado PATH del sistema para poderlas usar. Para esto seguimos las siguientes instrucciones, disponibles en inglés <a title="Path" href="http://cs.calvin.edu/curriculum/cs/112/resources/installingEclipse/path/" target="_blank">aqui</a>:
<ol>
	<li>En el Panel de Control buscamos <strong>Sistema</strong>.</li>
	<li>En dentro de Sistema, buscamos Propiedades del Sistema,  y después <strong>Propiedades Avanzadas</strong>.</li>
	<li>Dentro de las propiedades avanzadas encontraremos el botón que dice <strong>Variables de Sistema</strong> (Environment Variables) y le damos click.</li>
	<li>En la ventana Variables de Sistema que se abre, buscamos en la sección de <strong>Variables de Sistema</strong> y ahí buscamos donde diga <strong>PATH</strong>.</li>
	<li>Seleccionamos <strong>PATH</strong> y damos click en <strong>Editar</strong>, nos aparecera un cuadro de diálogo con dos campos de texto, en el <strong>segundo</strong>, añadiremos los siguiente:
<pre>;C:\cygwin\bin\</pre>
</li>
	<li>Debemos tener cuidado de que la ruta anterior sea igual a la ruta donde instalamos Cygwin, sino cambiaron nada y siguieron las instrucciones tal como lo indique, deberá de ser la misma, la ruta va completa con todo y el punto y coma (;) al inicio.</li>
	<li>Damos click en <strong>OK</strong> (o Aceptar) para guardar, y damos Aceptar en los diálogos hasta cerrarlos todos, con esto ya tendremos instalado g++, make y gdb en el PATH del sistema y podremos usar la librería <strong>iostream </strong>que es la librería estándar para leer y escribir.</li>
</ol>
Si siguieron las instrucciones podrán usar y compilar sin ningún problema los códigos que les puse en el repositorio de código, de manera que sin importar si ustedes usan Windows y yo Linux, deberían de funcionar.

Espero sus tareas el día de mañana <strong>viernes 22 de febrero</strong>.
