# 🧩 VM_Configuration

## 🎯 Objectif

Ce dossier contient les **fichiers de configuration essentiels** utilisés pour l’installation et la mise en service de **GLPI sur Debian 11**.
Ils permettent de **reproduire la configuration du serveur Apache2 et PHP** sans devoir importer la machine virtuelle complète.

Ces fichiers ont été utilisés et testés lors du projet _Installation complète de GLPI sur Debian_
réalisé par **Théo FRANÇOIS – Octobre 2025**.

---

## 📁 Contenu du dossier

| Fichier                    | Emplacement système                                | Description                                                             |
| -------------------------- | -------------------------------------------------- | ----------------------------------------------------------------------- |
| `apache2_glpi.conf`        | `/etc/apache2/sites-available/glpi.conf`           | Configure le VirtualHost GLPI (port 80) et le dossier racine `/public`. |
| `php_99-glpi-sessions.ini` | `/etc/php/7.4/apache2/conf.d/99-glpi-sessions.ini` | Définit le chemin et les paramètres des sessions PHP pour GLPI.         |
| `glpi_public_htaccess`     | `/var/www/html/glpi/public/.htaccess`              | Gère la réécriture des URL et la sécurité des fichiers sensibles.       |

---

## ⚙️ Instructions d’utilisation

### 1️⃣ Copier les fichiers dans les bons répertoires

```bash
sudo cp apache2_glpi.conf /etc/apache2/sites-available/glpi.conf
sudo cp php_99-glpi-sessions.ini /etc/php/7.4/apache2/conf.d/99-glpi-sessions.ini
sudo cp glpi_public_htaccess /var/www/html/glpi/public/.htaccess
```

---

### 2️⃣ Vérifier les permissions

```bash
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
```

---

### 3️⃣ Activer la configuration Apache

```bash
sudo a2enmod rewrite
sudo a2ensite glpi.conf
sudo systemctl reload apache2
```

---

### 4️⃣ Vérifier le bon fonctionnement

Accéder à :
➡️ `http://<IP_DE_LA_VM>`
Tu dois voir la page de connexion GLPI.

---

## 💡 Bonnes pratiques

- Sauvegarde avant toute modification :

  ```bash
  sudo cp /etc/apache2/sites-available/glpi.conf /etc/apache2/sites-available/glpi.conf.backup
  ```

- Redémarre Apache après chaque changement PHP ou `.conf` :

  ```bash
  sudo systemctl restart apache2
  ```

- Si les sessions ne fonctionnent pas :

  - Vérifie le chemin défini dans `php_99-glpi-sessions.ini`
  - Vérifie que les droits appartiennent bien à `www-data`

---

## 🧠 À retenir

Ces fichiers représentent la **base de configuration minimale pour faire fonctionner GLPI** sur un environnement Debian stable.
Ils respectent :

- la structure de GLPI 10 (`/public` comme racine web),
- les standards Apache2,
- et les bonnes pratiques de sécurité PHP.

> ✅ En combinant ces fichiers avec la documentation technique principale, il est possible de **reconstruire la machine Debian GLPI à l’identique**.
