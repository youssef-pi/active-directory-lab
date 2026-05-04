# 🪟 Active Directory Lab — Déploiement complet d’un domaine Windows Server (AD DS + DNS + GPO)

> Lab pratique visant à mettre en place un **domaine Active Directory** fonctionnel : contrôleur de domaine, DNS interne, poste client joint au domaine et application de **GPO**.

---

## 🎯 Objectifs

- Comprendre l’**authentification centralisée** via Active Directory
- Structurer l’annuaire : **OU, utilisateurs, groupes**
- Joindre un poste **Windows 11** au domaine et valider le fonctionnement
- Appliquer des **stratégies GPO** (sécurité + paramètres utilisateurs)
- Mettre en place des **bonnes pratiques** (IP statique, DNS interne, organisation)

---

## 🧰 Technologies & outils

- **Windows Server 2019/2022** : AD DS, DNS
- **Windows 11** : poste client
- **GPO** : Group Policy Management
- **VirtualBox** : virtualisation

---

## 🗺️ Architecture du lab

### 🔧 Machines
| Rôle | Nom (exemple) | OS | IP (exemple) |
|---|---|---|---|
| Contrôleur de domaine | `DC01` | Windows Server 2019/2022 | `192.168.56.10` (statique) |
| Poste client | `PC01` | Windows 11 | DHCP / statique (selon le lab) |

### 🌐 Réseau
- **NAT** : accès internet (updates, etc.)
- **Host-Only** : réseau isolé entre les VMs
- **Domaine** : `helpdesk-lab.local`
- **DNS** : assuré par le contrôleur de domaine (`DC01`)

> Important : le poste client doit utiliser **le DNS du DC** (ex: `192.168.56.10`) pour rejoindre le domaine.

---

## ✅ Mise en place (résumé des étapes)

### 1) Préparation serveur
- Installation Windows Server + mise à jour
- **IP statique** sur le serveur
- Nom du serveur (ex: `DC01`)
- Vérification connectivité réseau

### 2) Installation des rôles
- Ajout des rôles :
  - **Active Directory Domain Services (AD DS)**
  - **DNS Server**

### 3) Promotion en contrôleur de domaine
- Création d’une nouvelle forêt :
  - Domaine : `helpdesk-lab.local`
- Vérification services AD + DNS

### 4) Organisation de l’annuaire
- Création d’**OU** (exemples) :
  - `OU=Utilisateurs`
  - `OU=Groupes`
  - `OU=Postes`
- Création des **utilisateurs** et **groupes**
- Affectation des groupes aux utilisateurs (selon scénario)

### 5) Jonction du poste client au domaine
- Configuration DNS du client → **DNS = IP du DC**
- Join domaine : `helpdesk-lab.local`
- Vérification :
  - connexion avec un compte de domaine
  - PC visible dans AD (OU `Postes`)

### 6) Configuration des GPO
- Création et lien des GPO sur les OU concernées
- Exemples :
  - **Restrictions horaires de connexion**
  - paramètres de sécurité et session utilisateur
- Mise à jour des policies (`gpupdate /force`) et tests

---

## 🔐 Bonnes pratiques & sécurité appliquées

- **IP statique** obligatoire pour le Domain Controller
- DNS interne géré par AD (**le DNS est central** dans un domaine)
- Organisation via **OU** pour appliquer les GPO proprement
- Gestion centralisée des comptes (utilisateurs/groupes)

---

## 🧪 Tests & vérifications

- ✅ Connexion au domaine depuis le poste client (compte AD)
- ✅ Résolution DNS interne
- ✅ Application des GPO (test + vérif `gpresult`)

Commandes utiles (côté client) :
```powershell
gpupdate /force
gpresult /r
whoami
```

---

## 📌 Ce que j’ai appris

- Le rôle critique du **DNS** dans Active Directory
- La logique de structuration via **OU** (pour gérer et appliquer les GPO)
- Déploiement d’un environnement Windows “entreprise” : utilisateurs, groupes, postes
- Méthodologie de test : validation de l’auth, des policies et de la résolution de noms

---

## 📬 Contact
Si tu as des questions ou suggestions : **ymansouri.pro@gmail.com**
