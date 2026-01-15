# 🏠 Homelab Command Center

Dashboard centralisé pour la gestion et le monitoring de mon infrastructure homelab.

## 📋 Vue d'ensemble

Ce projet est un tableau de bord web moderne construit avec React et Tailwind CSS, permettant de gérer et monitorer l'ensemble des services self-hosted de mon infrastructure personnelle.

### ✨ Fonctionnalités principales

- **Dashboard interactif** : Vue d'ensemble de tous les services avec indicateurs de statut en temps réel
- **Catégorisation intelligente** : Services organisés par type (Infrastructure, Applications, Médias, Téléchargements, Monitoring)
- **Recherche et filtrage** : Recherche rapide parmi tous les services
- **Monitoring système** : Métriques CPU, RAM, Disque en temps réel via Glances
- **Gestion Docker** : Statistiques des conteneurs et accès aux logs via Dozzle
- **Mode édition** : Configuration dynamique des services
- **Terminal SSH intégré** : Accès direct au serveur depuis le dashboard
- **Design moderne** : Interface glassmorphism avec thème sombre

## 🛠️ Stack technique

- **Frontend** : React 18 (standalone)
- **Styling** : Tailwind CSS
- **Icons** : Lucide Icons
- **Architecture** : Single Page Application (SPA)
- **Configuration** : JSON dynamique

## 📦 Services hébergés

### Infrastructure (5 services)
- **Roundcube** - Webmail client
- **Nginx Proxy Manager** - Reverse proxy & SSL
- **Portainer** - Interface de gestion Docker
- **IRMC S5** - Gestion serveur physique
- **Kopia UI** - Système de sauvegarde

### Applications (6 services)
- **Actual Budget** - Gestion financière personnelle
- **Vaultwarden** - Gestionnaire de mots de passe (Bitwarden)
- **Nextcloud** - Cloud privé & collaboration
- **Portfolio** - Site personnel
- **IT-Tools** - Boîte à outils développeur

### Médias (6 services)
- **Plex** - Serveur multimédia
- **Overseerr** - Requêtes de contenu
- **Tautulli** - Statistiques Plex
- **Tdarr** - Transcodage automatisé
- **Radarr** - Gestion films
- **Sonarr** - Gestion séries
- **Bazarr** - Gestion sous-titres

### Téléchargements (2 services)
- **qBittorrent** - Client torrent avec VPN
- **Prowlarr** - Gestion des indexeurs

### Monitoring (6 services)
- **Grafana** - Tableaux de bord visuels
- **Prometheus** - Collecte de métriques
- **cAdvisor** - Métriques conteneurs
- **Uptime Kuma** - Monitoring de disponibilité
- **Dozzle** - Visualisation logs conteneurs

## 🚀 Installation

### Prérequis
- Serveur web (nginx, Apache, ou autre)
- Accès aux services backend (Glances, Dozzle)
- Configuration DNS pour les sous-domaines `*.du-cray.eu`

### Déploiement

1. **Cloner le repository**
```bash
git clone <repo-url>
cd homelab
```

2. **Configuration**
Éditer `config.json` pour personnaliser vos services :
```json
{
  "categories": [...],
  "services": [...]
}
```

3. **Déploiement**
```bash
# Copier les fichiers vers le serveur web
cp -r . /var/www/dashboard/

# Ou utiliser docker-compose (exemple)
docker run -d -p 80:80 \
  -v $(pwd):/usr/share/nginx/html:ro \
  nginx:alpine
```

4. **Configuration DNS**
Configurer les enregistrements DNS pour pointer vers votre serveur :
- `dashboard.du-cray.eu` → IP serveur
- `*.du-cray.eu` → IP serveur (wildcard)

## ⚙️ Configuration

### Structure du fichier config.json

```json
{
  "categories": [
    {
      "id": "category-id",
      "name": "Nom de la catégorie",
      "icon": "lucide-icon-name"
    }
  ],
  "services": [
    {
      "id": "service-id",
      "name": "Nom du service",
      "cat": "category-id",
      "icon": "lucide-icon-name",
      "desc": "Description",
      "color": "bg-color-500",
      "url": "https://service.domain.com/",
      "logsUrl": "https://logs.service.com/" // optionnel
    }
  ]
}
```

### Variables d'environnement

Modifier dans `index.html` :
```javascript
const BASE_DOMAIN = 'du-cray.eu';
const DOZZLE_URL = `https://dozzle.${BASE_DOMAIN}`;
const GLANCES_URL = `https://glances.${BASE_DOMAIN}`;
```

## 🔒 Sécurité

- Tous les services sont accessibles via HTTPS (Let's Encrypt)
- Authentification via Nginx Proxy Manager
- Certains services protégés par authentification basique
- VPN intégré pour qBittorrent

## 📊 Monitoring

Le dashboard intègre plusieurs sources de monitoring :
- **Glances** : Métriques système en temps réel
- **Dozzle** : Logs Docker en direct
- **Uptime Kuma** : Vérification de disponibilité
- **Grafana/Prometheus** : Métriques détaillées et alertes

## 🎨 Personnalisation

### Thème
Le dashboard utilise un thème sombre avec effet glassmorphism. Les couleurs peuvent être personnalisées dans la section `<style>` de `index.html`.

### Icônes
Les icônes proviennent de [Lucide Icons](https://lucide.dev/). Voir la documentation pour la liste complète des icônes disponibles.

## 📝 Licence

Usage personnel - © 2026 Louis-Marie PERRET DU CRAY

## 🔗 Liens utiles

- [React Documentation](https://react.dev/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Lucide Icons](https://lucide.dev/)
- [Nginx Proxy Manager](https://nginxproxymanager.com/)

---

**Statut** : 🟢 Production  
**Version** : 1.0  
**Dernière mise à jour** : Janvier 2026
