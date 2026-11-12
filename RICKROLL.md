# Rickroll sur échec de test — GraphHopper

## Objectif

Configurer GitHub Actions afin d'afficher un Rickroll lorsqu'un test du projet GraphHopper échoue, en utilisant une action réutilisable.

## Implémentation

Le workflow `.github/workflows/rickroll.yml` exécute la classe `ReaderElementTest` du module `core` avec Maven et Java 17.

L'action réutilisable se trouve dans `.github/actions/rickroll/action.yml`. Il s'agit d'une action composite qui affiche un message GitHub Actions et le lien du Rickroll.

Le workflow appelle cette action avec :

```yaml
- name: Rickroll on test failure
  if: ${{ failure() && steps.tests.outcome == 'failure' }}
  uses: ./.github/actions/rickroll
```

Cette condition vérifie que l'étape de tests Maven a échoué. L'action Rickroll s'exécute alors, sans masquer l'échec du workflow.

## Validation

| Scénario | Résultat |
|---|---|
| Tests `ReaderElementTest` réussis (3 tests, 0 échec) | Workflow réussi, action Rickroll ignorée |
| Échec simulé avec `exit 1` après les tests Maven | Workflow échoué, action Rickroll exécutée |

Le deuxième scénario démontre que l'action composite est bien appelée lorsque l'étape de test se termine en échec.

Il s'agit d'un **échec simulé**, et non d'une assertion Java réellement échouée.

## Branches

- `tache3-rickroll` : version principale de la solution.
- `demo-reusable-rickroll` : démonstration du déclenchement de l'action réutilisable.

## Dépôt

https://github.com/laylaelshahawy/graphhopper

