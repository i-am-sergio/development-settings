## Guía de Limpieza y Liberación de Espacio en Debian 13

Esta guía recopila en orden lógico todas las tareas de mantenimiento, desde la limpieza del sistema hasta la depuración de tu carpeta de usuario y herramientas de desarrollo.

---

### 1. Limpieza del Sistema y Gestor de Paquetes (`APT`)

Elimina instaladores `.deb` residuales, dependencias que ya no se usan y configuraciones de paquetes borrados a medias.

```bash
# Limpiar el caché de instaladores descargados por APT
sudo apt clean

# Eliminar paquetes descargados obsoletos que ya no están en repositorios
sudo apt autoclean

# Desinstalar dependencias huérfanas junto con sus archivos de configuración
sudo apt autoremove --purge -y

# Purgar configuraciones residuales de paquetes desinstalados previamente
dpkg -l | grep '^rc' | awk '{print $2}' | xargs -r sudo dpkg --purge

```

---

### 2. Reducción de Registros del Sistema (`systemd-journald`)

Los registros de eventos del kernel y servicios crecen indefinidamente si no se les fija un tope.

```bash
# Consultar cuánto espacio consumen los logs actuales
journalctl --disk-usage

# Conservar únicamente los registros de los últimos 3 días
sudo journalctl --vacuum-time=3d

# O limitar el tamaño acumulado a un máximo de 100 MB
sudo journalctl --vacuum-size=100M

```

---

### 3. Limpieza de Archivos Temporales del Sistema

```bash
# Vaciar directorios temporales globales
sudo rm -rf /tmp/* /var/tmp/*

```

---

### 4. Limpieza Inmediata de Cachés de Usuario

Estos directorios contienen datos prescindibles que los navegadores, el escritorio y las herramientas regeneran de forma automática.

```bash
# Caché general de usuario (navegadores, miniaturas, Electron)
rm -rf ~/.cache/*

# Caché de miniaturas de imágenes y videos
rm -rf ~/.cache/thumbnails/*

# Papelera de reciclaje
rm -rf ~/.local/share/Trash/*

```

---

### 5. Limpieza de Herramientas de Desarrollo

Comandos específicos para liberar espacio acumulado por gestores de paquetes y entornos de programación:

* **Node.js / NPM / Bun:**
```bash
# Forzar el vaciado del caché de npm
npm cache clean --force
rm -rf ~/.npm/*

# Vaciar el caché del gestor de paquetes Bun
bun pm cache rm

```


* **Java / Maven:**
```bash
# Borrar dependencias .jar descargadas en compilaciones antiguas
rm -rf ~/.m2/repository/*

```


* **SonarQube / SonarLint:**
```bash
# Borrar cachés locales del analizador de código
rm -rf ~/.sonar/cache/* ~/.sonarlint/*

```


* **Docker / Podman (si se usan o usaron contenedores):**
```bash
# Elimina contenedores parados, redes sin uso, imágenes huérfanas y volúmenes anónimos
sudo docker system prune -a --volumes

```


* **Flatpak (en caso de tener aplicaciones de este tipo instaladas):**
```bash
# Elimina runtimes y librerías que ya ninguna aplicación usa
flatpak uninstall --unused

```



---

### 6. Diagnóstico y Revisión Manual

Para auditar periódicamente en qué directorios se está acumulando el peso:

* **Ver el estado de las particiones montadas:**
```bash
df -h

```


* **Identificar las 10 carpetas más pesadas en la raíz del sistema:**
```bash
sudo du -h --max-depth=1 -x / | sort -hr | head -n 10

```


* **Identificar qué carpetas ocupan más espacio en tu usuario (`/home`):**
```bash
du -h --max-depth=1 ~ | sort -hr | head -n 15

```


* **Inspeccionar qué aplicaciones llenan la carpeta de configuración (`~/.config`):**
```bash
du -h --max-depth=1 ~/.config | sort -hr | head -n 10

```


* **Encontrar carpetas `node_modules` pesadas dentro de `~/Documents`:**
```bash
find ~/Documents -name "node_modules" -type d -prune -exec du -sh {} + | sort -hr | head -n 10

```