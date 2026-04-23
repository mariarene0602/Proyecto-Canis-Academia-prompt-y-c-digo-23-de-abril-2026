Para desarrollar proyectos de Flutter con Firebase de manera profesional, es indispensable contar con el **Firebase CLI** (Command Line Interface). Este permite automatizar configuraciones y gestionar servicios desde tu terminal.

Aquí tienes la guía paso a paso para preparar tu entorno de desarrollo en Windows.

---

## 1. Preparación: Instalación de Node.js y NPM
El Firebase CLI es un paquete de Node.js. Por lo tanto, necesitas instalar Node.js, el cual incluye automáticamente **npm** (Node Package Manager).

### ¿Cómo verificar si ya están instalados?
Abre una terminal (CMD, PowerShell o Terminal de VS Code) y escribe los siguientes comandos:

```bash
node -v
npm -v
```
* Si ves un número de versión (ej. `v20.x.x` y `10.x.x`), **ya los tienes instalados** y puedes saltar al paso 2.
* Si recibes un error como *"no se reconoce como un comando"*, procede con la instalación.

### Pasos para instalar Node.js y NPM en Windows
1.  Ve al sitio oficial: **[nodejs.org](https://nodejs.org/)**.
2.  Descarga la versión **LTS (Long Term Support)**; es la más estable y recomendada.
3.  Ejecuta el archivo `.msi` descargado y sigue el asistente de instalación (puedes dejar las opciones por defecto).
4.  **Importante:** Al finalizar, **reinicia tu computadora**. Esto asegura que las variables de entorno se actualicen y el sistema reconozca los nuevos comandos (`node` y `npm`).

---

## 2. Instalación de Firebase CLI
Una vez que `npm` esté funcionando, instalarás las herramientas de Firebase de manera **global** en tu sistema.

1.  Abre tu terminal y ejecuta:
    ```bash
    npm install -g firebase-tools
    ```
    * La bandera `-g` le indica a npm que instale la herramienta de forma **global**, para que puedas usar el comando `firebase` en cualquier carpeta de tu equipo.

---

## 3. Acceso a Firebase con tu Cuenta de Google
Para vincular tu terminal con tu cuenta de Google y gestionar tus proyectos, utiliza el siguiente comando:

1.  Ejecuta en tu terminal:
    ```bash
    firebase login
    ```
2.  El sistema abrirá automáticamente tu navegador web predeterminado.
3.  Selecciona tu cuenta de Google y haz clic en **"Permitir"** para conceder permisos a Firebase CLI.
4.  Una vez hecho esto, la terminal confirmará que has iniciado sesión exitosamente (`Success! Logged in as...`).

---

## 4. Uso de Firebase en tu proyecto Flutter
Ahora que el entorno está listo, el flujo de trabajo estándar para tu proyecto `crudscanisacademia` es:

### Instalar FlutterFire CLI
Es un complemento necesario para Flutter que genera automáticamente la configuración de Firebase:
```bash
dart pub global activate flutterfire_cli
```

### Configurar Firebase en tu proyecto
Navega a la carpeta de tu proyecto (`xfluttermaria0602/crudscanisacademia`) y ejecuta:
```bash
flutterfire configure
```
* Este comando detectará automáticamente tus proyectos de Firebase, te permitirá seleccionar las plataformas (Android, iOS, Web) y creará el archivo `firebase_options.dart` necesario para conectar tu App.

### Resumen de comandos útiles
| Comando | Función |
| :--- | :--- |
| `firebase login` | Inicia sesión con tu cuenta de Google. |
| `firebase logout` | Cierra la sesión actual de la terminal. |
| `flutterfire configure` | Vincula tu proyecto Flutter con la consola de Firebase. |
| `npm install -g firebase-tools` | Actualiza o instala la CLI de Firebase. |

---

### Recomendación de Oro para Estudiantes
Si llegas a tener problemas de permisos al instalar paquetes globales con `npm`, recuerda ejecutar tu terminal como **Administrador** (clic derecho sobre el icono de la terminal -> "Ejecutar como administrador"). Esto suele resolver los errores de acceso a las carpetas del sistema.

¿Te gustaría que te ayude a estructurar el archivo `main.dart` para inicializar Firebase utilizando el archivo `firebase_options.dart` que acabas de generar?
