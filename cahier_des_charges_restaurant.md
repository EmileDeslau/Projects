# Cahier des Charges — Application de Gestion de Restaurant

> **Version** : 1.0  
> **Date** : 14 mars 2026  
> **Statut** : Draft  

---

## 1. Présentation du Projet

### 1.1 Contexte

Conception et développement d'une application complète de gestion de restaurant permettant la prise de commandes, la gestion du menu avec **tarification dynamique selon la quantité**, le suivi des tables, la facturation et le pilotage de l'activité.

### 1.2 Objectifs

| # | Objectif |
|---|----------|
| 1 | Fluidifier la prise de commande (salle & en ligne) |
| 2 | Appliquer automatiquement une grille tarifaire variable selon la quantité commandée |
| 3 | Centraliser la gestion du menu, des stocks et des paiements |
| 4 | Offrir une visibilité temps réel sur l'activité du restaurant |

### 1.3 Utilisateurs Cibles

| Rôle | Description |
|------|-------------|
| **Administrateur** | Propriétaire / gérant — accès total |
| **Serveur** | Prise de commande, gestion des tables |
| **Cuisinier** | Visualisation des commandes en cuisine |
| **Caissier** | Encaissement et facturation |
| **Client** | Consultation du menu, commande en ligne (optionnel) |

---

## 2. Modèle de Tarification Dynamique

### 2.1 Principe

Chaque article du menu possède une **grille tarifaire par palier de quantité**. Plus le client commande d'unités d'un même article, plus le prix unitaire peut varier (réduction ou tarif dégressif).

### 2.2 Structure de Prix

```
Article : Pizza Margherita
┌────────────┬────────────────┬────────────┐
│  Quantité  │  Prix Unitaire │   Total    │
├────────────┼────────────────┼────────────┤
│  1         │  12.00 €       │  12.00 €   │
│  2 – 4     │  11.00 €       │  22 – 44 € │
│  5 – 9     │  10.00 €       │  50 – 90 € │
│  10+       │   9.00 €       │  90.00 €+  │
└────────────┴────────────────┴────────────┘
```

### 2.3 Règles Métier

| Règle | Description |
|-------|-------------|
| **R1** | Chaque article a au minimum 1 palier (prix de base) |
| **R2** | Les paliers sont définis par l'administrateur (quantité min → quantité max → prix unitaire) |
| **R3** | Le prix affiché au client se recalcule en temps réel dès modification de la quantité |
| **R4** | Les paliers sont cumulables par article, pas entre articles différents |
| **R5** | Un article peut aussi avoir des **variantes** (taille, supplément) avec leur propre grille |

### 2.4 Schéma de Données — Tarification

```
Article
├── id
├── nom
├── description
├── catégorie
├── image
├── variantes[] (optionnel : taille S/M/L, etc.)
│   ├── id
│   ├── label
│   └── paliers_prix[]
└── paliers_prix[]
    ├── quantité_min
    ├── quantité_max (null = illimité)
    └── prix_unitaire
```

---

## 3. Exigences Fonctionnelles

### 3.1 MUST HAVE — Fonctionnalités Obligatoires

#### 3.1.1 Gestion du Menu

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| M-01 | Créer / modifier / supprimer un article | Nom, description, catégorie, image, statut (actif/inactif) |
| M-02 | Définir les paliers de prix par quantité | Interface d'ajout de paliers (qté min, qté max, prix unitaire) |
| M-03 | Gérer les catégories | Entrées, Plats, Desserts, Boissons, Menus/Formules… |
| M-04 | Gérer les variantes d'un article | Taille (S/M/L), cuisson, suppléments — chaque variante a ses propres paliers |
| M-05 | Activer / désactiver un article | Masquer temporairement un plat (rupture de stock) |
| M-06 | Affichage du prix dynamique | Le prix unitaire et total se mettent à jour selon la quantité sélectionnée |

#### 3.1.2 Gestion des Commandes

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| M-07 | Créer une commande | Associer à une table ou à un client (emporter/livraison) |
| M-08 | Ajouter des articles avec quantité | Sélection d'articles, modification de quantité, recalcul automatique du prix |
| M-09 | Modifier une commande en cours | Ajouter/retirer des articles, changer les quantités |
| M-10 | Annuler une commande | Annulation totale ou partielle avec motif |
| M-11 | Statuts de commande | En attente → En préparation → Prête → Servie → Clôturée |
| M-12 | Notes / instructions spéciales | Allergies, préférences, cuisson, sans gluten… |

#### 3.1.3 Gestion des Tables

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| M-13 | Plan de salle configurable | Créer/positionner les tables, définir capacité |
| M-14 | Statut des tables | Libre → Occupée → Réservée → À nettoyer |
| M-15 | Associer une commande à une table | Lien direct table ↔ commande active |

#### 3.1.4 Facturation & Paiement

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| M-16 | Générer l'addition | Récapitulatif détaillé avec prix unitaires par palier et totaux |
| M-17 | Modes de paiement | CB, Espèces, Ticket restaurant, Paiement mixte |
| M-18 | Division de l'addition | Partager par nombre de convives ou par article |
| M-19 | Impression / envoi du ticket | Impression thermique ou envoi par e-mail / SMS |
| M-20 | TVA configurable | Taux par catégorie (sur place / à emporter) |

#### 3.1.5 Affichage Cuisine (KDS)

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| M-21 | Écran de commandes en cuisine | Liste des commandes en attente, triées par ancienneté |
| M-22 | Marquage « Prêt » | Le cuisinier valide la préparation, notification au serveur |

#### 3.1.6 Authentification & Rôles

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| M-23 | Connexion sécurisée | Login / mot de passe ou code PIN rapide (serveurs) |
| M-24 | Gestion des rôles | Admin, Serveur, Cuisinier, Caissier — permissions distinctes |
| M-25 | Journal d'activité | Traçabilité des actions (qui a fait quoi, quand) |

---

### 3.2 SHOULD HAVE — Fonctionnalités Recommandées

#### 3.2.1 Commande en Ligne (Client)

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| S-01 | Menu consultable en ligne | Page web / QR code avec les prix dynamiques affichés |
| S-02 | Commande à emporter / livraison | Le client compose sa commande, voit les prix varier en temps réel |
| S-03 | Paiement en ligne | Intégration Stripe / PayPal |
| S-04 | Suivi de commande client | Statut en temps réel (préparation, prêt, en livraison) |

#### 3.2.2 Gestion des Stocks

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| S-05 | Suivi des ingrédients | Quantité en stock, seuil d'alerte |
| S-06 | Déduction automatique | Réduction du stock à chaque commande validée |
| S-07 | Alertes de rupture | Notification quand un ingrédient passe sous le seuil |

#### 3.2.3 Réservations

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| S-08 | Système de réservation | Date, heure, nombre de couverts, nom du client |
| S-09 | Confirmation automatique | E-mail / SMS de confirmation et rappel |
| S-10 | Intégration au plan de salle | Attribution automatique des tables |

#### 3.2.4 Programme de Fidélité

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| S-11 | Compte client | Historique de commandes, préférences |
| S-12 | Points de fidélité | Cumul de points selon le montant dépensé |
| S-13 | Réductions fidélité | Paliers de récompenses (ex : -10% après 500 points) |

#### 3.2.5 Tableau de Bord & Rapports

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| S-14 | Dashboard temps réel | CA du jour, commandes en cours, taux d'occupation |
| S-15 | Rapports de vente | Par période, par article, par catégorie |
| S-16 | Analyse des paliers | Statistiques sur les quantités commandées et l'impact des paliers de prix |
| S-17 | Export des données | CSV / PDF pour la comptabilité |

#### 3.2.6 Multi-langue & Accessibilité

| ID | Fonctionnalité | Détail |
|----|----------------|--------|
| S-18 | Interface multilingue | FR / EN minimum |
| S-19 | Accessibilité | Conformité WCAG 2.1 AA |

---

## 4. Exigences Non Fonctionnelles

| ID | Catégorie | Exigence |
|----|-----------|----------|
| NF-01 | **Performance** | Temps de réponse < 300 ms pour le recalcul des prix |
| NF-02 | **Performance** | Support de 50 commandes simultanées minimum |
| NF-03 | **Disponibilité** | Uptime ≥ 99.5% pendant les heures de service |
| NF-04 | **Sécurité** | Chiffrement des données (HTTPS, bcrypt pour les mots de passe) |
| NF-05 | **Sécurité** | Conformité RGPD pour les données clients |
| NF-06 | **Compatibilité** | Responsive — tablette (principal), desktop, mobile |
| NF-07 | **Sauvegarde** | Backup automatique quotidien de la base de données |
| NF-08 | **Scalabilité** | Architecture permettant l'ajout de modules (livraison, multi-site…) |

---

## 5. Architecture Technique (Recommandée)

```
┌──────────────────────────────────────────────────┐
│                   FRONT-END                      │
│  ┌─────────────┐  ┌───────────┐  ┌───────────┐  │
│  │  App Salle   │  │ App Cuisine│  │ App Client │  │
│  │  (Tablette)  │  │   (KDS)   │  │   (Web)   │  │
│  └──────┬──────┘  └─────┬─────┘  └─────┬─────┘  │
│         │               │               │        │
└─────────┼───────────────┼───────────────┼────────┘
          │               │               │
    ┌─────▼───────────────▼───────────────▼─────┐
    │              API REST / WebSocket          │
    │              (Back-end Server)              │
    ├────────────────────────────────────────────┤
    │  • Moteur de tarification dynamique        │
    │  • Gestion commandes & tables              │
    │  • Authentification & autorisations        │
    │  • Notifications temps réel                │
    └─────────────────┬──────────────────────────┘
                      │
              ┌───────▼───────┐
              │  Base de Données │
              │  (PostgreSQL)    │
              └─────────────────┘
```

### Stack Suggérée

| Couche | Technologie |
|--------|-------------|
| Front-end | React / Next.js ou Vue.js |
| Back-end | Node.js (Express/Fastify) ou Python (Django/FastAPI) |
| Base de données | PostgreSQL |
| Temps réel | WebSocket (Socket.io) |
| Paiement | Stripe API |
| Hébergement | Docker + VPS ou Cloud (AWS/GCP) |

---

## 6. Parcours Utilisateur — Tarification Dynamique

```
Client sélectionne "Pizza Margherita"
        │
        ▼
Quantité = 1 → Prix affiché : 12.00 €
        │
        ▼  [Client augmente à 3]
Quantité = 3 → Palier 2–4 détecté → Prix unitaire : 11.00 €
             → Total affiché : 33.00 €
        │
        ▼  [Client augmente à 6]
Quantité = 6 → Palier 5–9 détecté → Prix unitaire : 10.00 €
             → Total affiché : 60.00 €
        │
        ▼
Ajout au panier avec le prix calculé
        │
        ▼
Récapitulatif commande :
  Pizza Margherita × 6 ............ 60.00 €
  (prix unitaire : 10.00 € — palier 5-9)
```

---

## 7. Exemple de Ticket / Addition

```
═══════════════════════════════════════
        RESTAURANT [NOM]
        [Adresse complète]
        Tél : [Numéro]
═══════════════════════════════════════
  Table : 7          Serveur : Marie
  Date  : 14/03/2026   Heure : 20:15
───────────────────────────────────────
  Article          Qté   P.U.    Total
───────────────────────────────────────
  Pizza Margherita   6  10.00€   60.00€
    → palier 5-9 appliqué (-2€/u)

  Tiramisu            2  7.50€   15.00€
    → palier 2-4 appliqué (-0.50€/u)

  Coca-Cola 33cl      3  3.00€    9.00€
    → prix standard

  Vin rouge (verre)   1  6.00€    6.00€
    → prix standard
───────────────────────────────────────
  Sous-total HT                  75.00€
  TVA 10%                         7.50€
  TVA 20% (boissons alcool)       1.20€
───────────────────────────────────────
  TOTAL TTC                     83.70€
═══════════════════════════════════════
  Paiement : CB
  Merci de votre visite !
═══════════════════════════════════════
```

---

## 8. Planning Prévisionnel

| Phase | Contenu | Durée estimée |
|-------|---------|---------------|
| **Phase 1** — MVP | Menu + tarification dynamique + commandes + tables + facturation | 6 – 8 semaines |
| **Phase 2** — Cuisine & Rôles | KDS cuisine + authentification + rôles + journal | 3 – 4 semaines |
| **Phase 3** — En ligne | Commande client web + paiement en ligne + QR code | 4 – 5 semaines |
| **Phase 4** — Avancé | Stocks + réservations + fidélité + rapports | 4 – 6 semaines |

---

## 9. Critères de Validation

| Critère | Condition de succès |
|---------|-------------------|
| Tarification dynamique | Le prix se recalcule correctement à chaque changement de quantité |
| Commande complète | Un serveur peut prendre une commande de A à Z en moins de 2 min |
| Facturation | L'addition reflète exactement les paliers appliqués par article |
| Cuisine | Les commandes s'affichent en < 3 secondes sur l'écran cuisine |
| Paiement | Le paiement mixte (CB + espèces) fonctionne sans erreur |
| Rôles | Un serveur ne peut pas accéder aux fonctions administrateur |

---

## 10. Glossaire

| Terme | Définition |
|-------|------------|
| **Palier de prix** | Tranche de quantité associée à un prix unitaire spécifique |
| **KDS** | Kitchen Display System — écran d'affichage des commandes en cuisine |
| **Variante** | Déclinaison d'un article (taille, option) avec tarification propre |
| **MVP** | Minimum Viable Product — version minimale fonctionnelle |
| **RGPD** | Règlement Général sur la Protection des Données |

---

*Document rédigé le 14 mars 2026 — À valider par les parties prenantes avant le démarrage du développement.*
