# Resumen de Comandos Git

## Traer Todas las Ramas del Remoto

Para traer todas las ramas del remoto a tu repositorio local:

```bash
git fetch --all
```
Para ver todas las ramas (locales y remotas):
```bash
git branch -a
```

## Trabajar en una Rama Remota
Para trabajar en una rama remota en particular (por ejemplo, main):

```bash
git checkout -b main_local origin/main
```
Esto crea una nueva rama local (main_local) que sigue a la rama remota origin/main y cambia a esa nueva rama.

## Enviar Cambios Locales al Remoto
Después de hacer cambios locales en tu rama, puedes enviarlos al remoto:
```bash
git push origin main_local
```
Asegúrate de ajustar los nombres de las ramas según tu configuración específica.







