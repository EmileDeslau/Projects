# Proposition Commerciale

## Application de Gestion de Restaurant avec Tarification Dynamique

---

> **Destinataire** : _[Nom du client]_  
> **Émetteur** : _[Votre société]_  
> **Date** : 14 mars 2026  
> **Référence** : PROP-RESTO-2026-001  
> **Validité** : 30 jours  

---

## 1. Résumé du Projet

Vous souhaitez une application de gestion de restaurant complète incluant :

- Gestion du menu avec **tarification dynamique par quantité**
- Prise de commande en salle et en ligne
- Gestion des tables et du plan de salle
- Facturation avec TVA configurable
- Écran cuisine (KDS) pour le suivi des préparations
- Système de rôles et permissions

Le prix de chaque article varie automatiquement selon la quantité commandée par le client, via un système de **paliers configurables**.

---

## 2. Détail des Modules & Tarification

### Phase 1 — MVP (Cœur de l'application)

| Réf. | Fonctionnalité | Détail | Jours | Prix HT |
|------|----------------|--------|------:|--------:|
| | **MODULE : GESTION DU MENU** | | | |
| M-01 | Création / modification / suppression d'articles | CRUD complet avec nom, description, catégorie, image, statut | 3 | 900 € |
| M-02 | Paliers de prix par quantité | Interface de configuration des tranches tarifaires par article | 5 | 1 500 € |
| M-03 | Gestion des catégories | Entrées, Plats, Desserts, Boissons, Formules… | 1.5 | 450 € |
| M-04 | Variantes d'article | Taille, cuisson, suppléments avec tarification propre | 3 | 900 € |
| M-05 | Activation / désactivation d'article | Masquer un plat en rupture de stock | 0.5 | 150 € |
| M-06 | Affichage du prix dynamique | Recalcul en temps réel selon la quantité sélectionnée | 4 | 1 200 € |
| | **Sous-total Menu** | | **17** | **5 100 €** |
| | | | | |
| | **MODULE : COMMANDES** | | | |
| M-07 | Créer une commande | Association table ou mode emporter/livraison | 2 | 600 € |
| M-08 | Ajouter des articles avec recalcul prix | Sélection, quantité, recalcul automatique par palier | 4 | 1 200 € |
| M-09 | Modifier une commande en cours | Ajout/retrait d'articles, changement de quantités | 2 | 600 € |
| M-10 | Annuler une commande | Annulation totale/partielle avec motif | 1.5 | 450 € |
| M-11 | Workflow de statuts | En attente → Préparation → Prête → Servie → Clôturée | 2 | 600 € |
| M-12 | Notes et allergies | Instructions spéciales, tags allergènes | 1 | 300 € |
| | **Sous-total Commandes** | | **12.5** | **3 750 €** |
| | | | | |
| | **MODULE : TABLES** | | | |
| M-13 | Plan de salle configurable | Placement des tables, capacité, vue graphique | 4 | 1 200 € |
| M-14 | Statuts des tables | Libre / Occupée / Réservée / À nettoyer | 1.5 | 450 € |
| M-15 | Lien table ↔ commande | Association automatique et vue depuis le plan | 1.5 | 450 € |
| | **Sous-total Tables** | | **7** | **2 100 €** |
| | | | | |
| | **MODULE : FACTURATION** | | | |
| M-16 | Génération de l'addition | Détail par article avec palier appliqué, TVA, total | 3 | 900 € |
| M-17 | Modes de paiement | CB, Espèces, Ticket restaurant, paiement mixte | 2 | 600 € |
| M-18 | Division de l'addition | Split par convive ou par article | 2 | 600 € |
| M-19 | Impression / envoi ticket | Imprimante thermique, e-mail, PDF | 2.5 | 750 € |
| M-20 | TVA configurable | Taux par catégorie, sur place vs emporter | 1.5 | 450 € |
| | **Sous-total Facturation** | | **11** | **3 300 €** |
| | | | | |
| | **TOTAL PHASE 1** | | **47.5 j** | **14 250 €** |

---

### Phase 2 — Cuisine & Rôles

| Réf. | Fonctionnalité | Détail | Jours | Prix HT |
|------|----------------|--------|------:|--------:|
| | **MODULE : CUISINE (KDS)** | | | |
| M-21 | Écran de commandes en cuisine | Affichage temps réel, tri, code couleur | 4 | 1 200 € |
| M-22 | Marquage « Prêt » | Validation par le cuisinier, notification serveur | 2 | 600 € |
| | **MODULE : AUTHENTIFICATION** | | | |
| M-23 | Connexion sécurisée | Login/mot de passe + code PIN rapide | 3 | 900 € |
| M-24 | Rôles et permissions | Admin, Serveur, Cuisinier, Caissier | 3 | 900 € |
| M-25 | Journal d'activité | Audit log complet, non modifiable | 2 | 600 € |
| | **TOTAL PHASE 2** | | **14 j** | **4 200 €** |

---

### Phase 3 — Commande en Ligne

| Réf. | Fonctionnalité | Détail | Jours | Prix HT |
|------|----------------|--------|------:|--------:|
| S-01 | Menu en ligne + QR code | Page publique responsive avec prix dynamiques | 4 | 1 200 € |
| S-02 | Commande emporter / livraison | Panier interactif avec prix en temps réel | 5 | 1 500 € |
| S-03 | Paiement en ligne | Intégration Stripe / PayPal (PCI DSS) | 4 | 1 200 € |
| S-04 | Suivi de commande client | Page de suivi temps réel + notifications | 3 | 900 € |
| | **TOTAL PHASE 3** | | **16 j** | **4 800 €** |

---

### Phase 4 — Fonctionnalités Avancées

| Réf. | Fonctionnalité | Détail | Jours | Prix HT |
|------|----------------|--------|------:|--------:|
| | **MODULE : STOCKS** | | | |
| S-05 | Suivi des ingrédients | CRUD ingrédients, quantités, seuils d'alerte | 3 | 900 € |
| S-06 | Déduction automatique | Réduction du stock à chaque commande | 2.5 | 750 € |
| S-07 | Alertes de rupture | Notifications + désactivation auto si rupture | 1.5 | 450 € |
| | **MODULE : RÉSERVATIONS** | | | |
| S-08 | Système de réservation | Date, heure, couverts, gestion des conflits | 3 | 900 € |
| S-09 | Confirmation auto | E-mail/SMS de confirmation et rappel J-1 | 2 | 600 € |
| S-10 | Intégration plan de salle | Attribution automatique des tables | 2 | 600 € |
| | **MODULE : FIDÉLITÉ** | | | |
| S-11 | Compte client | Historique, préférences enregistrées | 2 | 600 € |
| S-12 | Points de fidélité | Cumul automatique selon le montant | 2 | 600 € |
| S-13 | Réductions par paliers | Récompenses configurables | 1.5 | 450 € |
| | **MODULE : RAPPORTS** | | | |
| S-14 | Dashboard temps réel | CA, commandes, taux d'occupation | 3 | 900 € |
| S-15 | Rapports de vente | Par période, article, catégorie + graphiques | 3 | 900 € |
| S-16 | Analyse des paliers de prix | Statistiques d'impact des tarifs dégressifs | 2 | 600 € |
| S-17 | Export CSV / PDF | Pour la comptabilité, planification auto | 1.5 | 450 € |
| | **MODULE : UX** | | | |
| S-18 | Interface multilingue | Français / Anglais minimum | 2 | 600 € |
| S-19 | Accessibilité WCAG 2.1 | Contraste, clavier, lecteur d'écran | 2 | 600 € |
| | **TOTAL PHASE 4** | | **33 j** | **9 900 €** |

---

## 3. Récapitulatif Financier

| Phase | Description | Jours | Montant HT |
|-------|-------------|------:|-----------:|
| **Phase 1** | MVP — Menu, commandes, tables, facturation | 47.5 | 14 250 € |
| **Phase 2** | Cuisine & Rôles | 14 | 4 200 € |
| **Phase 3** | Commande en ligne | 16 | 4 800 € |
| **Phase 4** | Fonctionnalités avancées | 33 | 9 900 € |
| | | | |
| | **TOTAL PROJET** | **110.5 j** | **33 150 € HT** |
| | TVA (20%) | | 6 630 € |
| | **TOTAL TTC** | | **39 780 € TTC** |

> **Taux journalier appliqué** : 300 € HT / jour  
> **Prix minimum par fonctionnalité** : 150 € HT  

---

## 4. Options de Livraison

Le client peut choisir de ne réaliser que certaines phases :

| Option | Phases incluses | Montant HT | Montant TTC |
|--------|----------------|----------:|-----------:|
| **Essentiel** | Phase 1 uniquement | 14 250 € | 17 100 € |
| **Standard** | Phase 1 + 2 | 18 450 € | 22 140 € |
| **Complet** | Phase 1 + 2 + 3 | 23 250 € | 27 900 € |
| **Premium** | Toutes les phases | 33 150 € | 39 780 € |

---

## 5. Modalités de Paiement

| Étape | Moment | Pourcentage | Montant (Premium) |
|-------|--------|:----------:|---------:|
| Acompte | Signature du devis | 30% | 9 945 € HT |
| Jalons intermédiaires | Livraison de chaque phase | 50% (répartis) | 16 575 € HT |
| Solde | Recette finale | 20% | 6 630 € HT |

---

## 6. Délais de Livraison

| Phase | Durée estimée | Livraison prévisionnelle |
|-------|:------------:|:------------------------:|
| Phase 1 — MVP | 6–8 semaines | Juin 2026 |
| Phase 2 — Cuisine & Rôles | 3–4 semaines | Juillet 2026 |
| Phase 3 — En ligne | 4–5 semaines | Août 2026 |
| Phase 4 — Avancé | 4–6 semaines | Octobre 2026 |

---

## 7. Ce qui est inclus

- Développement complet de l'application
- Tests fonctionnels et techniques
- Documentation technique et utilisateur
- Déploiement sur votre infrastructure
- Formation utilisateurs (1 demi-journée par phase)
- **Garantie corrective : 3 mois** après la livraison finale

## 8. Ce qui n'est pas inclus

- Hébergement et noms de domaine (à la charge du client)
- Matériel (tablettes, imprimantes thermiques, écrans cuisine)
- Maintenance évolutive au-delà de la garantie
- Contenu du menu (textes, photos des plats)
- Intégration avec des systèmes tiers non spécifiés

---

## 9. Conditions Générales

- Toute modification de périmètre fera l'objet d'un avenant chiffré
- Les délais sont indicatifs et dépendent de la réactivité du client pour les validations
- Le code source reste propriété du client après paiement intégral

---

## 10. Signatures

| | Client | Prestataire |
|---|--------|-------------|
| **Nom** | _________________________ | _________________________ |
| **Fonction** | _________________________ | _________________________ |
| **Date** | _________________________ | _________________________ |
| **Signature** | | |
| | | |
| **Option choisie** | ☐ Essentiel  ☐ Standard  ☐ Complet  ☐ Premium | |

---

*Ce document constitue une offre commerciale. Il devient contractuel après signature des deux parties.*
