# auracapillaire-site
Site vitrine pour la marque capillaire 
import zipfile
import os
from PIL import Image

# Créer un répertoire temporaire
temp_dir = "website_with_logo"
os.makedirs(temp_dir, exist_ok=True)

# Créer un sous-dossier "images" pour le logo
images_dir = os.path.join(temp_dir, "images")
os.makedirs(images_dir, exist_ok=True)

# Ajouter un fichier logo (ici je vais créer un simple fichier image de test)
logo_path = os.path.join(images_dir, "logo.png")

# Créer une image vide (100x100 pixels, blanc)
img = Image.new('RGB', (100, 100), color='blue')
img.save(logo_path)

# Créer un fichier index.html simple qui va afficher le logo
html_content = """
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Site avec Logo</title>
</head>
<body>
    <h1>Bienvenue sur mon site !</h1>
    <img src="images/logo.png" alt="Logo" width="100" height="100">
</body>
</html>
"""

# Créer le fichier index.html
index_path = os.path.join(temp_dir, "index.html")
with open(index_path, "w") as f:
    f.write(html_content)

# Créer un fichier zip
zip_path = "website_with_logo.zip"
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zipf:
    for root, dirs, files in os.walk(temp_dir):
        for file in files:
            zipf.write(os.path.join(root, file), os.path.relpath(os.path.join(root, file), temp_dir))

print(f"Le fichier zip a été créé : {zip_path}")
