# Documentación del proceso con Git
## Creación del repositorio PPS-Unidad0-Tarea-Mariollorente

En esta sección se detallan los pasos seguidos para crear y configurar el repositorio de la tarea, utilizando Git y GitHub.

---

## 1. Creación del repositorio en GitHub

1. Accedí a la página principal de GitHub.
2. Seleccioné **New Repository**.
3. Introduje el nombre del repositorio: PPS-Unidad0-Tarea-Mariollorente
4. Seleccioné visibilidad **Public**.
5. Añadí un archivo `README.md`.
6. Creé el repositorio.

---

## 2. Clonación del repositorio en local

En el terminal cloné el repositorio usando:

```bash
git clone https://github.com/vjp-MarioLG/PPS-Unidad0-Tarea-Mariollorente.git
cd PPS-Unidad0-Tarea-Tu_nombre
```
---

## 3. Añadir al profesor como colaborador
1. Desde GitHub: Settings > Collaborators > Add collaborator: PPSvjp

---

## 4. Creación de la estructura base

Siguiendo la estructura recomendada:

```bash
mkdir -p docs
mkdir -p .github/workflows
mkdir -p calculator
touch docs/index.md docs/git.md docs/gitActions.md docs/gitPages.md docs/docker.md docs/conclusiones.md
touch calculator/__init__.py calculator/gui.py
touch mkdocs.yml requirements.txt

---

## 5. Primer commit y subida al repositorio

```bash
git add .
git commit -m "Estructura inicial del proyecto"
git push -u origin main
```
---

## 6.Otros comandos adicionales útiles

### Ver estado del repositorio:
```bash
git status
```
Muestra qué archivos han sido modificados, cuáles están en staging y cuáles no están siendo rastreados.

### Ver historial de commits:
```bash
git log
```
Muestra el historial completo de commits con autor, fecha y mensaje.

### Ver historial resumido:
```bash
git log --oneline
```
Muestra el historial en formato compacto, ideal para ver rápidamente la evolución del proyecto.

### Crear y cambiar de rama:
```bash
git checkout -b nombre-rama
```
Crea una nueva rama y cambia a ella inmediatamente.

### Actualizar repositorio local:
```bash
git pull
```
Descarga y fusiona los cambios del repositorio remoto a la rama actual.

---

## Conclusión

El dominio de estos comandos de Git es fundamental para cualquier desarrollador. Permiten:
- Mantener un historial ordenado y documentado del proyecto
- Trabajar de forma colaborativa y  eficientemente
- Revertir cambios cuando sea necesario
- Poder resolver problemas sin afectar el código principal
- Sincronizar trabajo 

La correcta gestión del repositorio demuestra profesionalismo y buenas prácticas de desarrollo de software.
