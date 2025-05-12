# Proyecto de prueba de n8n con bot de Telegram
![Logo de n8n bot](logoprueban8nbot.png)

## Introducción

Este proyecto es de prueba, para aprender a usar la herramienta n8n, que consiste en la automatización de tareas.

Para la primera prueba he optado en realizar una automatización con Telegram, para ello se necesita crear un bot en Telegram, escribir a este bot para obtener los datos necesarios y crear el flujo en n8n.

El proyecto consta de varios archivos:

- [Flujo de n8n](n8npruebaBot.json)
- [Archivos en la carpeta proyecto](proyecto/)
  - [Archivo html](proyecto/index.html)
  - [Archivo css](proyecto/styles.css)

## Pasos

### Instalación n8n con Docker

Para la instalación de n8n con Docker, debemos en primer lugar descargar Docker desde su [página oficial](https://www.docker.com/products/docker-desktop/), además para cualquier duda en la misma web está la documentación oficial.

El comando necesario para la instalación de n8n es el siguiente, **Para usar este comando debemos abrir una terminal en Docker**:

```
docker run -it --rm \
  -p 5678:5678 \
  -e N8N_BASIC_AUTH_ACTIVE=true \
  -e N8N_BASIC_AUTH_USER=admin \
  -e N8N_BASIC_AUTH_PASSWORD=adminpassword \
  n8nio/n8n
```

Esto:

Publica el puerto 5678 (acceso vía navegador).

Activa la autenticación básica (admin / adminpassword).

Elimina el contenedor al cerrar (--rm).

Este método es bueno para probar, pero los datos se perderán al detener el contenedor.

Abre tu navegador y ve a:

http://localhost:5678

Inicia sesión con las credenciales que hayas definido (admin / adminpassword).

### Creación del bot de Telegram

1. Abre Telegram y busca el bot oficial llamado @BotFather.

2. Escribe /start y luego /newbot.

3. Te pedirá que le des un nombre y un usuario (único, terminado en bot, como miboton8nbot).

4. Te devolverá un token como este:
   
   ```
   123456789:ABCDefghIJKlmnoPQRstuvWXyz
   ```

**Guarda este token porque es el que vas a usar en n8n y en el archivo html**

Para empezar a usar el flujo, además de que son necesarias alguna configuración que detallaré más adelante, es necesario que escribas al bot para que obtenga los datos necesarios, estos datos que obtiene el bot puedes obtenerlos a través de la url https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates .

Cuando accedas a esta url verás los datos de esta forma:

```
{
  "message": {
    "chat": {
      "id": 123456789,
      "first_name": "TuNombre"
    },
    "text": "Lo que sea"
  }
}
```

### Creación de flujo

Una vez hecho lo demás debes importar el archivo del flujo, una vez importado es importante que en el nodo de Telegram accedas a la configuración y en el campo que pone credenciales añadas una nueva credencial con ell token del bot que has creado.

## Pruebas y producción

### Para pruebas

Teniendo todo hecho en n8n puedes hacer una prueba o activar el flujo para poder usarlo siempre que tengas n8n abierto.

Para hacer pruebas necesitas darle a test workflow que aparece en un botón naranja.

En el flujo debes acceder a la configuración del nodo **Webhook** y copiar la url que aparece en la opción de test.

En el archivo html en la línea 126 debes cambiar al url por la que has copiado y en la línea 33 en la constante botToken debes poner entre comillas el token del bot que has creado.

Tras esto puedes iniciar el archivo html y comprobar que funciona.

**Importante saber que cuando se manda un mensaje debes volver a darle a test workflow para volver a usarlo**

### Para producción

La otra opción es activar el flujo, esta opción se encuentra en la esquina superior derecha.

Una vez activo debemos ir a la configuración del WebHook y copiar la url que aparece en la opción de producción y cambiar la url que aparece en la línea 126 del archivo html.

En la línea 33 debes poner el token del bot que creaste para que funcione correctamente, si no lo has hecho ya

## Conclusión

Este proyecto me ha permitido entender cómo funciona n8n y su capacidad para automatizar flujos mediante integraciones con servicios externos, como Telegram. Al crear un bot, obtener el `chatId` y configurar un Webhook, he aprendido a conectar diferentes sistemas de forma sencilla y visual.

Además, trabajar con Docker ha facilitado la ejecución local de n8n sin necesidad de instalaciones complejas. Esta prueba básica sirve como base para automatizaciones más avanzadas y me ha ayudado a familiarizarme con conceptos clave como Webhooks, APIs y control de flujos.

El resultado es un flujo funcional que recibe mensajes desde una interfaz HTML y los envía a través de Telegram, demostrando la potencia y flexibilidad de n8n.
