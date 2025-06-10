 Clase Docker: ClamAV (Antivirus en contenedor)

 # 🐳 Clase Docker - Antivirus con ClamAV

En este ejercicio vas a aprender a usar Docker para levantar un contenedor que ejecuta **ClamAV**, un antivirus gratuito y de código abierto.  
Vamos a usarlo para escanear archivos locales desde un contenedor.

---

## ✅ Requisitos previos

- Tener [Docker Desktop](https://www.docker.com/products/docker-desktop/) instalado.
- Tener una terminal disponible (PowerShell, CMD o Git Bash).
- Conexión a internet (para descargar la imagen la primera vez).

---

## 📦 ¿Qué hace este proyecto?

Levanta un contenedor con el antivirus ClamAV y comparte una carpeta local llamada `files_to_scan` donde podés colocar archivos para escanear.

---

## 📁 Estructura del proyecto
clamav_docker/
├── docker-compose.yml # Configura el contenedor
├── files_to_scan/ # Carpeta para dejar los archivos a escanear
│ └── archivo_prueba.txt # Archivo de prueba (podés borrarlo o agregar más)

---

## 🚀 Paso a paso

### 1. Descargar o clonar este proyecto

Si tenés Git instalado:

```bash
git clone https://github.com/tu-usuario/clamav_docker.git
cd clamav_docker

2. Levantar el contenedor
Desde la terminal:
docker compose up -d

Esto hará lo siguiente:

Descargar la imagen mkodockx/docker-clamav

Crear el contenedor clamav

Montar la carpeta local files_to_scan como /scan dentro del contenedor


3. Colocar archivos para escanear
Copiá cualquier archivo que quieras analizar dentro del directorio:
clamav_docker/files_to_scan/
Ejemplo: documentos .doc, imágenes .jpg, comprimidos .zip, etc.

4. Escanear archivos
Ejecutá el siguiente comando para iniciar el escaneo:
docker exec -it clamav clamscan -r /scan

Esto le dice al contenedor que escanee de forma recursiva (-r) la carpeta /scan, que corresponde a files_to_scan en tu máquina.

5. Interpretar los resultados
Si todo está limpio, verás algo como:

/scan/archivo_prueba.txt: OK

----------- SCAN SUMMARY -----------
Known viruses: 8573264
Engine version: 0.103.3
Scanned directories: 1
Scanned files: 1
Infected files: 0
Data scanned: 0.00 MB
Time: 5.643 sec (0 m 5 s)

Si encuentra algo sospechoso, te mostrará:
/scan/archivo_malicioso.exe: Eicar-Test-Signature FOUND

🧹 Para apagar el contenedor
Cuando termines:
docker compose down

🔄 Actualizar base de virus (opcional)
La imagen actualiza automáticamente la base cuando se inicia.
Si querés forzar una actualización manual:
docker exec -it clamav freshclam


