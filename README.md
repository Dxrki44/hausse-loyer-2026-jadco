# Hausse de loyer 2026 — Collection Équinoxe (défi JADCO)

## Résultat

**Hausse de loyer 2026 : 3,25 %** (scénario central)
Fourchette : 1,77 % (bas) à 5,18 % (haut), selon l'évolution des concessions.

**Définition :** croissance annualisée à unité constante du loyer effectif (`sRentEffective`),
combinée par segment (province, régime réglementaire, renouvellement ou relocation).

**Validation (backtest 2023-2025) :** erreur absolue moyenne de 1,22 point, contre 1,55 pour
la hausse de l'année précédente et 1,40 pour la moyenne sur 3 ans.

## Exécution

1. Placer les 4 fichiers CSV fournis par JADCO dans le même dossier que `starter.ipynb` :
   `equinoxe_listings.csv`, `equinoxe_lease_history.csv`, `equinoxe_concessions.csv`,
   `equinoxe_asking_history.csv`.
   Ces fichiers ne sont **pas inclus** dans ce dépôt, par confidentialité.
2. Installer les dépendances : `pip install -r requirements.txt`
3. Ouvrir `starter.ipynb` et exécuter toutes les cellules dans l'ordre (Run All).
   Les fichiers sources ne sont jamais modifiés : toutes les transformations sont faites dans le notebook.

## Versions

- Python 3.11
- pandas, NumPy, matplotlib : versions exactes dans `requirements.txt`

## Méthode (résumé)

1. Comparaison de chaque unité à son propre bail précédent (clé `sPropCode` + `sUnitCode`),
   pour éliminer l'effet de composition.
2. Loyer effectif plutôt que contractuel, car les concessions absorbent environ la moitié
   de la hausse affichée en 2025.
3. Cinq segments selon le régime réglementaire : TAL (Québec), section F (immeubles neufs
   du Québec), The Met (Ontario, exempté de la ligne directrice).
4. Pour chaque segment : mélange entre une ancre externe (TAL ou SCHL) et la tendance interne,
   avec réglages choisis par backtest, plus un effet des concessions selon trois scénarios.

Le détail des choix, des hypothèses et des limites se trouve dans les cellules Markdown du notebook.

## Sources et outils d'IA

Voir la section **Références** à la fin du notebook (TAL, gouvernement de l'Ontario, SCHL,
articles de presse, et Claude d'Anthropic comme outil d'IA).
