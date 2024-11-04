---
title: ¿Qué es la criptografía?
description: En la era de la digitalización, la necesidad por salvaguardar la privacidad de nuestra información y nuestras comunicaciones, ha hecho de la criptografía una herramienta fundamental de ciberseguridad para proteger nuestra información confidencial de hackers, gobiernos y ciberdelincuentes. 
date: 2024-11-04 21:00:00 +0200
categories: [Criptografia]
tags: [Criptografia, Privacidad, Principiante]
pin: false
mermaid: true
image:
  path: /assets/img/posts/2024-11-04-Que-es-la-criptografia/cryptography.jpg
  alt: Designed by Freepik
---
## Índice

1. [Introducción](#Introduccion)
2. [¿Qué es la criptografía?](#Que-es-la-criptografia)
3. [Tipos de cifrado](#Tipos-de-cifrado)
    - [Criptografía simétrica](#Criptografia-simetrica)
    - [Criptografía asimétrica](#Criptografia-asimetrica)
    - [Criptografía híbrida](#Criptografia-hibrida)
4. [Funciones hash](#Funciones-hash)
5. [Firma digital](#Firma-digital)
6. [Certificado digital](#Certificado-digital)

## Introducción {#Introduccion}

En la era de la digitalización, la necesidad por salvaguardar la privacidad de nuestra información y nuestras comunicaciones, ha hecho de la criptografía una herramienta fundamental de ciberseguridad para proteger nuestra información confidencial de hackers, gobiernos y ciberdelincuentes. 

Derivada de la palabra griega "kryptos", que significa "oculto" y "graphé", que significa "grafo" o "escritura", "criptografía" se traduce literalmente como "escritura oculta".

La criptografía puede emplearse para ocultar cualquier forma de información digital, como texto, imágenes, vídeo o audio, entre otros. En la actualidad, la criptografía se utiliza en una amplia variedad de aplicaciones, como el cifrado de bases de datos, teléfonos móviles, ordenadores, servidores, comunicaciones en Internet, firmas digitales, criptomonedas, entre otros.

En este artículo, exploraremos qué es la criptografía, sus diferentes tipos y algoritmos más relevantes, así como sus diversas aplicaciones en el mundo actual.

## 1. ¿Qué es la criptografía? {#Que-es-la-criptografia}

La criptografía es el ámbito de la criptología que se centra en el diseño y aplicación de algoritmos matemáticos utilizados para proteger la información. Dichos algoritmos alteran la representación lingüística original de los mensajes, conocido como texto plano, con el objetivo de hacerlos incomprensibles a terceros que no posean la clave de descifrado. La criptología por su parte, es un campo más amplio que incluye a la criptografía como una de sus disciplinas, entre otras como el criptoanálisis, la esteganografía o el estegoanálisis. La criptografía tiene cuatro objetivos principales:

1. **Confidencialidad:** Implica proteger la información para que solo los usuarios autorizados que posean la clave de descifrado puedan acceder a ella.

2. **Integridad:** Consiste en asegurar que los datos no son alterados ni modificados de forma no  autorizada durante su transmisión o almacenamiento. Para lograrlo, se utilizan técnicas como la función hash, que genera un resumen o "hash" único para un conjunto de datos. Si la información se altera en cualquier forma, el hash resultante será diferente, lo que permite detectar cualquier cambio no autorizado.

3. **Autenticación:** Se refiere a la capacidad de verificar la identidad de un individuo u organización, asegurando que sean quienes dicen ser. La criptografía proporciona mecanismos para la autenticación, como las firmas digitales y los certificados digitales, que utilizan claves criptográficas asimétricas para verificar la integridad y el origen de un mensaje o documento.

4. **No repudio:** El objetivo es evitar que una entidad pueda negar la autoría de un mensaje o acción realizada. Esto se puede lograr mediante el uso de firmas digitales. Al utilizar una clave privada para firmar un mensaje, se puede demostrar de manera irrefutable que el remitente es quien dice ser, lo que evita que pueda negar su participación.

## 2. Tipos de cifrado {#Tipos-de-cifrado}

Existen tres tipos de criptografía ampliamente utilizados en seguridad informática: la criptografía simétrica, la criptografía asimétrica o de clave pública y la criptografía híbrida, que combina las características de las dos anteriores, solucionando así las limitaciones de cada una.

### 2.1. Criptografía simétrica {#Criptografia-simetrica}

La criptografía simétrica se basa en el uso de una única clave para cifrar y descifrar la información. En caso de que dicha información quiera ser compartida, deberemos compartir la clave con el receptor. Esta clave debe compartirse de manera segura, de lo contrario, la clave puede ser interceptada y nuestra información quedaría expuesta a terceros no autorizados. Debido a esto, este tipo de cifrado suele emplearse en combinación con la criptografía asimétrica o de clave pública, para establecer un canal de comunicación seguro para compartir la clave. O para cifrar información a la que solo nosotros tenemos acceso y no deseamos compartir, como el cifrado de discos duros, particiones, archivos, unidades externas como USBs, etc. 

![Criptografia-Simetrica](/assets/img/posts/2024-11-04-Que-es-la-criptografia/esquema-criptografia-simetrica.png)
_Creado por <strong>José Rodríguez</strong> usando <strong>diagrams.net</strong>_

Actualmente el algoritmo más utilizado en criptografía simétrica es Rijndael, desarrollado en Bélgica en 1997 por los criptógrafos Vincent Rijmen y Joan Daemen. En 2001, tras ganar el concurso organizado por el NIST (Instituto Nacional de Estándares y Tecnología), Rijndael fue apodtado como el nuevo estándar de cifrado por el gobierno de los Estados Unidos, convirtiéndose así en el AES (Advanced Encryption Standard) y reemplazando al anterior estándar, DES (Data Encription Standard), desarrollado entre 1973 y 1974 por IBM y adoptado como estándar en los Estados Unidos en 1976. También existen otros algoritmos utilizados en la actualidad como Serpent, Twofish o Camellia, entre otros.

### 2.2. Criptografía asimétrica {#Criptografia-asimetrica}

Por otro lado, la criptografía asimétrica resuelve el problema anterior del intercambio de claves mediante el uso de un par de claves vinculadas entre sí: una clave privada y una clave pública derivada de la primera. La clave pública puede compartirse libremente, ya que se utiliza para cifrar la información destinada al titular de la clave privada. Es decir, el emisor cifra el mensaje utilizando la clave pública del receptor antes de enviarlo. El receptor, por su parte,  posee la clave privada necesaria para descifrar la información que ha sido cifrada previamente con la clave pública correspondiente. Esta clave privada debe mantenerse en secreto y no compartirse con nadie, ya que se emplea tanto para descifrar la información cifrada con la clave pública, como para firmar digitalmente. Cualquiera que obtenga esta clave, tendría acceso a la información del titular de la clave y podría hacerse pasar por el. 

Este enfoque, soluciona el problema del intercambio de claves que tiene la criptografía simétrica, permitiendo una comunicación segura sin necesidad de compartir la clave privada. En este tipo de cifrado, existen diversos tipos de algoritmos utilizados, como el RSA, desarrollado en 1977 y llamado así por las siglas de los apellidos de sus creadores, Ron Rivest, Adi Shamir y Leonard Adleman. DSA (Digital Signature Algorithm) desarrollado en 1991 por el NIST como parte del estándar FIPS 186. O algoritmos basados en matemáticas de curvas elipticas, ECC (Elliptic Curve Cryptography), como ECDSA (Elliptic Curve Digital Signature Algorithm), utilizado en criptomonedas como Bitcoin para firmas digitales o ECDH (Elliptic Curve Diffie-Hellman), utilizado para el intercambio seguro de claves,  entre otros.

![Criptografia-Asimetrica](/assets/img/posts/2024-11-04-Que-es-la-criptografia/esquema-criptografia-asimetrica.png)
_Creado por <strong>José Rodríguez</strong> usando <strong>diagrams.net</strong>_

### 2.3. Criptografía híbrida {#Criptografia-hibrida}

La criptografía híbrida, aborda las limitaciones de la criptografía simétrica y la criptografía asimétrica combinandolas para aprovechar las ventajas de cada una.

La criptografía simétrica es rápida y eficiente para cifrar y descifrar grandes cantidades de información. Sin embargo, su mayor limitación es el intercambio de claves, ya que si se desea compartir la información cifrada, es necesario compartir la clave de descifrado con el receptor, lo que puede comprometer la confidencialidad de la comunicación si la clave es interceptada. 

Por otro lado, la criptografía asimétrica o de clave pública, resuelve este problema ya que no requiere compartir la clave privada. Sin embargo, es más ineficiente y lenta en comparación con el cifrado simétrico, especialmente al tratar con grandes cantidades de información.

Aquí es donde entra en juego la criptografía híbrida, combinando la seguridad del intercambio de claves de la criptografía asimétrica y la eficiencia del cifrado de datos de la criptografía simétrica, asegurando así comunicaciones seguras y rápidas en una amplia gama de aplicaciones. Es importante entender que  la criptografía híbrida no se basa en algoritmos específicos, sino que es un método basado en la combinación de algoritmos de criptografía asimétrica para establecer un canal de comunicación seguro y generar una clave compartida, que luego se utilizará para el cifrado eficiente de las comunicaciones empleando un algoritmo de cifrado simétrico.

Este proceso puede realizarse manualmente o de forma automática. Por ejemplo, en una comunicación por correo electrónico, el emisor puede generar una clave simétrica para cifrar un archivo y luego cifrar esta clave simétrica con la clave pública del receptor antes de enviarla. El receptor descifra la clave simétrica con su clave privada y luego utiliza esta clave para descifrar el archivo recibido.

![Criptografia-Hibrida](/assets/img/posts/2024-11-04-Que-es-la-criptografia/esquema-criptografia-hibrida.png)
_Creado por <strong>José Rodríguez</strong> usando <strong>diagrams.net</strong>_

Automáticamente, este proceso se implementa en programas y protocolos como TLS (Transport Layer Security), SSH (Secure Shell) o Tor (The Onion Router), entre otros. Un ejemplo clave es el intercambio de claves de Diffie-Hellman, que utiliza criptografía asimétrica (como DH o ECDH - Elliptic Curve Diffie-Hellman) para generar y compartir de forma segura una clave común. Esta clave común se emplea luego para cifrar la información con un algoritmo de criptografía simétrica como AES (Advanced Encryption Standard).

## 3. Funciones hash {#Funciones-hash}

Una función hash es un algoritmo matemático que transforma una entrada de datos de longitud variable en una salida de longitud fija, comúnmente conocida como valor hash o resumen. Este proceso se realiza de tal forma que cualquier cambio en la entrada, por mínimo que sea, produce un cambio en la salida significativamente diferente al anterior.

Las funciones hash se utilizan en una gran variedad de aplicaciones en informática, como verificar que los datos de un archivo no hayan sido alterados, para almacenar contraseñas cifradas, de forma que cuando un usuario intenta autenticarse, el sistema compara el hash de la contraseña proporcionada con el hash almacenado, o para firmas digitales, ya que generalmente la firma se aplica sobre el hash del mensaje o archivo en lugar de sobre el mensaje o archivo completo. Entre otras aplicaciones.

Los algoritmos más utilizados en la actualidad son MD5 (Message Digest Algorithm 5), desarrollado en 1991 por el criptógrafo y profesor del MIT Ronald Rivest, como reemplazo del algoritmo MD4. Y SHA-2, que consiste en un conjunto de funciones hash que consta de cuatro variantes principales especificados por su longitud en bits: SHA-224, SHA-256, SHA-384 y SHA-512. Estas funciones fueron diseñadas por la Agencia de Seguridad Nacional (NSA) como reemplazo de SHA-1, incluyendo un número significativo de mejoras respecto a su predecesor, y publicadas en 2001 por el Instituto Nacional de Estándares y Tecnología (NIST) como un Estándar Federal de Procesamiento de Información (FIPS), con la publicación de FIPS PUB 180-2.

## 4. Firma digital {#Firma-digital}

Las firmas digitales son un mecanismo criptográfico utilizado para validar la autenticidad e integridad de un mensaje, software o documento digital. Una firma digital asegura que la información no ha sido alterada y que proviene de un remitente legítimo. 

El proceso de creación de una firma digital, comienza con la generación de un hash del mensaje o archivo que se desea firmar. Posteriormente, el hash resultante se cifra usando la clave privada del firmante, creando así la firma digital. La firma digital se adjunta luego al mensaje o documento original.

Para verificar la firma digital, el receptor genera el hash del mensaje recibido usando la misma función hash que el remitente. Luego, la firma digital se descifra utilizando la clave pública del firmante, verificando de esta forma la autenticidad del mensaje. Si el hash desencriptado coincide con el hash generado a partir del mensaje recibido, se confirma que la firma es válida y que el mensaje no ha sido alterado.

Consiste en cifrar el hash resultante del archivo o mensaje con la clave privada del firmante, de tal forma que cualquiera que tenga la clave pública correspondiente, puede descifrar el hash y por tanto verificar la autenticidad del mensaje.

![Firma-digital](/assets/img/posts/2024-11-04-Que-es-la-criptografia/esquema-firma-digital.png)
_Creado por <strong>José Rodríguez</strong> usando <strong>diagrams.net</strong>_

En la práctica, las firmas digitales se utilizan en una amplia variedad de aplicaciones, como en correos electrónicos, transacciones financieras en línea, la firma de documentos legales o la distribución de software, entre otros.

## 5. Certificado digital {#Certificado-digital}

Un certificado digital, es la firma digital de una clave pública vinculada con la identidad de una persona, organización o dispositivo, por parte de una entidad de certificación (AC o CA, por sus siglas en inglés). Su propósito principal, es proporcionar un medio seguro para autenticar la identidad del dueño de la clave.

Los certificados digitales son emitidos por entidades de certificación (AC o CA, por sus siglas en inglés), que son organizaciones de confianza públicas o privadas, encargadas de verificar la identidad del solicitante antes de emitir el certificado. La AC primero verifica la identidad del solicitante y una vez que ha confirmado la identidad, firma digitalmente la clave pública del solicitante, creando así el certificado digital. Este certificado incluye la clave pública del solicitante, su identidad, la fecha de expiración (si la tiene) y la firma digital de la AC. 

Un certificado digital puede utilizarse para la autenticación de usuarios, organizaciones o dispositivos en línea, la validación de firmas digitales de documentos y transacciones, el cifrado de correos electrónicos, la identificación en servicios gubernamentales, o para validar la autenticidad e identidad de un sitio web y establecer conexiones seguras (HTTPS), entre otros.

