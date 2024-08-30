---
title: "Como contribuir en un repositorio oficial de Go"
date: 2024-08-28T17:36:39-03:00
draft: false
author: Thiago Mowszet 
year: "2024"
month: "2024/08"
categories:
- Go
- Comunidad
tags:
- Comunidad
- Golang
- Repositorio oficial
keywords:
- Go
- Go Team
- Contribute
disableComments: false
---

{{<postimage "images/gopher.png" "Gopher">}}

Hace poco, nuestra comunidad logro contribuir por primera vez contribuir a un repositorio oficial de Go, creando la versión en español del Tour de Go.

A lo largo de este artículo, descubriras los requisitos, los desafíos que enfrentamos, y las soluciones que implementamos al colaborar con el Go Team. 

¡Espero que esta guía te sea útil para futuras contribuciones! 💡.

<!--more-->

## Pre-Requisitos

Go cuenta con su propia [guía](https://go.dev/doc/contribute) para que puedas orientarte y conocer los pasos a seguir. La idea de este post no es replicar esa guía, sino resumirte los pasos que nosotros realizamos para empezar a contribuir.

**Paso 0: Elegi una cuenta de Google** 

Las contribuciones a Go, se hacen mediante una cuenta de Google con un mail especifico, asegurate que estes usando la misma cuenta a lo largo del proceso.
Tambien debes tener en cuenta que la cuenta de Git sea la misma de Google. Podes hacer esto de la siguiente forma:

```shell
$ git config --global user.email name@example.com   # cambia la configuracion global
$ git config user.email name@example.com            # cambia la configuracion local
```

**Paso 1: Acepta las licencias de colaborador**

Antes de enviar tus cambios, deberas de completar una de las siguientes CLA's (Contributor License Agreement - Acuerdo de licencia de colaborador):

* Si sos es el titular de los derechos de autor, tendrás que aceptar el acuerdo de [licencia de colaborador individual](https://cla.developers.google.com/about/google-individual), que puede completarse en línea.
* Si la organización es la titular de los derechos de autor, deberá aceptar el acuerdo de [licencia de colaborador corporativo](https://cla.developers.google.com/about/google-corporate).

**Paso 2: Configura la autenticacion de Git**

El repositorio principal de Go se encuentra en go.googlesource.com, un [servidor Git alojado en Google](https://go.googlesource.com/). La autenticación en el servidor web se realiza a través de tu cuenta de Google, pero también necesitas configurar git en tu ordenador para acceder a él. Siguiendo estos pasos para obtener acceso:

1. Visita go.googlesource.com y haz clic en "Generar contraseña" en la barra de menú superior derecha de la página. Se te redirigirá a accounts.google.com para iniciar sesión.

2. Tras iniciar sesión, accederás a una página con el título "Configurar Git". Esta página contiene un script personalizado que, al ejecutarse localmente, configurará Git para mantener tu clave de autenticación única. Esta clave se empareja con otra que se genera y almacena en el servidor, de forma análoga a como funcionan las claves SSH.

3. Copia y ejecuta este script localmente en tu terminal para almacenar tu token secreto de autenticación en un archivo .gitcookies. Si utiliza un ordenador con Windows y ejecuta cmd, deberá seguir las instrucciones del cuadro amarillo para ejecutar el comando; de lo contrario, ejecute el script normal.


**Paso 3: Crea una cuenta de Gerrit**

Gerrit es una herramienta de código abierto utilizada por los mantenedores de Go para discutir y revisar las nuevas propuestas o cambios.

Para registrar su cuenta, visite go-review.googlesource.com/login/ e inicie sesión una vez con la misma cuenta de Google que utilizó anteriormente.


**Paso 4: Instala el comando git-codereview**

Los cambios en Go deben ser revisados antes de ser aceptados, independientemente de quién los realice. Un comando git personalizado llamado git-codereview simplifica el envío de cambios a Gerrit.

Instala el comando git-codereview ejecutando:

```shell
go install golang.org/x/review/git-codereview@latest 
# Podes ejecutar luego: 'git codereview help' para conocer mas sobre el comando.
```


# Como comenzamos?
Lo primero fue elegir el nombre del proyecto, pensamos en ideas como: go-tour_es, tour-es y al final quedo go-tour-es como opción ganadora, siguiendo la sintaxis del repositorio anterior
generado en español por @rcostu.

# Primeros problemas
Una vez creado el repositorio comenzamos a traducir los diferentes módulos que existían y notamos dos inconvenientes:

1. Necesitábamos un live-reload para poder ver los cambios en tiempo real que realizábamos.
2. Notábamos que cuando clonamos el repo no se podía hacer un build y ejecutarlo de forma local.

y esto se debia a que habiamos elegido mal el repositorio para trabajar, ya que trabajamos sobre un repositorio que no correspondia.
El correcto es el siguiente: https://cs.opensource.google/go/x/website

y si nos fijamos bien, en la guia oficial es justamente lo que nos indica:

{{<postimage "images/contribuite-guide.png" "Guia Oficial">}}
