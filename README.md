# Solución: Cómo conectarse a los servidores de Mortal Kombat 11 (Steam / PC)

# Fix: Mortal Kombat 11 Server Connection Error (Steam / PC)

## El Problema | Issue
Al intentar jugar Mortal Kombat 11 en Steam, el juego no logra conectarse a los servidores de WB Games.


**Síntomas**
* Mensaje de error al intentar acceder a las funciones en línea. 
* Verificar la integridad de los archivos en Steam no soluciona el problema.
* Agregar exclusiones en el Firewall o Windows Defender no tiene efecto.
* Borrar la carpeta `AppData` del juego tampoco funciona.

## La Causa
El error ocurre porque Windows no descargó o no tiene actualizados los **Certificados Raíz de Seguridad (Root Certificates)** necesarios para establecer una conexión segura con los servidores de Warner Bros. Al no tener este certificado, el servidor rechaza la conexión de tu equipo.

## La Solución (Vía PowerShell)
Para solucionarlo, necesitamos forzar a Windows a descargar e instalar los certificados más recientes directamente desde Windows Update mediante la consola.

### Pasos:
1. Haz clic en el menú Inicio, escribe `PowerShell`.
2. **Importante:** Haz clic derecho sobre Windows PowerShell y selecciona **Ejecutar como administrador**.
3. Copia y pega los siguientes comandos uno por uno, presionando `Enter` después de cada línea:

```powershell
# 1. Crear una carpeta temporal para los certificados
md $Env:TEMP\certs

# 2. Navegar a la carpeta temporal
cd $Env:TEMP\certs

# 3. Descargar los certificados raíz actualizados desde Windows Update
CertUtil -generateSSTFromWU $Env:TEMP\certs\RootStore.sst

# 4. Importar el certificado a la máquina local (Instalación directa)
Import-Certificate -FilePath "$Env:TEMP\certs\RootStore.sst" -CertStoreLocation Cert:\LocalMachine\Root
```
## Issue
Trying to play Mortal Kombat 11 in steam, the game cannot connect to WB Games servers.

**Symptoms**
* Error message acceding online functions
* verifying the integrity if the files in Steam doesn't solve the issue
* Adding exclusions to the Firewall or Windows Defender hasn't effect.
* Deleting `AppData` file doesn't work.

## The Cause
This error occurs because Windows hasn't downloaded or updated the root security certificates needed for establishing a safe connection to Warner Bros servers. Since Windows doesn't have this certificate, servers reject the connection.

## How to solve the issue (PowerShell)
For solving this issue we need to force Windows to download and install the current certificates directly from Windows Update.

## Steps
1. Open PowerShell (**Run as administrator**)
2. Copy and paste the following comands.

```powershell
# 1. Create a temporal folder for certificates
md $Env:TEMP\certs

# 2. Navigate to the temporary folder
cd $Env:TEMP\certs

# 3. Download the updated root certificates from Windows Update
CertUtil -generateSSTFromWU $Env:TEMP\certs\RootStore.sst

# 4. Import the certificate to the local machine
 Import-Certificate -FilePath "$Env:TEMP\certs\RootStore.sst" -CertStoreLocation Cert:\LocalMachine\Root
```
