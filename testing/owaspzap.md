Aquí tienes una guía básica sobre cómo usar OWASP ZAP para realizar pruebas de seguridad en tus proyectos, incluyendo los comandos necesarios y la ejecución desde Docker.

---

# OWASP ZAP Security Testing Documentation

## Introduction

OWASP ZAP (Zed Attack Proxy) es una herramienta popular de seguridad que permite realizar pruebas de penetración y encontrar vulnerabilidades en aplicaciones web. Esta documentación proporciona una guía para configurar y usar OWASP ZAP para pruebas de seguridad en tus proyectos.

## Prerequisites

1. **Java Installed:** Ensure Java is installed on your system.
2. **Docker Installed:** Ensure Docker is installed on your system.
3. **OWASP ZAP Image:** Download the latest OWASP ZAP Docker image.

## Setting Up OWASP ZAP

### 1. Running OWASP ZAP with Docker

1. **Create a Bash Script for Running ZAP:**

   Create a file named `run-zap.sh` with the following content:

  ```bash
  #!/bin/bash

  # Mostrar mensaje de inicio
  echo "=== Security Testing Start ==="

  # Create the directories to store the reports
  mkdir -p zap-wrk
  mkdir -p zap-reports

  # Dar permisos de escritura a los directorios
  chmod 777 zap-wrk
  chmod 777 zap-reports

  # Ejecutar el comando y guardar la salida en SecurityTestReport.txt
  docker run --network host -v $(pwd)/zap-wrk:/zap/wrk -v $(pwd)/zap-reports:/zap/reports -t zaproxy/zap-stable zap-baseline.py -t http://<ipaddress>:8007 -r SecurityTestReport.html > SecurityTestReport.txt

  # Mostrar mensaje de fin
  echo "=== Security Testing End ==="

  # Añadir la salida del comando al archivo de reporte
  cat SecurityTestReport.txt

  # Move the report to the reports directory
  mv zap-wrk/SecurityTestReport.html TestReports/SecurityTestReport.html
  mv SecurityTestReport.txt TestReports/SecurityTestReport.txt

  # Delete the directories
  rm -rf zap-wrk
  rm -rf zap-reports
  ```

2. **Make the Script Executable:**

   ```bash
   chmod +x run-zap.sh
   ```

3. **Run the Script:**

   ```bash
   ./run-zap.sh
   ```

   This script will create necessary directories, set permissions, and run the OWASP ZAP Docker container to perform a baseline security test on your application, generating a report named `SecurityTestReport.html`.

## Command Line Options

OWASP ZAP supports various command line options to customize the behavior and configuration of your tests. Here are some commonly used options:

- `-version`: Reports the ZAP version.
- `-cmd`: Run inline (exits when command line options complete).
- `-daemon`: Starts ZAP in daemon mode, without a UI.
- `-config <kvpair>`: Overrides the specified key=value pair in the configuration file.
- `-configfile <path>`: Overrides the key=value pairs with those in the specified properties file.
- `-dir <dir>`: Uses the specified directory as the home directory, instead of the default one.
- `-installdir <dir>`: Overrides the code that detects where ZAP has been installed with the specified directory.
- `-h` or `-help`: Shows all available command line options.
- `-newsession <path>`: Creates a new session at the given location.
- `-session <path>`: Opens the given session after starting ZAP.
- `-lowmem`: Use the database instead of memory as much as possible (experimental).
- `-experimentaldb`: Use the experimental generic database code (experimental).
- `-nostdout`: Disables default logging through standard output.
- `-loglevel <level>`: Sets the log level, overriding values specified in the `log4j2.properties` file in the home directory.
- `-silent`: Ensures ZAP does not make any unsolicited requests.
- `-addoninstall <addOnId>`: Installs the add-on with the specified ID from the ZAP Marketplace.
- `-addoninstallall`: Installs all available add-ons from the ZAP Marketplace.
- `-addonuninstall <addOnId>`: Uninstalls the add-on with the specified ID.
- `-addonupdate`: Updates all changed add-ons from the ZAP Marketplace.
- `-addonlist`: Lists all installed add-ons.
- `-script <script>`: Runs the specified script if in command line/daemon mode, or just loads it.

## Example Commands

Here are some example commands to run OWASP ZAP with different configurations:

- **Run in Daemon Mode:**
  ```bash
  docker run -u zap -p 8080:8080 -d owasp/zap2docker-stable zap.sh -daemon
  ```

- **Start a New Session:**
  ```bash
  docker run -u zap -v $(pwd):/zap/wrk -d owasp/zap2docker-stable zap.sh -newsession /zap/wrk/newsession.session
  ```

- **Run a Specific Script:**
  ```bash
  docker run -u zap -v $(pwd):/zap/wrk -d owasp/zap2docker-stable zap.sh -script /zap/wrk/myscript.js
  ```

- **Install an Add-on:**
  ```bash
  docker run -u zap -d owasp/zap2docker-stable zap.sh -addoninstall <addOnId>
  ```
For more detailed information, refer to the [OWASP ZAP documentation](https://www.zaproxy.org/docs/).