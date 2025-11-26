# Loquendo UNIX

## Motivación

Los vídeos Loquendo han sido importante para muchos usuarios, incluyendo a
la persona que escribe esto, ya sea porque les hace gracia, o porque fueron
parte de su infancia en cualquier forma, o sencillamente porque requieren
de estas voces para cualquier cosa.

Se puede usar Loquendo en sistemas UNIX ejecutando el Loquendo TTS Director
7 tranquilamente en Wine, y aquello funciona.. Pero por motivos
específicos, decidimos crear un servicio de API de Loquendo HTTP apoyándose
en SAPI5, que es lo que usan las voces Loquendo para funcionar.

## Requisitos

1. Dolorosamente, un servidor Windows, esto lo probamos en un Win10LTSC
   enterprise
2. Un python de 32-bit
El python de 32-bits es MENESTER, porque las voces de Loquendo son de
32bits y si usas python de 64-bits simplemente no las detectará.
3. El Loquendo TTS Director 7 instalado con sus voces.
4. pyttsx5


## API Web

**/getVoces**

Te dice las voces disponibles. Están hardcodeadas en el script así que ve
cambiandolo tú según las voces que tengas en el registro de windows:
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Speech\Voices\Tokens\LTTS7Jorge` por
ejemplo.

**/generar**

toma parámetros: voz y texto

La voz es una de las disponibles en `/getVoces` y el texto es lo que
quieras que lea el Loquendo.

## Programa

lokendo es un programa que lee la entrada estandar y escupe un wav. Tiene
bastantes parametros para ajustar el pitch, el sample rate y poner la
música de fondo de Loquendo.


## Ejemplos

`curl -X POST -F "texto=Hola culeros, les saluda el anticristo. hoy les traigo una crítica a los pinches otakus" -F "voz=Juan" https://loquendo.zsh.jp/generar | aplay`

`echo "Hola amigos de youtube, hoy les enseñaré a descargar g t a san andreas para pecé" | lokendo  --voz=Carlos | aplay`
