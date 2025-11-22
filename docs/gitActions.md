# GitHub Actions – WorkFlow para generar documentación

Este documento describe el proceso de automatización mediante GitHub Actions para generar y publicar la documentación con MkDocs.

---

## 1. Objetivo del WorkFlow

El workflow se encarga de:

- Instalar dependencias necesarias para MkDocs.  
- Construir la documentación.  
- Publicarla en la rama `gh-pages`.  
- Ejecutarse automáticamente en cada **push** a la rama `main`.

---

## 2. Archivo del WorkFlow

Ruta: .github/workflows/CreacionDocumentacion.yml

Contenido:

```yaml
# -----------------------------------------------------------
# CONFIGURACIÓN DEL WORKFLOW
# -----------------------------------------------------------
name: Deploy MkDocs # Define el nombre de este flujo de trabajo (aparece en la pestaña 'Actions' de GitHub).

on:
  # Define el evento que dispara este flujo de trabajo.
  push:
    # Este workflow se ejecutará automáticamente cada vez que se haga un 'push' (subida)
    # de código al repositorio.
    branches:
      - main # Específicamente, solo se ejecuta si el push se realiza sobre la rama 'main'.

# -----------------------------------------------------------
# PERMISOS
# -----------------------------------------------------------
# Otorga permisos específicos al GITHUB_TOKEN que se usará en este workflow.
permissions:
  contents: write # Permite que el token pueda leer y escribir contenido (necesario para la rama gh-pages).
  pages: write    # Permite gestionar y escribir en la configuración de GitHub Pages.
  id-token: write # Permite solicitar tokens de OpenID Connect (necesario para algunas integraciones de seguridad).

# -----------------------------------------------------------
# DEFINICIÓN DEL TRABAJO (JOB)
# -----------------------------------------------------------
jobs:
  deploy: # Define un único trabajo llamado 'deploy'.
    runs-on: ubuntu-latest # Especifica que este trabajo se ejecutará en un servidor virtual con la última versión de Ubuntu.

    steps: # La secuencia de comandos o acciones a ejecutar en el servidor de Ubuntu.
    
    # -------------------------------------------------------
    # PASO 1: OBTENER EL CÓDIGO FUENTE
    # -------------------------------------------------------
    - name: Checkout Repo # Nombre descriptivo del paso.
      # Utiliza una acción oficial de GitHub para clonar el repositorio
      # completo en el entorno de trabajo del Runner.
      uses: actions/checkout@v3

    # -------------------------------------------------------
    # PASO 2: CONFIGURAR PYTHON
    # -------------------------------------------------------
    - name: Set up Python # Nombre descriptivo del paso.
      # Utiliza una acción oficial para configurar el entorno de Python.
      uses: actions/setup-python@v4
      with:
        python-version: '3.x' # Especifica que se debe usar la última versión de Python 3.

    # -------------------------------------------------------
    # PASO 3: INSTALAR DEPENDENCIAS
    # -------------------------------------------------------
    - name: Install dependencies # Nombre descriptivo del paso.
      # Comando que se ejecuta en la terminal de Ubuntu.
      # Instala el generador de documentación MkDocs (necesario para el siguiente paso).
      run: pip install mkdocs

    # -------------------------------------------------------
    # PASO 4: CONSTRUIR Y DESPLEGAR LA DOCUMENTACIÓN
    # -------------------------------------------------------
    - name: Deploy docs # Nombre descriptivo del paso.
      # Comando que se ejecuta en la terminal.
      # 1. 'mkdocs gh-deploy': Construye la documentación (generando los archivos HTML/CSS/JS).
      # 2. '--force': Sube esos archivos generados y fuerza su publicación en la rama 'gh-pages'.
      run: mkdocs gh-deploy --force
      # Configuración de variables de entorno específicas para este paso.
      env:
        # Pasa el Token de GitHub. MkDocs lo necesita para autenticarse y subir
        # los archivos a la rama 'gh-pages' del repositorio.
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
---

## Conclusión
La implementación del workflow con GitHub Actions ha permitido automatizar la generación y publicación de la documentación de manera eficiente y sin intervención manual. Cada vez que se realiza un push a la rama principal, el flujo de trabajo construye automáticamente la documentación con MkDocs y la publica en la rama gh-pages, garantizando que la web esté siempre actualizada.

Este ejercicio demuestra cómo la integración continua puede aplicarse a la documentación, no solo al código, reforzando las buenas prácticas DevSecOps. Además, permite comprender conceptos clave como la configuración de jobs, uso de acciones predefinidas, manejo de secretos y despliegue automático en entornos de producción estáticos.

En definitiva, el uso de GitHub Actions aporta eficiencia, consistencia y fiabilidad al proceso de documentación, convirtiéndose en una herramienta esencial dentro de un flujo de trabajo moderno de desarrollo seguro.
