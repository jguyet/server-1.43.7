> ⚠️ **ATTENTION**
> - Cet émulateur a été grandement modifié.  
> - Aucune aide ne sera apportée si vous souhaitez également le modifier.  
> - L'utilisation de ce travail à des fins malhonnêtes est interdite.  

---

![Logo](./aegnorlogo.png)

# 🐉 AEGNOR SERVEUR — Game 1.43.7

Cet émulateur est **open source** et disponible pour tout le monde.  
Merci de **ne pas le vendre** : vous l’avez reçu gratuitement, donnez-le gratuitement 🤗.  

Originalement développé pour un **client 1.34.1**, ce game est désormais **porté pour le client Dofus Retro 1.43.7**.  
Il est lié au GitHub login suivant :  
👉 [login-1.43.7](https://github.com/jguyet/login-1.43.7) (fork du Aegnor login / Locos)

---

## 🆕 Compatibilité client 1.43.7

Le portage vers le client Dofus Retro 1.43.7 inclut :

### Networking & dispatcher
- **Transport** : version client `1.43.7`, réponse Flash `<policy-file-request/>`, parser format `ù` 3-parts (`base64ù<chksum>ù<commande>`), `encryptPacket = false`.
- **Cases dispatcher** ajoutés/corrigés : `'k'` (Kolizéum no-op), `'z'` (zones / Almanax no-op), `'I'` (window desc), `'H'` (character switch `HS`), `'p'`/`'q'`/`'r'` (ping/qping/rpong). Fix fallthrough sur `'X'`.
- **GI cyrillique** : normalisation `'І' (U+0406) → 'I'` (le client 1.43.7 envoie le caractère cyrillique).
- **GI throttle** : 800ms (sinon spam → re-envoi en boucle des entités → flicker).
- **GDM short format** : revenu au format court `GDM|id|date|key` (Bustemu n'utilise pas le format long).
- **Restauration clés de décryption maps** depuis `static_maps` (9218 maps mises à jour en SQL).

### No-op stubs pour features 1.43.7
- `BK` (vocab sanction → réponse `BN`)
- `BR` (report → ignoré)
- Almanax, Ornements, Succès, Live action, Ladder, boutique in-game : no-op natif via sous-switch sans `default`.

### Bugs gameplay débloqués par l'analyse du parser AS2
- **Console admin "Erreur de protocole"** : format `BAT{type}|0||{msg}` (au lieu de `BAT0<msg>` qui faisait planter le parser).
- **Boost stats "Boost Invalide"** : split du packet `AB<id>|<qty>` sur `|` (au lieu de `;`). Refactor de `boostStats2` pour interpréter qty comme nombre de stats voulus.
- **Commande `.LEVEL`** : envoi explicite de `GAME_SEND_STATS_PACKET` + `GAME_SEND_SPELL_LIST` après le levelup pour rafraîchir l'UI.
- **Character switch (`HS`)** : flow complet implémenté côté game (génération ticket, notification login via Exchange `WS<accId>;<ticket>#`, `closeOnFlush` au lieu de `closeNow`).
- **Couleurs des monstres tous noirs** : format `+cell;ori;star;groupId;mobIDs;-3;gfx;levels;colors_mob1;acc_mob1;...` (sans `totalExp` qui décalait les positions attendues par le parser AS2).

---

## ⚙️ INFORMATIONS

Aegnor est un serveur **EasyLike** :  
- Une expérience de jeu légèrement accélérée  
- Un système de rareté des objets  
- De nouvelles fonctionnalités absentes du client officiel  

Cet émulateur est basé sur **Starloco** et diverses autres sources afin d’en extraire le meilleur.  
👉 Plus d’informations disponibles sur l’ancien [Discord du serveur](https://discord.com/invite/f2cNEZ2cev).

---

## 🐞 DEBUGS

La liste complète des debugs est visible sur le **Discord** dans l’onglet *Patchnote*.

---

## ✨ FONCTIONNALITÉS PRINCIPALES

- 🔹 Système de rareté d’équipement  
- 🔹 Runes spécifiques associées  
- 🔹 Donjons simplifiés  
- 🔹 Tous les métiers accessibles dès la création d’un personnage  
- 🔹 Core spécifique obligatoire pour gérer la rareté & fonctionnalités avancées  
- 🔹 Fonctionnalités multi-comptes : *OneWindows, ControlInvo*, etc.  

---

## 📥 TÉLÉCHARGEMENT

L’archive **Aegnor_Serveur.zip** contient l’intégralité des fichiers nécessaires pour exécuter le serveur en local.
👉 [Aegnor_Serveur.zip](https://mega.nz/file/GFZhXQ7L#r9-qOuBxayiz0oUXc65SHHbQrkVybgL6EFaEl-ZRKUA) 

---

## 🚀 INSTALLATION

1. Compilez le projet en `.jar`  
2. Lancez le serveur avec :  

   ```bash
   java -Xmx2G -jar Aegnor.jar
   ```
3. Connectez-vous avec le compte déjà créé :  
   - **login** : `admin1`  
   - **mot de passe** : `admin`  

🎥 Tutoriel vidéo d’installation : [Cliquez ici](https://youtu.be/06tjFmFvEkk)

---

## 🙏 REMERCIEMENTS

Un grand merci à :  
- **Hydronish** pour son aide lors du développement  
- **Locos** pour la base de son travail
- L’ensemble des donateurs qui ont soutenu le projet  
- Tous les auteurs qui ont contribués aux émulateurs précédents ou ultérieur

👤 Portage client **1.43.7** : **Jiji** ([@jguyet](https://github.com/jguyet))  
👤 Auteur original : [@arwase](https://github.com/arwase)  
💬 Discord : `Arwase#6656`

---
