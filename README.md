from zipfile import ZipFile
import os

# Simulamos una estructura básica de un proyecto Android para "Mi DNI Perro"
project_files = {
    "MiDniPerro/app/src/main/AndroidManifest.xml": "<manifest package='com.midniperro'></manifest>",
    "MiDniPerro/app/src/main/java/com/midniperro/MainActivity.java": "public class MainActivity {}",
    "MiDniPerro/app/src/main/res/layout/activity_main.xml": "<LinearLayout></LinearLayout>",
    "MiDniPerro/app/build.gradle": "apply plugin: 'com.android.application'",
    "MiDniPerro/build.gradle": "buildscript {}",
    "MiDniPerro/README.md": "# Mi DNI Perro App"
}

# Crear estructura de carpetas y archivos temporales
base_path = "/mnt/data/MiDniPerro"
for path, content in project_files.items():
    full_path = os.path.join("/mnt/data", path)
    os.makedirs(os.path.dirname(full_path), exist_ok=True)
    with open(full_path, "w") as f:
        f.write(content)

# Crear el archivo ZIP
zip_path = "/mnt/data/MiDniPerro.zip"
with ZipFile(zip_path, "w") as zipf:
    for path in project_files:
        full_path = os.path.join("/mnt/data", path)
        zipf.write(full_path, arcname=path)

zip_path
