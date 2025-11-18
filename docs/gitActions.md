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
name: Generar Documentación MkDocs

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout del repositorio
      uses: actions/checkout@v4

    - name: Configurar Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.x'

    - name: Instalar dependencias
      run: |
        pip install mkdocs mkdocs-material

    - name: Construir documentación
      run: mkdocs build

    - name: Desplegar en GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./site
```
---

## Conclusión
La implementación del workflow con GitHub Actions ha permitido automatizar la generación y publicación de la documentación de manera eficiente y sin intervención manual. Cada vez que se realiza un push a la rama principal, el flujo de trabajo construye automáticamente la documentación con MkDocs y la publica en la rama gh-pages, garantizando que la web esté siempre actualizada.

Este ejercicio demuestra cómo la integración continua puede aplicarse a la documentación, no solo al código, reforzando las buenas prácticas DevSecOps. Además, permite comprender conceptos clave como la configuración de jobs, uso de acciones predefinidas, manejo de secretos y despliegue automático en entornos de producción estáticos.

En definitiva, el uso de GitHub Actions aporta eficiencia, consistencia y fiabilidad al proceso de documentación, convirtiéndose en una herramienta esencial dentro de un flujo de trabajo moderno de desarrollo seguro.
