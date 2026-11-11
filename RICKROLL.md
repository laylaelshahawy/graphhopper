# Rickroll sur échec de test — GraphHopper

## Objectif

Configurer un workflow GitHub Actions qui affiche un Rickroll lorsqu'un test GraphHopper échoue.

## Implémentation

Le fichier `.github/workflows/rickroll.yml` exécute `ReaderElementTest` avec Maven sur Java 17.

Une étape conditionnelle utilise `if: failure()` pour afficher le message et le lien du Rickroll lorsqu'une étape précédente échoue. Le workflow conserve son statut d'échec.

## Validation

Deux scénarios ont été vérifiés sur GitHub Actions :

| Scénario | Résultat |
|---|---|
| Tests réussis (3 tests, 0 échec) | Workflow réussi, Rickroll ignoré |
| Échec simulé avec `exit 1` après les tests | Workflow échoué, Rickroll affiché |

La seconde vérification valide le déclenchement conditionnel après un échec du workflow, sans constituer un échec réel d'assertion Java.

## Branches

- `tache3-rickroll` : version définitive du workflow.
- `demo-rickroll-failure` : démonstration de l'échec contrôlé.

Dépôt : https://github.com/laylaelshahawy/graphhopper