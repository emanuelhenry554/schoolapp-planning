# SchoolApp — TP Outils d'estimation, Sheets et GitHub

Ce document centralise les valeurs du PDF du TP pour configurer manuellement GitHub Projects et recouper les estimations. Les champs personnalisés et les vues GitHub Projects doivent être créés dans l'interface web.

## 1. Projet GitHub Projects

- **Nom du projet :** SchoolApp - Gestion scolaire
- **Vue 1 :** Backlog (layout Table)
- **Vue 2 :** Kanban (layout Board, colonne = Status, filtre `no:parent-issue`)
- **Vue 3 facultative :** Roadmap (date de début = Début prévu ; date de fin = Fin prévue)
- **Status (dans cet ordre) :** Backlog, Prêt, En cours, En revue, Terminé
- **Champs personnalisés :**
  - Priorité — Single select : Must, Should, Could
  - Epic — Single select : E1 Authentification, E2 Élèves, E3 Classes et enseignants, E4 Présences, E5 Évaluations, E6 Bulletins, E7 Espace parent
  - Points — Number
  - Charge (j/h) — Number
  - Profil — Single select : CP, UX, BE, FE, QA
  - Dépend de — Text
  - Coût (FCFA) — Number
  - Début prévu — Date
  - Fin prévue — Date

## 2. Valeurs du backlog (US01 à US06)

| User Story | Priorité | Epic | Points | Dépend de |
|---|---|---|---:|---|
| US01 - Se connecter | Must | E1 Authentification | 3 | - |
| US02 - Gérer les comptes | Must | E1 Authentification | 5 | US01 |
| US03 - Inscrire un élève | Must | E2 Élèves | 8 | US05 |
| US04 - Rechercher un élève | Should | E2 Élèves | 3 | US03 |
| US05 - Gérer classes et enseignants | Must | E3 Classes et enseignants | 5 | US02 |
| US06 - Faire l'appel | Must | E4 Présences | 5 | US03, US05 |

Mettre le statut **Backlog** sur les 12 User Stories. Les stories US07 à US12 restent sans priorité/epic/points pour cette étape du TP.

**Contrôles des points :** E1 = 8 ; E2 = 11 ; E3 = 5 ; E4 = 5 ; total US01 à US06 = 29 points.

## 3. Sous-tâches US06 (valeurs à saisir dans les champs du projet)

| Ticket | Profil | Charge (j/h) | Coût (FCFA) | Lot | Début prévu | Fin prévue | Dépend de |
|---|---|---:|---:|---|---|---|---|
| US06-T1 - API des présences (#13) | BE | 2.6 | 91000 | L4 | 26/01/2027 | 10/03/2027 | Après US03, US05 |
| US06-T2 - Écran d'appel de la classe (#14) | FE | 3.0 | 105000 | L5 | 03/02/2027 | 02/03/2027 | US06-T1 (DD) |
| US06-T3 - Gestion des justificatifs d'absence (#15) | BE | 1.6 | 56000 | L4 | 26/01/2027 | 10/03/2027 | US06-T1 |
| US06-T4 - Tests de l'appel (#16) | QA | 1.5 | 37500 | L6 | 11/03/2027 | 12/04/2027 | US06-T1, US06-T2, US06-T3 |

**Contrôles US06 :** charge = 8.7 j/h ; coût = 289500 FCFA. Par profil : BE = 4.2 j/h / 147000 FCFA ; FE = 3.0 j/h / 105000 FCFA ; QA = 1.5 j/h / 37500 FCFA.

> Important : créer les tickets ne garantit pas qu'ils soient rattachés techniquement comme « sub-issues » à US06. Vérifier la section **Sub-issues** du ticket #6 et utiliser **Add sub-issue** pour relier les tickets #13 à #16 si nécessaire. Le compteur attendu est « 0 / 4 ».

## 4. TP C — Estimation PERT (11 tâches)

| ID | US | Tâche | Profil | O | M | P | Dépend de |
|---|---|---|---|---:|---:|---:|---|
| US04-T1 | US04 | API de recherche et de filtres | BE | 1.0 | 2.0 | 3.0 | Après US03 |
| US04-T2 | US04 | Écrans liste et fiche élève | FE | 1.5 | 2.0 | 3.0 | US04-T1 (DD) |
| US04-T3 | US04 | Tests de la recherche | QA | 0.5 | 1.0 | 1.5 | US04-T1, US04-T2 |
| US05-T1 | US05 | API des classes, matières et affectations | BE | 2.0 | 3.0 | 4.0 | Après US02 |
| US05-T2 | US05 | Écrans classes et affectations | FE | 2.0 | 3.0 | 4.0 | US05-T1 (DD) |
| US05-T3 | US05 | Règles de gestion (capacité d'une classe) | BE | 0.5 | 1.0 | 2.0 | US05-T1 |
| US05-T4 | US05 | Tests des classes | QA | 1.0 | 1.5 | 2.0 | US05-T1, US05-T2, US05-T3 |
| US06-T1 | US06 | API des présences | BE | 1.5 | 2.5 | 4.0 | Après US03, US05 |
| US06-T2 | US06 | Écran d'appel de la classe | FE | 2.0 | 3.0 | 4.0 | US06-T1 (DD) |
| US06-T3 | US06 | Gestion des justificatifs d'absence | BE | 1.0 | 1.5 | 2.5 | US06-T1 |
| US06-T4 | US06 | Tests de l'appel | QA | 1.0 | 1.5 | 2.0 | US06-T1, US06-T2, US06-T3 |

Dans Google Sheets français :
- H2 : `=ARRONDI((E2+4*F2+G2)/6;1)`, recopier jusqu'à H12.
- I2 : `=G2-E2`, recopier jusqu'à I12.
- L2:L4 (totaux US) : `=SOMME.SI.ENS($H$2:$H$12;$B$2:$B$12;K2)`
- O2:O4 (totaux profils) : `=SOMME.SI.ENS($H$2:$H$12;$D$2:$D$12;N2)`
- H14 : `=SOMME(H2:H12)`
- Validation de données D2:D12 : CP, UX, BE, FE, QA.
- Mise en forme conditionnelle I2:I12 : supérieur ou égal à 2.

**Contrôles TP C :** US04 = 5.1 ; US05 = 8.6 ; US06 = 8.7 ; BE = 10.3 ; FE = 8.1 ; QA = 4.0 ; total = 22.4 j/h ; 5 cellules avec écart ≥ 2.

## 5. TP D — Valeurs finales à contrôler dans le modèle Excel d'origine

Le fichier source `SchoolApp_Modele_Estimation_a_completer.xlsx` est nécessaire pour préserver les 53 tâches et les paramètres préremplis. Les résultats attendus du PDF sont :

- Charge totale des tâches : 126.3 j/h
- Coût des tâches : 4 219 000 FCFA
- Total coûts humains avec pilotage : 4 664 500 FCFA
- Coûts non humains : 470 000 FCFA
- Base : 5 134 500 FCFA
- Réserve de 15 % : 770 175 FCFA
- **Budget global : 5 904 675 FCFA**
- Durée : 78 jours ouvrés
- Fin prévue : 29/04/2027
- Fin avec réserve : 12/05/2027
- Synthèse : quatre contrôles « OK »

Ces valeurs sont des contrôles cibles, pas une preuve que le classeur D a déjà été calculé.