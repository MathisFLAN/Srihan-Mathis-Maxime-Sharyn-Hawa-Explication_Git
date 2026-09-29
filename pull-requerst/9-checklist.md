# 9. Checklists

## 9.1 Checklist de l'auteur

### Avant de créer la PR

- [ ] La branche cible est correcte
- [ ] La branche contient uniquement le travail nécessaire
- [ ] Les changements non liés ont été retirés
- [ ] Le code est formaté
- [ ] Le lint passe
- [ ] Les tests pertinents passent
- [ ] Le diff a été relu
- [ ] Les commits sont compréhensibles
- [ ] Aucun secret ou donnée sensible n'est présent
- [ ] La branche est suffisamment à jour

### Description

- [ ] Le problème est expliqué
- [ ] La solution est expliquée
- [ ] Les tests effectués sont indiqués
- [ ] Les risques ou points d'attention sont signalés
- [ ] Le ticket est référencé si nécessaire
- [ ] Les changements nécessitant une attention particulière sont indiqués

### Avant le merge

- [ ] Tous les commentaires importants ont été traités
- [ ] Les checks CI sont verts
- [ ] Les approvals requis sont présents
- [ ] Le diff final a été vérifié
- [ ] La PR est toujours cohérente avec son objectif

---

## 9.2 Checklist du reviewer

### Compréhension

- [ ] Je comprends le problème résolu
- [ ] Je comprends la solution
- [ ] Le périmètre est cohérent

### Code

- [ ] Le comportement est correct
- [ ] Les cas limites sont pris en compte
- [ ] Les erreurs sont correctement gérées
- [ ] L'architecture reste cohérente
- [ ] Le code est maintenable
- [ ] Aucun problème évident de sécurité n'est introduit
- [ ] Les performances sont acceptables pour le contexte

### Tests

- [ ] Les tests couvrent le comportement principal
- [ ] Les cas importants sont couverts
- [ ] Les tests existants restent pertinents
- [ ] La CI est verte

### Review

- [ ] Mes commentaires sont précis
- [ ] Je distingue les problèmes bloquants des suggestions
- [ ] Je n'impose pas une préférence personnelle sans raison technique
- [ ] J'évite de bloquer la PR sur des détails automatisables

---

## 9.3 Exemple de template de PR

```markdown
## Contexte

<!-- Pourquoi cette PR est-elle nécessaire ? -->

## Changements

<!-- Résumer les changements principaux -->

- 
- 
- 

## Tests

- [ ] Tests unitaires
- [ ] Tests d'intégration
- [ ] Tests manuels
- [ ] Aucun test supplémentaire nécessaire

## Points d'attention

<!-- Y a-t-il quelque chose que les reviewers doivent particulièrement vérifier ? -->

## Risques

<!-- Décrire les risques connus et/ou le plan de rollback -->

## Ticket

<!-- Lien ou référence vers le ticket -->
```

---

## 9.4 Exemple de checklist automatisable

Une partie du processus peut être automatisée :

```text
PR ouverte
   ↓
Lint ────────────┐
Tests ───────────┤
Build ───────────┤
Security scan ───┤
                 ↓
             Checks OK
                 ↓
              Review
                 ↓
              Approval
                 ↓
               Merge
```

Plus les contrôles sont automatisés, plus les reviewers peuvent consacrer leur temps aux décisions qui nécessitent réellement du jugement humain.
