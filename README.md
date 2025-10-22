# socleMvcIut
Installation et Configuration
1. Installer les dépendances

# Mettre à jour les paquets
sudo apt update

# Installer Apache, MySQL et PHP
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y

# Vérifier les installations
php -v
mysql --version
apache2 -v

2. Créer la structure du projet

# Aller dans le dossier web d'Apache
cd /var/www/html

# Créer le dossier du projet
sudo mkdir simple-mvc
cd simple-mvc

# Créer l'arborescence
sudo mkdir -p config controllers models views/users

# Créer les fichiers (copier le contenu de l'artifact dans chaque fichier)
sudo nano index.php
sudo nano config/database.php
sudo nano controllers/UserController.php
sudo nano models/User.php
sudo nano views/users/login.php
sudo nano views/users/list.php
sudo nano views/users/create.php
sudo nano views/users/edit.php

# Donner les permissions
sudo chown -R www-data:www-data /var/www/html/simple-mvc
sudo chmod -R 755 /var/www/html/simple-mvc

3. Configurer MySQL
   
# Se connecter à MySQL
sudo mysql -u root

# Dans le prompt MySQL, exécuter :
CREATE DATABASE simple_mvc;
USE simple_mvc;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Créer un utilisateur de test (password: "admin123")
INSERT INTO users (name, email, password) 
VALUES ('Admin', 'admin@example.com', '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi');

EXIT;

4. Démarrer le serveur
# Démarrer Apache
sudo systemctl start apache2

# Activer Apache au démarrage
sudo systemctl enable apache2

# Vérifier le statut
sudo systemctl status apache2
```

### 5. **Accéder à l'application**
Ouvrez votre navigateur et allez à :
```
http://localhost/simple-mvc/

Identifiants de test :
Email : admin@example.com
Mot de passe : admin123

Si le serveur ne démarre pas :
sudo systemctl restart apache2
sudo tail -f /var/log/apache2/error.log

Si erreur de connexion MySQL :
# Réinitialiser le mot de passe root MySQL
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '';
FLUSH PRIVILEGES;
EXIT;

Modifier config/database.php si besoin pour adapter les identifiants MySQL.
