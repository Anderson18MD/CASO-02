# Manual para Script de Instalación
#### Docker | GitLab | Opción SSL | Opción SSH
#### Facturador PRO4

### Descripción

Hemos elaborado un script para uso en instancias Linux con Ubuntu 18 o superior, este es un archivo que actualiza el sistema, instala las herramientas, sus dependencias y realiza todas las configuraciones previas, dejando el aplicativo listo para probar en menos de 20 minutos (siempre y cuando el dominio ya esté configurado hacia la instancia), su ejecución es muy sencilla.

### Requisitos previos
    1. Tener acceso a su servidor, <code>vps, máquina virtual o local via SSH</code>, en las instalaciones que realizamos para <code>AWS</code> o <code>Google Cloud</code>, hacemos entrega del usuario, la IP del servidor y la clave ssh que puede ser un archivo <code>.ppk</code> o <code>.pem</code>, recuerde almacenarlas en su equipo local.
    2. Tener instalado una versión de ssh en su máquina para conectarse de manera remota, puede utilizar putty, filezilla o una consola terminal. para mayor información sobre el acceso SSH visite los siguientes manuales: 

        * [guía para acceder con Putty (gestión de servidor)](https://docs.google.com/document/d/1PmQejvNd_dkXVm8DPUYlQTag0wvES46tMpxX3MPhkNY/edit#heading=h.nezjsyganf1w)

        * [guía para acceder con Winscp (gestión de archivos con aplicación de escritorio)](https://docs.google.com/document/d/1Xpri2102N4b5C-dG-FVPXW5ZWjEz5S4iDjpvl7Zwq2E/edit#heading=h.nezjsyganf1w)

       
    3. Si es posible configurar su dominio apuntando a su instancia para que al finalizar la instalación se encuentre disponible el aplicativo. Edite los récords <code>A</code> y <code>CNAME</code> donde <code>A</code> debe contener su IP y <code>CNAME</code> el valor * (asterisco) para que se tomen los subdominios registrados por la herramienta.

        ![](./img/1.png )

    4. En caso de contar con servicios instalados en su instancia como <code>mysql</code>, <code>apache</code> o <code>nginx</code>, debe detenerlos, ya que estos ocupan los puertos que pasarán a usar el aplicativo con los contenedores de Docker.

### Pasos

    1. Acceder a su instancia <code>vía SSH</code>.
    2. Loguearse como super usuario 
        ~~~
        ejecute sudo su
        ~~~
    3. Clonar el <code>snippet</code> de <code>gitlab</code> que contiene el <code>script</code>
        ~~~
        ```
        git clone https://gitlab.com/snippets/2079063.git script
        ```
        ~~~
    4. Ingrese a la carpeta clonada
        ~~~
        cd script
        ~~~
    5. Dar permisos de ejecución al <code>script</code>
        ~~~
        chmod +x install.sh
        ~~~
    6. El comando a utilizar para iniciar el despliegue requiere de un parámetro principalmente:
        ~~~
        ./install.sh [dominio]
        ~~~
        por ejemplo:
        ~~~
        ./install.sh facturador.pro
        ~~~
    7. Una vez ejecutado el comando iniciará el proceso de actualización del sistema, en el proceso se le solicitará:

        a. El usuario y contraseña de GitLab, para que se pueda descargar el proyecto en su instancia

        b. Si desea instalar  <code>SSL</code> gratuito, tenga en cuenta que este debe ser actualizado cada 90 días, el mensaje será el siguiente:

                * Instalar con <code>SSL</code>? (debe tener acceso al panel de su dominio para editar/agregar records TXT). si[s] no[n]

                    ¡. Deberá contestar con “s” o “n” para continuar

                    ¡¡. Si selecciona **SÍ**, deberá contestar las siguientes preguntas con “y”, son 2 en total, seguidamente se le ofrecerá un código que debe añadir en un récord tipo TXT en su dominio quedando como **_acme-challenge.example.com** o simplemente **_acme-challenge dependerá de su proveedor.**

                    ¡¡¡. Para continuar presione **enter**, luego deberá repetir las acciones para añadir un segundo código y habrá finalizado la configuración, si el proceso es exitoso la ejecución del <code>script</code> continuará.
        c. si desea obtener y gestionar actualizaciones automáticas, deberá disponer de su sesión de <code>gitlab</code> al momento
                * Configurar clave <code>SSH</code> para actualización automática? (requiere acceso a https://gitlab.com/profile/keys). si[s] no[n]

                    ¡. Deberá contestar con “s” o “n” para continuar

                    ¡¡. De seleccionar SÍ, al final del despliegue se le dará un extracto de texto que debe añadir a su configuración de <code>gitlab</code>
                        
                        ![](./img/2.png)
    8. Finalizado el <code>script</code> y dependiendo de sus selecciones anteriores, se le entregará varios datos que debe guardar, como:

        * Usuario administrador
        * Contraseña para usuario administrador
        * Url del proyecto
        * Ubicación del proyecto dentro del servidor
        * Clave <code>ssh</code> para añadir a <code>gitlab</code> (obligatorio para quienes seleccionan la instalación de <code>SSH</code>)

:::tip Enlaces de interés

* [Actualización de SSL](https://gitlab.com/b.mendoza/facturadorpro3/-/snippets/1955372)
* [Actualización mediante ejecución Script para instalaciones Docker](https://gitlab.com/b.mendoza/facturadorpro3/-/wikis/Script-Update-Docker)
* [Gestión de SSL independiente, no el que incorpora el Script](https://docs.google.com/document/d/1D87YJ9fq9yHiAauu6SGVugiC3m_i42DrFUt6VKYXuDI/edit#heading=h.5gkh9djmh9b)
* [Guía gitlab para la instalación, contiene el script usado en el presente manual](https://gitlab.com/b.mendoza/facturadorpro3/-/snippets/1971490), además posee los parámetros extras que pueden usarse en la ejecución del paso 6
:::


:::info
The docusaurus.config.js file supports:
- Configuring the site's metadata.
- Customizing the site's appearance.
- Managing plugins.
:::
