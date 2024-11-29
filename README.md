# Projet ESP32 : Surveillance de l'environnement

Ce projet utilise une carte ESP32 pour surveiller la température, la lumière et contrôler des équipements comme un ventilateur et une LED. Les données sont collectées à l'aide de capteurs et exposées via un serveur HTTP intégré. Une connexion Wi-Fi est utilisée pour envoyer des données JSON à un hôte distant.

---

## Fonctionnalités principales
- **Surveillance de la température** :
  - Lecture des températures via un capteur DS18B20.
  - Stockage de l'historique des températures.
  - Calcul de la température moyenne au-dessus d'un seuil.
- **Surveillance de la lumière** :
  - Mesure de l'intensité lumineuse avec un photorésistor.
- **Gestion des équipements** :
  - Contrôle d'un ventilateur en fonction de la température.
  - Activation d'une LED en cas de détection de chaleur élevée.
- **API HTTP** :
  - Exposition des données via des endpoints (`/info`, `/updateTarget`).
  - Serveur HTTP intégré pour la communication.
- **Envoi de données JSON** :
  - Envoi des données collectées à un hôte distant configurable.
- **Interface utilisateur** :
  - Serveur pour servir une page HTML statique (`index.html`).

---

## Matériel requis
1. **ESP32**.
2. **Capteur de température DS18B20** (connecté sur le pin 23).
3. **Photorésistor** (connecté sur le pin 34).
4. **Ventilateur** (contrôlé par le pin 27).
5. **LED** (connectée au pin 2).
6. **Accès Wi-Fi** avec les identifiants :
   - SSID : `IOT`
   - Mot de passe : `iotmiage`.

---

## Bibliothèques utilisées
- **WiFi.h** : Pour la gestion du réseau Wi-Fi.
- **OneWire.h** et **DallasTemperature.h** : Pour communiquer avec le capteur DS18B20.
- **ArduinoJson.h** : Pour la gestion des objets JSON.
- **WebServer.h** : Pour créer un serveur HTTP intégré.
- **SPIFFS.h** : Pour gérer les fichiers statiques.
- **HTTPClient.h** : Pour les requêtes HTTP sortantes.

---

## Structure des données (JSON)
Les données sont organisées dans un objet JSON structuré selon plusieurs sections : 

- **Status** : Informations sur la température, la lumière, les états des équipements, etc.
- **Location** : Détails de localisation (latitude, longitude, salle, adresse).
- **Regul** : Seuils bas et haut pour la régulation de température.
- **Info** : Informations sur l'utilisateur et l'appareil.
- **Net** : Informations réseau (SSID, adresse MAC, IP, uptime).
- **ReportHost** : Cible pour l'envoi des données (IP, port, fréquence d'échantillonnage).

---

## Endpoints HTTP
1. **`/`** : Sert une page HTML depuis le système de fichiers SPIFFS.
2. **`/info`** : Retourne les données actuelles sous forme de JSON.
3. **`/updateTarget`** (POST) : Met à jour les informations de l'hôte cible (IP, port, fréquence d'échantillonnage).

---

## Configuration
### Connexion Wi-Fi
Modifiez les identifiants Wi-Fi dans le code si nécessaire :
```cpp
const char* ssid = "IOT";
const char* password = "iotmiage";
