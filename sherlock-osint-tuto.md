# 🔍 Sherlock — Trouver un pseudo sur 300+ plateformes

> **Niveau** : Débutant | **Durée** : 20 min | **OS** : Kali Linux / Ubuntu / Windows

---

## 📌 Table des matières

1. [C'est quoi Sherlock ?](#cest-quoi-sherlock)
2. [Prérequis](#prérequis)
3. [Installation](#installation)
4. [Utilisation de base](#utilisation-de-base)
5. [Options avancées](#options-avancées)
6. [Exemples concrets](#exemples-concrets)
7. [Interpréter les résultats](#interpréter-les-résultats)
8. [Bonnes pratiques et éthique](#bonnes-pratiques-et-éthique)
9. [Ressources pour aller plus loin](#ressources-pour-aller-plus-loin)

---

## C'est quoi Sherlock ?

**Sherlock** est un outil open source écrit en Python qui permet de rechercher un nom d'utilisateur (pseudo) sur plus de **300 plateformes** en une seule commande.

Il est utilisé dans le domaine de l'**OSINT (Open Source Intelligence)** pour :

- Retrouver les comptes liés à une personne
- Vérifier si un pseudo est utilisé ailleurs
- Analyser la présence en ligne d'une cible
- Auditer sa propre empreinte numérique

> ⚠️ **Usage légal uniquement** — Sherlock doit être utilisé sur des cibles autorisées ou pour auditer vos propres comptes. Toute utilisation malveillante est illégale.

---

## Prérequis

Avant de commencer, assure-toi d'avoir :

- [ ] Kali Linux, Ubuntu ou tout système Linux
- [ ] Python 3.6 ou supérieur
- [ ] pip3 installé
- [ ] Git installé
- [ ] Une connexion internet

Vérifier les versions installées :

```bash
python3 --version
pip3 --version
git --version
```

---

## Installation

### Méthode 1 — Cloner depuis GitHub (recommandée)

```bash
# 1. Cloner le dépôt officiel
git clone https://github.com/sherlock-project/sherlock.git

# 2. Entrer dans le dossier
cd sherlock

# 3. Installer les dépendances
pip3 install -r requirements.txt
```

### Méthode 2 — Via pip

```bash
pip3 install sherlock-project
```

### Méthode 3 — Sur Kali Linux (déjà disponible)

```bash
# Sherlock est parfois déjà installé sur Kali
sherlock --version

# Sinon l'installer via apt
sudo apt update && sudo apt install sherlock
```

### Vérifier l'installation

```bash
python3 sherlock --help
```

Si tu vois la liste des options, l'installation est réussie ✅

---

## Utilisation de base

### Recherche simple

```bash
python3 sherlock nom_du_pseudo
```

**Exemple :**

```bash
python3 sherlock batman
```

Ce que tu verras dans le terminal :

```
[*] Checking username batman on:
[+] GitHub: https://www.github.com/batman
[+] Instagram: https://www.instagram.com/batman
[+] Reddit: https://www.reddit.com/user/batman
[+] Twitter: https://www.twitter.com/batman
[!] Facebook: Not Found
...
[*] Results: 134 found. 172 not found.
```

- `[+]` = Compte trouvé ✅
- `[!]` = Compte non trouvé ❌
- `[*]` = Information générale

---

## Options avancées

### Rechercher plusieurs pseudos en même temps

```bash
python3 sherlock pseudo1 pseudo2 pseudo3
```

### Sauvegarder les résultats dans un fichier

```bash
# Sauvegarde automatique dans un fichier .txt
python3 sherlock batman --output resultats.txt

# Ou format CSV
python3 sherlock batman --csv
```

### Afficher uniquement les comptes trouvés

```bash
python3 sherlock batman --print-found
```

### Ignorer les erreurs de certificat SSL

```bash
python3 sherlock batman --no-color
```

### Définir un timeout (délai d'attente)

```bash
# Timeout de 10 secondes par site
python3 sherlock batman --timeout 10
```

### Mode silencieux (moins de sortie)

```bash
python3 sherlock batman --print-found --no-color > resultats.txt
```

### Tableau récapitulatif des options

| Option | Description |
|--------|-------------|
| `--help` | Affiche l'aide |
| `--output fichier.txt` | Sauvegarde dans un fichier |
| `--csv` | Exporte en format CSV |
| `--print-found` | Affiche seulement les comptes trouvés |
| `--timeout 10` | Délai max par site (secondes) |
| `--no-color` | Désactive les couleurs |
| `--verbose` | Mode détaillé |
| `--site NomSite` | Cherche sur un site spécifique |

---

## Exemples concrets

### Exemple 1 — Auditer son propre pseudo

```bash
# Remplace "ton_pseudo" par ton vrai pseudo
python3 sherlock ton_pseudo --print-found --output mon_audit.txt
```

C'est le meilleur exercice pour débuter : tu vois exactement ce qu'un inconnu peut trouver sur toi.

### Exemple 2 — Recherche sur un site spécifique

```bash
# Chercher uniquement sur GitHub
python3 sherlock batman --site GitHub

# Chercher sur Instagram
python3 sherlock batman --site Instagram
```

### Exemple 3 — Recherche multiple et export CSV

```bash
python3 sherlock batman joker harley --csv
```

Cela génère un fichier `batman.csv`, `joker.csv` et `harley.csv` que tu peux ouvrir dans Excel ou LibreOffice.

### Exemple 4 — Recherche rapide avec timeout court

```bash
# Parfait quand tu veux des résultats vite
python3 sherlock batman --timeout 5 --print-found
```

---

## Interpréter les résultats

### Ce que Sherlock trouve

Quand un compte est trouvé `[+]`, Sherlock te donne l'URL directe du profil.

Exemple de résultat réel :

```
[+] GitHub: https://www.github.com/batman
[+] Reddit: https://www.reddit.com/user/batman
[+] TikTok: https://www.tiktok.com/@batman
```

### Ce que tu peux faire avec ces infos

1. **Vérifier** que c'est bien la même personne (photo, bio, contenu)
2. **Croiser** les informations entre les plateformes
3. **Identifier** des infos supplémentaires (localisation, contacts, activités)
4. **Cartographier** la présence en ligne dans un rapport

### Limites de Sherlock

- Les faux positifs existent (un site peut dire "trouvé" même si le profil n'existe pas)
- Certains comptes privés ne sont pas accessibles
- Sherlock ne contourne pas les protections des sites
- Les résultats dépendent de la connexion internet

> 💡 **Astuce pro** : Toujours vérifier manuellement les liens trouvés avant de les inclure dans un rapport.

---

## Bonnes pratiques et éthique

### ✅ Utilisations légales

- Auditer ses propres comptes
- CTF (Capture The Flag) et challenges OSINT
- Pentest avec autorisation écrite
- Recherche académique encadrée

### ❌ Utilisations interdites

- Stalking / harcèlement d'une personne
- Collecte de données sans consentement (RGPD)
- Utilisation dans un but malveillant
- Doxxing (révéler l'identité de quelqu'un sans consentement)

### 🛡️ Protéger ton anonymat pendant l'investigation

```bash
# Utiliser avec un VPN activé
# Ou via Tor (plus lent mais plus anonyme)
torify python3 sherlock batman
```

---

## Ressources pour aller plus loin

### Outils complémentaires à Sherlock

| Outil | Usage | Lien |
|-------|-------|------|
| **Maigret** | Version améliorée de Sherlock | github.com/soxoj/maigret |
| **Holehe** | Recherche par email | github.com/megadose/holehe |
| **Social-Analyzer** | Analyse avancée de profils | github.com/qeeqbox/social-analyzer |
| **Maltego** | Graphes de liens visuels | maltego.com |

### Plateformes pour pratiquer légalement

- [TryHackMe](https://tryhackme.com) — Rooms OSINT guidées
- [CTFtime.org](https://ctftime.org) — Compétitions CTF
- [OSINT Framework](https://osintframework.com) — Catalogue d'outils

### Pour aller plus loin en OSINT

- Livre : *Open Source Intelligence Techniques* — Michael Bazzell
- Chaîne YouTube : NetworkChuck, David Bombal
- Site : bellingcat.com (investigations réelles)

---

## 📝 Résumé des commandes essentielles

```bash
# Installation
git clone https://github.com/sherlock-project/sherlock.git
cd sherlock && pip3 install -r requirements.txt

# Recherche simple
python3 sherlock pseudo

# Recherche avec export
python3 sherlock pseudo --output resultats.txt

# Recherche multiple
python3 sherlock pseudo1 pseudo2 pseudo3

# Afficher seulement les trouvés
python3 sherlock pseudo --print-found

# Sur un site spécifique
python3 sherlock pseudo --site GitHub
```

---

*Tutoriel rédigé dans un but éducatif — OSINT éthique et légal uniquement*

*N'hésite pas à ⭐ star ce repo si ce tuto t'a été utile !*
