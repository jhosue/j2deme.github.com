---
layout: post
title: "Práctica POO"
date: 2013-05-22 14:24
published: true
comments: true
categories: [POO]
---

Saludos alumnos.

Tal como les comente en clase, además del proyecto final, dentro de las estrategias de evaluación también se considera una práctica con un valor de 15% que les servira para complementar la calificación que obtengan en su proyecto final.

A continuación podrán encontrar más a detalle el problema a resolver en dicha práctica.

<!-- more -->

# Problema
Se debe generar un algoritmo de encriptación y desencriptación básico, que tome 2 parámetros, el primero de ellos, la acción a realizar, ya sea encriptar o desencriptar, y el segundo parámetro el archivo sobre el cual se va a trabajar, estos parámetros podran ingresarse como parámetros de la consola quedando de la siguiente manera (suponiendo que el programa se llama Crypto):

```
Crypto e miarchivo.txt //Para encriptar

Crypto d miarchivo.txt //Para desencriptar
```
De igual manera, podran leer los parámetros desde la ejecución del programa, es decir:

```
Crypto
[E]ncriptar o [D]esencriptar? E
Archivo a trabajar? miarchivo.txt

Archivo encriptado correctamente!
```

Una vez ingresados los respectivos parámetros, se debe realizar la acción indicada (encriptado o desencriptado), utilizando la implementación del algoritmo que se detalla más adelante, y se debe generar (escribir) un archivo con el resultado de la acción, este archivo debera llamarse igual que el archivo original, pero con el sufijo de la acción realizada, quedando por ejemplo:

```
Encriptando miArchivoSinEncriptar.txt > encriptado-miArchivoSinEncriptar.txt

Desencriptando miArchivoEncriptado.txt > desencriptado-miArchivoEncriptado.txt
```

Queda a su libertad el utilizar cualquier otro tipo de sufijos o prefijos para indicar la acción indicada (`miArchivo.e.txt` para encriptado y `miArchivo.d.txt` para desencriptado, por ejemplo).

## Encriptación y Desencriptación
El algoritmo de encriptado y desencriptado es muy simple, básicamente funciona suponiendo que el alfabeto es un anillo, y que cada letra del alfabeto se desplaza 4 posiciones hacia adelante para realizar la codificación o decodificación necesaria, funcionando de igual manera con los dígitos del 0 al 9, lo que genera un tabla de codificación de la siguiente manera:

```
abcdefghijklmnopqrstuvwxyz
efghijklmnopqrstuvwxyzabcd

0123456789
4567890123
```
De la tabla de codificación anterior se desprende lo siguiente:

- No funciona con letras tales como: ñ, ü, é, etc. Por lo que deberan omitirse al momento de escribir los textos (o permitirlos y no codificarlos).
- No funciona con símbolos tales como: #$%&/()=?¡¿!, etc. Aunque si bien se podría definir una regla de codificación, igualmente deberan omitirse en los textos (o permitirlos y no codificarlos).
- No se indica que hacer con los espacios, pero estos podrían cambiarse por guiones (-) al codificar, o simplemente quedarse iguales.
- No se indica que hacer con las mayúsculas, aunque podrían añadirse al final  (...wxyzABC...), sin embargo, para propósitos de la práctica se recomienda no considerarlas en los textos.

Omitiendo las limitantes que el algoritmo pudiera presentar, este algoritmo es funcional, por lo que para propósitos de esta práctica se debera implementar. Un ejemplo del uso de este algoritmo sería convertir la cadena `hola mundo` a `lspe qyrhs` y viceversa. En su caso deberan tomar textos más extensos, encriptarlos y desencriptarlos.

## Implementación

Deberan generar un clase (_p.e._ `Crypto`) con 2 funciones (además de constructor y destructor) encriptar y desencriptar, las cuales recibiran como parámetro una cadena (encriptada o de texto simple, según sea el caso), y deberán devolver una cadena con la acción indicada.

Los datos se obtendran desde archivos de texto plano (ya sean codificados o no), que seran leídos, procesados, y finalmente se debera guardar el resultado en otro archivo, tal como se indico anteriormente.

Podrán encontrar algunos ejemplos de escritura y lectura de archivos de texto plano [aquí](https://github.com/j2deme/POO_Cpp/tree/master/06_Flujos_y_Archivos/TextoPlano), aunque no estan limitados a eso.

## Consideraciones finales

- El trabajo debera realizarse por equipo, en este caso, serán los mismos equipos ya asignados para el proyecto final, o sí asi lo desean, en equipos a su gusto no mayores a 5 integrantes.
- Deben entregar únicamente un empaquetado (zip) con el código fuente de la aplicación, sin documento.
- La práctica esta pensada para realizarse para consola, pero si se realiza una implementación gráfica, se considerara para puntaje extra.
- La entrega de esta práctica será únicamente el día __Jueves 30 de Mayo de 2013__.