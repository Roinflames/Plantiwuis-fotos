🧩 2️⃣ Inicializar el repositorio Git
pipenv install dvc
pipenv install "dvc[gdrive]"

🧩 2️⃣ Verifica que esté instalado:
dvc version

🧩 3️⃣ Inicializar DVC
dvc init

🧩 4️⃣ Rastrear tus imágenes con DVC
dvc add .

🧩 5️⃣ Confirmar los cambios en Git
git add .gitignore .dvc .dvcignore *.dvc
git commit -m "Inicializa repositorio con DVC para imágenes"

🧩 6️⃣ (Opcional) Configurar almacenamiento remoto de DVC
dvc remote add -d myremote gdrive://<folder_id>
dvc remote add -d gdrive_remote gdrive://1c6HftLT2SV08kORDFuu8g79eAOxvDSSE

🧩 6️⃣ Luego configura permisos opcionales (para evitar pedir autenticación siempre):
dvc remote modify gdrive_remote gdrive_use_service_account true

🧩 6️⃣ 
dvc push

🧩 6️⃣ 
dvc remote add -d local_remote "D:\DVC_Remote\Plantiwuis"
dvc push

🧩 7️⃣ Verificar el estado
dvc status
dvc checkout
+------------------------------------------------------------------------------

🧩 2️⃣ Configurar el remoto de DVC apuntando a tu carpeta
dvc remote add -d gdrive gdrive://1c6HftLT2SV08kORDFuu8g79eAOxvDSSE
dvc remote list
dvc push
