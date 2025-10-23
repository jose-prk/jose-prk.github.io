---
title: Qué es GrapheneOS y cómo instalarlo en tu dispositivo
description: En un mundo donde la privacidad y la seguridad en línea son cada vez más importantes, el primer paso esencial que debemos tomar es cambiar nuestro sistema operativo. Este es el software principal que ejecuta todas las aplicaciones y que se comunica directamente con el hardware de nuestro dispositivo.
date: 2024-08-31 19:28:00 +0200
categories: [Android]
tags: [GrapheneOS, Android, Privacidad, Principiante]
pin: true
mermaid: true
image:
  path: /assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/grapheneos.png
  alt: GrapheneOS
---

## Índice

1. [Introducción](#Introducción) 
2. [¿Qué es GrapheneOS](#Que-es-GrapheneOS)
3. [Características de GrapheneOS](#Características-de-GrapheneOS)
4. [Como instalar GrapheneOS](#Como-instalar-GrapheneOS)
	1. [Requisitos](#Requisitos)
	2. [Instalación](#Instalacion)

## 1. Introducción {#Introducción}

En un mundo donde la privacidad y la seguridad en línea son cada vez más importantes, el primer paso esencial que debemos tomar es cambiar nuestro sistema operativo. Este es el software principal que ejecuta todas las aplicaciones y que se comunica directamente con el hardware de nuestro dispositivo. Si bien es verdad que Android es un sistema operativo de código abierto, lo cierto es que Google crea su propia capa de personalización sobre Android con GMS (Google Mobile Services) y los fabricantes realizan modificaciones al sistema base, creando sus propias distribuciones de Android que implementan componentes privativos y aplicaciones que espían y monitorizan nuestras actividades.

Es por ello que la mejor opción, es utilizar alternativas mas puras de Android que no incluyen este tipo de componentes privativos, o que incluso han sido desarrollados con enfoques específicos en la privacidad y la seguridad, añadiendo características adicionales al sistema base de Android. Existen diversas alternativas, entre las principales se encuentran GrapheneOS, CalyxOS, LineageOS o Lineage for MicroG, entre otras. En este artículo nos centraremos en GrapheneOS, puesto que es la mejor opción en términos de privacidad y seguridad y además, es la mas fácil de instalar para aquellos usuarios sin conocimientos técnicos. Exploraremos qué es GrapheneOS, cuales son sus principales características y cómo instalarlo en nuestro dispositivo.

## 2. ¿Qué es GrapheneOS? {#Que-es-GrapheneOS}

GrapheneOS es un sistema operativo de código abierto basado en AOSP (Android Open Source Project) que busca ofrecer una alternativa segura y privada para dispositivos móviles. Esta distribución de Android solo es compatible con los teléfonos Google Pixel. Esto se debe a los altos estándares de seguridad de GrapheneOS, que solo son cumplidos por los dispositivos Pixel, ya que están diseñados con un hardware que permite un mejor soporte para las características de seguridad avanzadas que GrapheneOS implementa, como el uso del chip de seguridad Titan M, que proporciona una capa adicional de protección con funciones como el arranque seguro o el cifrado por hardware.

## 3. Características de GrapheneOS {#Características-de-GrapheneOS}

GrapheneOS ofrece diversas características que mejoran la privacidad y seguridad de nuestro dispositivo. Algunas de estas incluyen:
1. Incremento del número máximo de caracteres del PIN y la contraseña, de 16 caracteres a 128 caracteres.
2. **PIN/Contraseña de coacción o duress password.** Permite borrar todo el contenido del dispositivo al introducir un pin o contraseña específicos.
3. El PIN o la contraseña no se muestran al ser introducidos.
4. **PIN Scrambling.** Reorganiza aleatoriamente el teclado del PIN en la pantalla de bloqueo, dificultando la adivinanza del código a partir del patrón de movimiento del dedo.
5. Desactivación de animaciones al ingresar el PIN de desbloqueo, lo que ayuda a evitar que otros vean las teclas que se están pulsando.
6. **Desbloqueo sin confirmación automática.** Impide desbloquear el teléfono automáticamente al ingresar la contraseña correcta; es necesario presionar un botón de confirmación.
7. **Storage Scopes.** En lugar de otorgar acceso completo a todos los datos del dispositivo, el permiso storage scopes permite especificar y restringir el acceso únicamente a aquellos recursos que son necesarios para el funcionamiento de la aplicación. 
	Por ejemplo, en lugar de permitir que una aplicación acceda a todos los archivos multimedia del usuario, storage scopes permite restringir el acceso de las aplicaciones únicamente a aquellos archivos multimedia que se deseen.
8. **Contact Scopes.** En lugar de otorgar a una aplicación acceso completo a todos los contactos del dispositivo, el permiso contact scopes permite especificar y restringir el acceso únicamente a un solo contacto o un grupo limitado de contactos.
9. **Desactivación de Wi-Fi y Bluetooth por inactividad.** Esta función apaga automáticamente las conexiones Wi-Fi y Bluetooth cuando no se están utilizando tras un tiempo determinado, lo que ayuda a conservar la batería y reduce la exposición a posibles ataques de red.
10. **Autoreboot.** Esta característica permite que el dispositivo se reinicie automáticamente en intervalos programados. Esto ayuda a mantener el sistema operativo en un estado óptimo, mejorando su rendimiento, cerrando aplicaciones que podrían estar funcionando en segundo plano y liberando recursos, previniendo ataques y el uso indebido de recursos del dispositivo por parte de aplicaciones maliciosas y a aplicar actualizaciones de seguridad de manera más efectiva.
11. **Degoogleado.** GrapheneOS no tiene ninguna dependencia de los servicios de Google por defecto, lo que mejora la privacidad del usuario al eliminar la recopilación de datos por parte de Google.
12. **Posibilidad de instalar los Google Play services en un entorno seguro y aislado (sandbox).** Esta característica permite a los usuarios instalar los Google Play Services en un entorno aislado que limita su acceso a otros datos y aplicaciones del dispositivo. Esto ayuda a mantener la privacidad del usuario mientras se utilizan aplicaciones que dependen de estos servicios.
13. **Perfiles de usuario aislados.** GrapheneOS permite crear perfiles de usuario separados y aislados en el mismo dispositivo, cada uno con su propio cifrado independiente del resto. Esto significa que cada perfil puede tener sus propias aplicaciones y configuraciones, lo que mejora la privacidad y la seguridad al evitar que las aplicaciones de un perfil accedan a los datos de otro.
14. **Aleatoriedad de la dirección MAC.** La dirección MAC es el identificador de la tarjeta de red del dispositivo. Esta función cambia la dirección MAC del dispositivo de forma aleatoria en cada conexión Wi-Fi. Esto ayuda a proteger la privacidad del usuario al dificultar el seguimiento del dispositivo en redes Wi-Fi.
15. **Aplicaciones privadas por defecto.** GrapheneOS incluye aplicaciones de código abierto necesarias para el uso básico del sistema, como la cámara, teléfono, contactos, sms, navegador, visor de pdf, launcher o teclado, entre otras, que están diseñadas para ser respetuosas con la privacidad al no recopilar datos y estar configuradas para proteger la información del usuario desde el principio, ofreciendo una alternativa más segura y privada a las aplicaciones predeterminadas de otras distribuciones de Android.
16. **Copias de seguridad cifradas.** Esta característica permite a los usuarios realizar copias de seguridad de sus datos tanto en local como en servicios en la nube, de manera segura mediante cifrado.

## 4. Como instalar GrapheneOS {#Como-instalar-GrapheneOS}

GrapheneOS ofrece dos métodos de instalación oficialmente soportados. Los usuarios pueden optar por el instalador basado en WebUSB, recomendado para la mayoría de usuarios, o seguir la guía de instalación mediante línea de comandos, destinada a usuarios más técnicos. En este caso nos centraremos en la primera opción, ya que este artículo está dirigido para usuarios no técnicos.
### 4.1. Requisitos {#Requisitos}

1. Teléfono Google Pixel compatible. En la siguiente tabla obtenida del sitio web oficial, podemos ver los dispositivos soportados y la duración de su soporte.
	
	| Dispositivo | Fin del soporte mínimo OEM | Duración mínima del soporte OEM |
	|-------------|----------------------------|---------------------------------|
	| Google Pixel 9 Pro Fold | Agosto 2031 | 7 años |
	| Google Pixel 9 Pro XL | Agosto 2031 | 7 años |
	| Google Pixel 9 Pro | Agosto 2031 | 7 años |
	| Google Pixel 9 | Agosto 2031 | 7 años |
	| Google Pixel 8a | Mayo 2031 | 7 años |
	| Google Pixel 8 Pro | Octubre 2030 | 7 años |
	| Google Pixel 8 | Octubre 2030 | 7 años |
	| Google Pixel Fold | Junio 2028 | 5 años |
	| Google Pixel Tablet | Junio 2028 | 5 años |
	| Google Pixel 7a | Mayo 2028 | 5 años |
	| Google Pixel 7 Pro | Octubre 2027 | 5 años |
	| Google Pixel 7 | Octubre 2027 | 5 años |
	| Google Pixel 6a | Julio 2027 | 5 años |
	| Google Pixel 6 Pro | Octubre 2026 | 5 años |
	| Google Pixel 6 | Octubre 2026 | 5 años |
	| Google Pixel 5a | Agosto 2024 | 3 años |

2. Tener el teléfono cargado por encima del 80% de batería.
3. Tener el sistema operativo que viene preinstalado de fábrica en el teléfono actualizado a su última versión.
4. Un ordenador para ejecutar el instalador web con al menos 2GB de RAM y 32GB de almacenamiento.
5. Un cable USB-C de alta calidad para conectar el teléfono al ordenador. Si su ordenador no dispone de puerto USB-C, deberá utilizar un cable USB-C a USB-A. El cable USB debe conectarse directamente al puerto USB trasero del ordenador o al puerto USB del portátil y evitar utilizar los concentradores USB, como el del panel frontal de la caja de un ordenador de sobremesa.
6. No instalar desde una máquina virtual.
7. Usar un sistema operativo compatible con el método de instalación web. Asegúrese de que su sistema operativo está actualizado antes de empezar. Sistemas operativos compatibles:
	- Windows 10
	- Windows 11
	- macOS Monterey (12)
	- macOS Ventura (13)
	- macOS Sonoma (14)
	- Arch Linux
	- Debian 11 (diana)
	- Debian 12 (ratón de biblioteca)
	- Ubuntu 20.04 LTS
	- Ubuntu 22.04 LTS
	- Ubuntu 24.04 LTS
	- Linux Mint 20 (siga las instrucciones de Ubuntu 20.04 LTS)
	- Linux Mint 21 (siga las instrucciones de Ubuntu 22.04 LTS)
	- Linux Mint 22 (siga las instrucciones de Ubuntu 24.04 LTS)
	- Linux Mint Debian Edition 6 (siga las instrucciones de Debian 12)
	- ChromeOS
	- GrapheneOS
	- Android 12 con certificación Play Protect
	- Android 13 con certificación Play Protect
	- Android 14 con certificación Play Protect

8. Utilizar un navegador compatible. Asegúrese de que el navegador está actualizado y de no utilizar el modo incógnito antes de empezar. Navegadores compatibles:
    - Chromium (fuera de Ubuntu, ya que envían un paquete Snap roto sin WebUSB que funcione).
	- Vanadium (GrapheneOS).
	- Google Chrome.
	- Microsoft Edge.
	- Brave (con los **Escudos de Brave desactivados**, ya que limita el uso de almacenamiento a un valor bajo para evitar la huella digital de almacenamiento disponible).
	- Si usas Linux, debes evitar las versiones Flatpak y Snap de los navegadores, ya que se sabe que causan problemas durante el proceso de instalación.

9. En muchas distribuciones de Linux, los dispositivos USB requieren permisos de root para ser utilizados, a menos que se configuren reglas específicas en `udev`, que es el sistema de gestión de dispositivos de Linux. 	Para facilitar el uso de dispositivos Android sin necesidad de permisos root, podemos instalar los siguientes paquetes:
	- En Arch Linux, instala el paquete `android-udev`. 
	- En sistemas basados en Debian y Ubuntu, instala el paquete `android-sdk-platform-tools-common`.

### 4.2. Instalación {#Instalacion}

#### 1. Accedemos a la instalación web de GrapheneOS

Para ello accedemos a grapheneos.org, hacemos clic en **Install GrapheneOS** y luego en **WebUSB-based installer**.

<img  src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/1.png" alt="CapturaPagina1" width="100%"/>
<img  src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/2.png" alt="CapturaPagina2" width="100%"/>

Esto nos llevará a la página de instalación web de GrapheneOS junto con su guía oficial. Una vez allí, deberemos revisar la guía oficial por si acaso ésta a quedado desactualizada en algún punto. Luego deberemos bajar hasta la parte que se muestra en la siguiente captura, en donde nos aparecerán los cuatro botones necesarios para la instalación.

<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/3.png" alt="CapturaPagina3" width="100%"/>

#### 2. Desbloqueo de OEM y depuración USB

Primero debemos activar las opciones para desarrollador, para ello nos dirigimos a **Ajustes > Información del teléfono > Número de compilación** y pulsamos sobre el número de compilación 7 veces seguidas.

<div style="display: flex; gap: 20px;">
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/capturas/1.png" alt="CapturaMovil1" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/capturas/2.png" alt="CapturaMovil2" width="100%"/>
</div>

Luego nos dirigimos a **Sistema > Opciones para desarrolladores** y habilitamos el **desbloqueo de OEM** y la **depuración por USB**.

<div style="display: flex; gap: 20px;">
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/capturas/3.png" alt="CapturaMovil3" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/capturas/4.png" alt="CapturaMovil4" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/capturas/5.png" alt="CapturaMovil5" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/capturas/6.png" alt="CapturaMovil6" width="100%"/>
</div>

#### 3. Iniciar Fastboot

Una vez hecho el paso anterior, apagamos el teléfono. Para iniciar fastboot, debemos **encender el teléfono manteniendo pulsados los botones de encendido y bajar volumen** durante unos segundos, hasta que se inicie el cargador de arranque o bootloader. 

<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/fotos/1.jpg" alt="Foto1" width="60%"/>

Una vez hecho esto, debemos conectar nuestro dispositivo al ordenador con la página de la instalación web de GrapheneOS abierta. Se nos abrirá una ventana en el navegador que nos mostrará el nombre del dispositivo y nos preguntará si queremos conectarlo, daremos clic en conectar.

<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/4.png" alt="CapturaPagina4" width="100%"/>

#### 4. Desbloquear el bootloader

Haremos clic en el primer botón que dice **Unlock bootloader**.

<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/5.png" alt="CapturaPagina5" width="100%"/>

En el móvil nos aparecerá una opción que dice **Do not unlock the bootloader**, así que para desbloquear el bootloader, deberemos dar al botón de bajar volumen para cambiar a la opción que dice **Unlock the bootloader** y aceptamos presionando el botón de encendido. Nos devolverá a la pantalla anterior que dice **start**, solo que esta vez nos indicará que el bootloader está desbloqueado. Deberemos presionar de nuevo el botón de encendido para aceptar. Esto reiniciará el dispositivo y nos devolverá a la pantalla de instalación del sistema operativo que viene de fábrica, por lo que deberemos repetir el proceso del paso dos en el que desbloqueamos el OEM y la depuración USB y volveremos a entrar al modo fastboot apagando el dispositivo e iniciandolo de nuevo pulsando el botón de endido y el botón de volumen abajo al mismo tiempo durante unos segundos.

<div style="display: flex; gap: 20px;">
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/fotos/2.jpg" alt="FotoMovil2" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/fotos/3.jpg" alt="FotoMovil1" width="100%"/>
</div>

#### 5. Descargar e instalar GrapheneOS

Ahora debemos descargar GrapheneOS, para ello haremos clic en **Download release** y esperamos a que descargue por completo. Luego haremos clic en **Flash release** y de nuevo esperaremos a que termine la instalación.

<div style="display: flex; gap: 20px;">
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/6.png" alt="CapturaPagina6" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/7.png" alt="CapturaPagina7" width="100%"/>
</div>

#### 6. Bloquear el bootloader

Por último, una vez finalizada la instalación, deberemos volver a bloquear el bootloader. Para ello haremos clic en el botón de la página de instalación que dice **Lock bootloader**. En el móvil pulsaremos el botón de bajar volumen para seleccionar la opción **Lock the bootloader** y pulsamos el botón de encendido para aceptar. Esto bloqueará de nuevo el bootloader y nos devolverá a la pantalla anterior, donde nos indica que el bootloader está bloqueado. Para salir, simplemente volvemos a pulsar el botón de encendido donde dice **start** y reniciará el dispositivo cargando por primera vez GrapheneOS. 

<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/pagina/8.png" alt="CapturaPagina8" width="100%"/>
<div style="display: flex; gap: 20px;">
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/fotos/4.jpg" alt="FotoMovil4" width="100%"/>
	<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/fotos/1.jpg" alt="FotoMovil1" width="100%"/>
</div>

Antes de cargar GrapheneOS, nos aparecerá un aviso con un triangulo amarillo avisandonos de que el sistema operativo se ha modificado. No pasa nada, seguimos esperando y aparecerá el logo de Google, después nos cargará el sistema operativo y nos aparecerá el logo de GrapheneOS.

<img src="/assets/img/posts/2024-08-31-Que-es-GrapheOS-y-como-instalarlo/fotos/5.jpg" alt="FotoMovil5" width="60%"/>