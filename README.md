En este repositorio estoy intentando implementar Data Version Control (DVC).

La ventaja de este enfoque es que los archivos grandes quedan respaldados en una nube como Drive, para que no tengan que quedar almacenados en alguna nube conectada con Git.

Las instrucciones de ejecución de DVC se encuentran [AQUÍ](./cheatsheet.md). 

Estoy gestionando las dependencias con Pipenv.


# 1️⃣ Configuración inicial de DVC y remotos
```bash
# Listar remotos existentes
dvc remote list

# Agregar un nuevo remoto (opcional)
dvc remote add -d backup_drive gdrive://<ID_DE_TU_CARPETA>

# Configurar Client ID y Client Secret (opcional)
dvc remote modify backup_drive gdrive_client_id <tu-client-id>
dvc remote modify backup_drive gdrive_client_secret <tu-client-secret>
```

# 2️⃣ Actualización de dependencias y fixes básicos
```bash
pip install --upgrade pip
pip install --upgrade cryptography pyOpenSSL google-auth
pip install --upgrade "dvc[gdrive]"

# Intentar un push inicial
dvc push
```

# 3️⃣ Ajustes de autenticación para Google Drive
```bash
# Desactivar temporalmente el uso de Service Account
dvc remote modify --local gdrive_remote gdrive_use_service_account false

# Limpiar credenciales locales antiguas
del .dvc\config.local
del .dvc\credentials

# Resetear Client ID y Client Secret si hay problemas
dvc remote modify --local gdrive_remote gdrive_client_id ""
dvc remote modify --local gdrive_remote gdrive_client_secret ""
```

# 4️⃣ Configuración final con credenciales de usuario
```bash
# Asignar archivo JSON de credenciales de usuario
dvc remote modify gdrive_remote gdrive_user_credentials_file E:\Projects\Plantiwuis-fotos\client_secret_890480662505-7giiorgp0ca4ib3vqan3uem66qjclunj.apps.googleusercontent.com.json

# Asegurarse de desactivar Service Account
dvc remote modify gdrive_remote gdrive_use_service_account false
```

# 5️⃣ Uso de Service Account (opcional, si se requiere)
```bash
# Activar Service Account
dvc remote modify --local gdrive_remote gdrive_use_service_account true

# Ruta al JSON de Service Account
dvc remote modify --local gdrive_remote gdrive_service_account_json_file_path "C:\Users\Rodrigo\Downloads\plantiwuisserviceacc-743d03d21dc8.json"

# ID del Shared Drive (si aplica)
dvc remote modify --local gdrive_remote gdrive_drive_id <ID_DEL_SHARED_DRIVE>
```

# 6️⃣ Subir datos y verificar
```bash
# Subir datos al remoto
dvc push -v

# Verificar status local vs remoto
dvc status -r gdrive_remote
dvc status -r gdrive
```
