# AndroidCLIWorkshop

Repositorio de apoyo para el taller **Android CLI de cero a flujos reales**.

El objetivo del workshop es aprender a usar `android`, una herramienta de linea de comandos para crear proyectos Android, gestionar SDKs, consultar documentacion oficial, manejar emuladores, desplegar apps, inspeccionar UI, capturar pantallas y automatizar pruebas o flujos de validacion.

La idea no es memorizar comandos sueltos, sino entender como combinarlos con un asistente como Codex para trabajar mas rapido y con mas evidencias: crear una app, revisar el entorno, actualizar SDKs, buscar documentacion oficial, lanzar un emulador, probar una feature, inspeccionar una pantalla y preparar un resumen listo para PR.

## Que vas a aprender

- Crear proyectos Android desde templates.
- Instalar, listar, actualizar o eliminar paquetes del Android SDK.
- Consultar documentacion oficial Android desde terminal.
- Crear, arrancar, detener y eliminar emuladores.
- Desplegar APKs en dispositivos o emuladores.
- Capturar pantallas como evidencia.
- Inspeccionar el arbol de layout de una app.
- Analizar la estructura de un proyecto para localizar artefactos como APKs.
- Automatizar flujos de validacion combinando build, run, layout y screenshots.

## Requisitos previos

Antes de empezar, valida que Android CLI y el entorno Android estan disponibles:

```bash
android --version
android info
android sdk list
android emulator list
```

Si alguno de estos comandos falla, la primera practica del taller sera diagnosticar el entorno antes de crear proyectos.

## Mapa rapido de comandos

```text
android
  create      Crear proyectos
  sdk         Gestionar SDK y paquetes
  docs        Buscar y leer documentacion Android
  emulator   Gestionar emuladores
  run         Desplegar y ejecutar APKs
  screen      Capturar o resolver elementos visuales
  layout      Inspeccionar arbol de UI
  describe    Analizar estructura del proyecto
  info        Ver informacion del entorno
  init        Inicializar entorno de Android CLI
  skills      Gestionar skills relacionadas
  update      Actualizar Android CLI
```

## Flujo base del workshop

### 1. Diagnosticar el entorno

```bash
android --version
android info
android sdk list
android emulator list
```

Resultado esperado:

- Sabes donde esta el SDK.
- Sabes que paquetes tienes instalados.
- Sabes si tienes algun emulador disponible.

Prompt sugerido:

```text
Revisa mi entorno Android CLI ejecutando los comandos necesarios. Quiero saber si puedo crear, compilar y ejecutar una app Android. Resume problemas, riesgos y siguientes pasos concretos.
```

### 2. Crear un proyecto desde cero

```bash
android create --list
android create empty-activity --name="Workshop App" --minSdk=24 --output=./workshop-app
android describe --project_dir=./workshop-app
```

Resultado esperado:

- Proyecto Android creado.
- Estructura inicial entendida.
- Modulos y artefactos identificados.

Prompt sugerido:

```text
Crea un proyecto Android nuevo llamado "Workshop App" con minSdk 24 usando Android CLI. Luego inspecciona la estructura generada, explicame los directorios importantes y dime como compilarlo y ejecutarlo.
```

### 3. Consultar documentacion oficial

```bash
android docs search "Jetpack Compose state hoisting"
android docs search "Android permissions camera"
android docs search "WorkManager periodic work"
```

Resultado esperado:

- Encuentras guias oficiales.
- Extraes recomendaciones aplicables al proyecto.
- Evitas depender de snippets desactualizados.

Prompt sugerido:

```text
Busca documentacion oficial con Android CLI sobre Jetpack Compose state hoisting. Resume las recomendaciones clave y aplicalas a una pantalla sencilla de contador en mi proyecto.
```

### 4. Gestionar SDKs

```bash
android sdk list --all
android sdk install platforms/android-35
android sdk install "build-tools;35.0.0"
android sdk update
```

Resultado esperado:

- SDK actualizado.
- Paquetes necesarios disponibles.
- Menos errores por plataformas faltantes.

### 5. Crear y arrancar un emulador

```bash
android emulator list
android emulator create
android emulator start <nombre-avd>
```

Resultado esperado:

- Emulador creado o seleccionado.
- Emulador arrancado y listo.
- App preparada para ejecutarse.

### 6. Ejecutar la app

```bash
android describe --project_dir=./workshop-app
android run --apks=./workshop-app/app/build/outputs/apk/debug/app-debug.apk
```

Tambien puedes ejecutar una actividad concreta:

```bash
android run --activity=.MainActivity --type=ACTIVITY --apks=./app/build/outputs/apk/debug/app-debug.apk
```

### 7. Capturar evidencias

```bash
mkdir -p evidencias
android screen capture > ./evidencias/home.png
android layout --output=./evidencias/layout-home.json --pretty
```

Resultado esperado:

- Captura PNG guardada.
- Layout JSON guardado.
- Evidencia lista para revision, bug report o PR.

### 8. Inspeccionar UI

```bash
android layout --pretty
android layout --diff --pretty
android layout --device=<serial> --pretty
```

Con esto puedes comprobar si existe un texto, detectar botones invisibles o mal jerarquizados y comparar cambios tras interactuar con la app.

## Practicas incluidas

1. Diagnostico inicial del entorno.
2. Creacion de un proyecto Android desde cero.
3. Consulta de documentacion oficial para implementar una feature.
4. Gestion de SDKs y dependencias del entorno.
5. Creacion y arranque de un emulador.
6. Compilacion, despliegue y ejecucion de la app.
7. Captura de pantalla como evidencia.
8. Inspeccion de UI con layout JSON.
9. Test automatico asistido de una feature.
10. Debug de una regresion visual.

## Mini proyecto final

Construir una app simple de tareas con:

- Pantalla home con titulo y lista vacia.
- Boton para crear tarea.
- Formulario con campo de texto.
- Validacion si el texto esta vacio.
- Tarea visible al guardar.
- Capturas de home, formulario, error y tarea creada.
- Layout JSON de cada estado importante.

Prompt completo:

```text
Crea o usa un proyecto Android existente para construir una mini app de tareas. Primero consulta documentacion oficial Android CLI sobre la tecnologia UI que use el proyecto. Implementa una pantalla home con lista vacia, un boton para crear tarea, un formulario con validacion de texto obligatorio y retorno a home mostrando la tarea creada. Luego arranca un emulador, compila, instala la app, ejecuta un smoke test del flujo completo, inspecciona layout en cada estado y guarda capturas como evidencias. Al final dame resumen de cambios, comandos usados, tests realizados y riesgos pendientes.
```

## Checklist de cierre

Antes de dar una practica por terminada:

- `android info` no muestra problemas criticos.
- SDK requerido instalado.
- Existe emulador o dispositivo conectado.
- Proyecto puede describirse con `android describe`.
- APK generado localizado.
- App instalada con `android run`.
- Pantalla validada con `android layout`.
- Captura guardada con `android screen capture > archivo.png`.
- Evidencias organizadas.
- Prompt final documentado para repetir el flujo.

## Prompts reutilizables

Diagnostico:

```text
Audita mi entorno Android CLI. Comprueba version, SDK, paquetes instalados y emuladores disponibles. Si falta algo, dame comandos concretos para resolverlo y explica brevemente por que hace falta.
```

Documentacion:

```text
Busca documentacion oficial Android sobre "<tema>" usando Android CLI. Resume las recomendaciones actuales, dame ejemplos aplicables y dime que cambios harias en este proyecto.
```

Ejecucion:

```text
Compila y ejecuta esta app Android en el emulador activo. Usa Android CLI para localizar el APK generado y desplegarlo. Si falla, diagnostica si el problema es de build, APK, dispositivo o actividad.
```

Evidencias:

```text
Genera evidencias de la pantalla actual: captura PNG, layout JSON pretty y un resumen corto de lo que se ve y que elementos interactivos existen.
```

PR:

```text
Antes de abrir PR, ejecuta una verificacion completa: entorno, build, emulador, instalacion, smoke test de UI, captura de pantalla y layout JSON. Resume riesgos y tests ejecutados.
```
