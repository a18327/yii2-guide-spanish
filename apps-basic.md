Plantilla de aplicación básica
==========================

La plantilla aplicación Yii básica es perfecta para proyectos pequeños o cuando solamente estas aprendiendo el framework.

La plantilla aplicación básica incluye cuatro páginas: una página de inicio, una página "acerca de", una página de contacto, y una página de inicio de sesión.
La página de contacto muestra un formulario de contacto que los usuarios pueden rellenar para enviar sus consultas al webmaster. Asumiendo que el sitio tiene acceso a un servidor de correo y que la dirección de correo del administrador se ha ingresado en el archivo de configuración, el formulario de contacto funcionara. Lo mismo ocurre con la página de inicio de sesión, el cual permite a los usuarios ser autenticados antes de acceder a contenido privilegiado.

Instalación
------------

La instalación del framework requiere [Composer](http://getcomposer.org/). Si todavía no tienes Composer en tu sistema, puedes descargarlo de
[http://getcomposer.org/](http://getcomposer.org/), o ejecuta el siguiente comando en Linux/Unix/MacOS:

~~~
curl -s http://getcomposer.org/installer | php
~~~

A continuación, puedes crear una aplicación Yii básica usando lo siguiente:

~~~
php composer.phar create-project --prefer-dist --stability=dev yiisoft/yii2-app-basic /path/to/yii-application
~~~

Ahora configura el directorio root de documentos de tu servidor web a /path/to/yii-application/web y deberías ser capaz de acceder a la aplicación usando la URL `http://localhost/`.

Estructura de directorios
-------------------

La aplicación básica no divide la aplicación en muchos directorios. Esta es la estructura básica:

- `assets` - archivos asset de la aplicación.
  - `AppAsset.php` - definición de los assets de la aplicación como CSS, JavaScript etc. Revisar [Managing assets](assets.md) para más detalles.
- `commands` - controladores de consola.
- `config` - configuración.
- `controllers` - controladores web.
- `models` - modelos de aplicación.
- `runtime` - registros (logs), estados (states), cache de archivos.
- `views` - plantillas de vistas.
- `web` - webroot.

El directorio root contiene un conjunto de archivos.

- `.gitignore` contiene una lista de los directorios ignorados por el sistema de versiones git. Si necesitas algo que nunca llega a tu repositorio de código fuente, agrégalo ahí.
- `codeception.yml` - configuración de Codeception.
- `composer.json` - Configuración de Composer descrito a detalle más abajo.
- `LICENSE.md` - Información de licencia. Pon la licencia de tu proyecto ahí. Especialmente cuando es open source.
- `README.md` - Información básica acerca de la instalación de la plantilla. Considera reemplazarlo con información acerca de tu proyecto y su instalación.
- `requirements.php` - Inspector de requerimientos de Yii.
- `yii` - Arranque de la aplicación de consola.
- `yii.bat` - Lo mismo pero para Windows.


### config

Este directorio contiene archivos de configuración:

- `console.php` - configuración de la aplicación de consola.
- `params.php` - parámetros comunes de la aplicación.
- `web.php` - configuración de la aplicación web.
- `web-test.php` - configuración de la aplicación web usada en la ejecución de tests de funcionalidad.

Todos estos archivos son arreglos (arrays) usados para configurar las propiedades correspondientes de la aplicación. Revisar la sección [Configuration](configuration.md) de la guía para más detalles.

### views

El directorio Views contiene las plantillas que tu aplicación está usando. En la plantilla básica están:

```
layouts
    main.php
site
    about.php
    contact.php
    error.php
    index.php
    login.php
```

`layouts` contiene layouts HTML p.e. el diseño (markup) de la página sin contar el contenido: tipo de documento (doctype), encabezado, menú principal, pie de página etc.
Por lo general los demás son vistas de controlador. Por convención estas se encuentran en subdirectorios que coinciden con el id (identificador) del controlador. Por lo cual las vistas de `SiteController` se encuentran en el subdirectorio `site`. Los nombres de las vistas normalmente coinciden con los nombres de las acciones (actions) del controlador.
Las vistas parciales se nombran a menudo comenzando con guion bajo.

### web

El directorio es un webroot. Normalmente un servidor web esta apuntado a él.

```
assets
css
index.php
index-test.php
```

`assets` contiene los archivos asset publicados, como CSS, JavaScript etc. El proceso de publicación es automático así que no necesitas hacer nada con este directorio que no sea asegurarse de que Yii tiene suficientes permisos para escribir en él.

`css` contiene archivos CSS y es útil para la CSS global que no va a ser comprimida o combinada por el assets manager.

`index.php` es el arranque principal y el punto de entrada central de la aplicación web. 

`index-test.php` es el punto de entrada para las pruebas de funcionalidad.

Configurando Composer
--------------------

Después de que la plantilla de la aplicación está instalada es una buena idea modificar el `composer.json` que viene por default el cual puede encontrarse en el directorio root:

```json
{
    "name": "yiisoft/yii2-app-basic",
    "description": "Yii 2 Basic Application Template",
    "keywords": ["yii", "framework", "basic", "application template"],
    "homepage": "http://www.yiiframework.com/",
    "type": "project",
    "license": "BSD-3-Clause",
    "support": {
        "issues": "https://github.com/yiisoft/yii2/issues?state=open",
        "forum": "http://www.yiiframework.com/forum/",
        "wiki": "http://www.yiiframework.com/wiki/",
        "irc": "irc://irc.freenode.net/yii",
        "source": "https://github.com/yiisoft/yii2"
    },
    "minimum-stability": "dev",
    "require": {
        "php": ">=5.4.0",
        "yiisoft/yii2": "*",
        "yiisoft/yii2-swiftmailer": "*",
        "yiisoft/yii2-bootstrap": "*",
        "yiisoft/yii2-debug": "*",
        "yiisoft/yii2-gii": "*"
    },
    "scripts": {
        "post-create-project-cmd": [
            "yii\\composer\\Installer::setPermission"
        ]
    },
    "extra": {
        "writable": [
            "runtime",
            "web/assets"
        ],
        "executable": [
            "yii"
        ]
    }
}
```

Primero modificamos la información básica. Cambia `name`, `description`, `keywords`, `homepage` and `support` para que coincida con tu proyecto.

Ahora la parte interesante. Puedes agregar más paquetes necesarios para tu aplicación a la sección `require`.
Todos esos paquetes vienen de [packagist.org](https://packagist.org/) así que siéntete libre de explorar el sitio web en busca de códigos útiles.

Después de que tu `composer.json` se ha modificado puedes ejecutar `php composer.phar update --prefer-dist`, espera a que los paquetes sean descargados e instalados y entonces solo úsalos. La autocarga (Autoloading) de las clases será manejada de forma automática.
