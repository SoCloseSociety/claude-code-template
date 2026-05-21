# Templates Claude Code : Prompts Optimisés Anti-Gaspillage

> Le but : remplacer les phrases ouvertes ("continue d'améliorer", "vérifie tout", "termine les phases") par des templates qui imposent un **scope**, un **format de sortie**, et un **critère de stop**.

---

## Principes de base (à graver)

1. **Toujours définir un scope** : file, folder, function. Jamais "le projet".
2. **Toujours imposer le format de sortie** : diff, table, JSON, checklist.
3. **Toujours définir le critère de done** : sinon Claude Code continue indéfiniment.
4. **Audit AVANT fix** : un audit coûte 10x moins qu'un refactor non maîtrisé.
5. **Plan AVANT code** : un plan validé évite 3 rounds d'aller-retour.
6. **One-shot vs itératif** : décide au début et préfixe.

---

## 1. AUDIT / DIAGNOSTIC

### AUDIT-1 : Audit rapide d'un module
```
AUDIT [module/path]
Pas de fix. Sortie rapport markdown <200 lignes avec line numbers, classé:
P0 = bugs critiques
P1 = code smells
P2 = risques sécurité
P3 = dette technique
```

### AUDIT-2 : Audit avant nouvelle feature
```
AUDIT PRE-FEATURE
Feature: [description en 2 lignes]
Réponds sans toucher au code:
1. Files à modifier
2. Risques d'impact sur autres modules
3. Tests existants à mettre à jour
4. Complexité (S/M/L/XL)
5. Bloqueurs potentiels
```

### AUDIT-3 : Cartographie module inconnu
```
MAP [folder]
Donne-moi:
1. Arbre des dépendances (max 2 niveaux)
2. Entry points
3. Side effects (DB, HTTP, FS, env)
4. Fichiers >300 lignes (candidats refactor)
Sortie markdown, pas de code.
```

---

## 2. TESTS

### TEST-1 : Couverture ciblée
```
TEST [file/function]
Génère uniquement les tests MANQUANTS pour:
- Edge cases
- Error paths  
- Boundary conditions
Pytest, AAA pattern, mocks pour DB/Redis/HTTP. Pas de tests triviaux (getters, etc.).
```

### TEST-2 : TDD inverse
```
TDD-REVERSE pour [function]
1. Liste tous les scénarios (happy + edge + error)
2. Génère les tests
3. Run pytest et donne-moi le report
Ne touche PAS au code source. Je veux voir ce qui casse.
```

### TEST-3 : Smoke test endpoint
```
SMOKE [endpoint path] [method]
5 requêtes httpx:
1. Happy path
2. Auth manquante
3. Payload invalide
4. Rate limit dépassé
5. Dépendance down (mock)
Sortie: tableau status/expected/actual.
```

### TEST-4 : Regression avant deploy
```
REGRESS
Liste les 5 scénarios critiques de cette app (basé sur le code).
Pour chaque: 1 test E2E.
Run tout. Sortie pass/fail seulement.
```

---

## 3. DEBUG / CORRECTION

### FIX-1 : Bug isolé
```
FIX
Symptôme: [description]
File: [path]:[line]
Logs:
[coller logs ici]

Étapes:
1. Reproduis localement
2. Root cause en 3 lignes
3. Patch minimal (PAS de refactor opportuniste)
4. Test de régression
Output: diff + explication 3 lignes max.
```

### FIX-2 : Bug systémique
```
DEBUG SYSTEMIC
Pattern observé: [description]
Hypothèse: [si tu en as une, sinon "à trouver"]
1. Grep le codebase pour pattern similaire
2. Liste TOUTES les occurrences (file:line)
3. Propose fix générique
4. STOP et attends confirmation avant d'appliquer
```

### FIX-3 : Erreur opaque
```
DIAGNOSE (pas de fix)
Error:
[stack trace complète]

Sortie:
1. Explique l'erreur en 5 lignes
2. Top 3 causes probables
3. Pour chaque: comment vérifier en <30s
4. Recommande la plus probable
```

### FIX-4 : Flaky test
```
UNFLAKE [test path]
Run le test 10x.
Si flaky:
1. Identifie source (race, ordre, sleep, état partagé)
2. Propose fix
3. Re-run 10x pour valider
```

---

## 4. REFACTOR / AMÉLIORATION

### REFACTOR-1 : Refactor ciblé
```
REFACTOR [file/function]
Objectif: [ex: réduire complexity, extraire logic, DRY entre X et Y]
Contraintes:
- Comportement identique (tests doivent passer)
- Pas de nouvelle dépendance
- Diff <100 lignes
Output: avant/après + justification 3 lignes.
```

### REFACTOR-2 : Découpage de gros module
```
SPLIT [file]
Le file dépasse [N] lignes.
1. Propose architecture cible (3 lignes max)
2. STOP, attends mon GO
3. Si validé: exécute, garde les imports publics compatibles
```

### REFACTOR-3 : Chasse à la dette
```
DEBT-KILL
Scope: [folder]
Trouve sans supprimer:
- Imports inutilisés
- Fonctions non appelées
- TODO/FIXME datés >1 mois
- console.log / print de debug
- Commentaires zombies
Liste tout. J'approuve ensuite la suppression.
```

### REFACTOR-4 : Migration de pattern
```
MIGRATE
From pattern: [ancien, ex: callback]
To pattern: [nouveau, ex: async/await]
Scope: [folder]
1. Liste toutes les occurrences
2. Migre par batch de 5 files
3. Run tests entre chaque batch
4. Stop au premier fail
```

---

## 5. DESIGN UI / UX

### UI-1 : Composant React from spec
```
COMPONENT [name]
Props: [TypeScript interface]
Stack: React 19 + TS + Tailwind (pas shadcn sauf si je demande)
Inclus obligatoirement:
- Loading state
- Error state
- Empty state
- Accessibility (aria, focus management, keyboard nav)
- Responsive mobile-first
Pas de lib externe sans validation.
```

### UI-2 : Design review
```
UI-REVIEW [component file]
Évalue (pas de réécriture):
1. Hierarchy visuelle
2. Spacing (système 4/8px cohérent ?)
3. Contraste WCAG AA
4. Touch targets >44px mobile
5. États interactifs (hover, focus, active, disabled, loading)
6. Dark mode si présent
Sortie: checklist + 3 suggestions concrètes max.
```

### UI-3 : Itération design (2 variantes max)
```
ITERATE [component]
Direction: [ex: plus dense / plus aéré / plus brutaliste / plus minimal]
Préserve: [features critiques]
Produis exactement 2 variantes en code, pas 3.
Format: diff côte à côte avec rationale 2 lignes par variante.
```

### UI-4 : Polish final
```
POLISH [component]
Checklist:
- Transitions/animations cohérentes (durée, easing)
- Empty states avec illustration ou message utile
- Loading skeletons (pas de spinner générique)
- Error states actionnables (CTA pour retry)
- Microcopy révisé (pas de "Submit", préfère verbes spécifiques)
Diff seulement.
```

---

## 6. PERFORMANCE

### PERF-1 : Audit perf
```
PERF-AUDIT [endpoint/component]
Identifie (pas de fix):
1. N+1 queries (ORM)
2. Re-renders inutiles (React)
3. Bundle bloat (imports lourds)
4. Sync calls dans contexte async
5. Manque d'index DB
Sortie: top 3 issues avec impact estimé (latence, taille, etc.).
```

### PERF-2 : Optim ciblée et mesurée
```
OPTIMIZE [function]
Métrique cible: [ex: <100ms p95]
1. Profile AVANT (timeit/cProfile/React Profiler), donne baseline
2. Applique UNE optim
3. Mesure delta
4. Répète tant que cible non atteinte
5. STOP dès que cible atteinte (ne pas surfitter)
```

### PERF-3 : Bundle slim
```
BUNDLE-SLIM
1. Analyse bundle actuel (taille par chunk)
2. Top 5 dépendances les plus lourdes
3. Pour chaque: alternative plus légère OU lazy load OU tree-shake
4. Propose, n'applique pas.
```

---

## 7. SÉCURITÉ

### SEC-1 : Audit sécu général
```
SEC-AUDIT [scope]
Check:
1. SQL injection (raw queries, f-strings dans SQL)
2. XSS (rendering user input sans sanitize)
3. Secrets hardcodés (regex sur API keys, tokens)
4. Auth bypass (endpoints sans @require_auth)
5. CORS trop permissif
6. Rate limiting absent sur endpoints publics
7. PII dans les logs
Output: tableau severity/file:line/fix proposé.
```

### SEC-2 : Hardening endpoint
```
HARDEN [endpoint]
Ajoute sans changer le comportement métier:
- Validation Pydantic stricte (constr, conint, etc.)
- Auth + permission check explicite
- Rate limit Redis (par IP + par user)
- Logging structuré sans PII
- Error responses uniformes (pas de stack trace leak)
Diff seulement.
```

### SEC-3 : Audit dépendances
```
DEPS-AUDIT
1. Run npm audit / pip-audit / cargo audit
2. Liste CVE par severity
3. Pour chaque high+: chemin de mitigation (bump, replace, accept)
Pas de upgrade automatique.
```

---

## 8. CONTINUATION / PHASES (le gros remplaçant de "continue")

### PHASE-1 : Reprise structurée (remplace "continue")
```
RESUME
Dernier état stable: [phase N, ce qui marche]
Prochaine étape attendue: [phase N+1, titre]
AVANT d'écrire du code:
1. Confirme ta compréhension de N+1 en 3 lignes
2. Liste les files que tu vas toucher
3. STOP, attends mon GO
```

### PHASE-2 : Plan multi-phase
```
PLAN
Objectif final: [description en 3 lignes]
Découpe en phases atomiques (chacune testable indépendamment):
Pour chaque phase: titre + critère done + tests associés
Max 6 phases. Pas de code, juste le plan en markdown.
```

### PHASE-3 : Exécution d'une phase
```
EXEC PHASE [N]: [titre]
Critère de done: [liste mesurable]
Tests à passer: [liste]
Règles:
- Travaille jusqu'à done
- Si bloqué >2 tentatives: STOP et demande
- Ne devine pas, ne refactor pas ce qui marche
- À la fin: résumé 5 lignes + diff stats
```

### PHASE-4 : Check de fin de phase
```
PHASE-CHECK [N]
1. Tous les critères de done atteints ? (liste yes/no)
2. Tests passent ? (run + output)
3. Pas de régression sur phases précédentes ?
4. Dette ajoutée pendant cette phase ?
Si tout vert: prêt pour phase N+1. Sinon: liste blockers.
```

---

## 9. DOCUMENTATION

### DOC-1 : Doc d'une fonction
```
DOC [function]
Format: docstring Google style
Inclus: args, returns, raises, 1 example minimal
Pas plus de 15 lignes. Pas de blabla sur la complexité Big-O sauf si non-trivial.
```

### DOC-2 : README de module
```
README [folder]
Sections obligatoires (et seulement celles-là):
1. Purpose (3 lignes)
2. Install/setup
3. Usage example (1 bloc code qui marche)
4. API public (table: function/signature/purpose)
5. Gotchas connus
Max 100 lignes. Pas d'emoji.
```

### DOC-3 : Architecture decision record
```
ADR
Decision: [ex: passer de Celery à Arq]
Format ADR standard:
- Context
- Options considérées (>=2)
- Decision
- Conséquences (positives + négatives)
- Status (proposed/accepted/superseded)
Max 1 page.
```

---

## 10. MODE ÉCONOMIQUE (ONE-SHOT)

### Principes
- Préfixe `ONE-SHOT:` pour signaler "pas d'itération attendue"
- Donne le contexte exact (files, lignes, exemples)
- Impose le format de sortie
- Bannit "explore", "réfléchis en profondeur", "analyse"

### Template ONE-SHOT
```
ONE-SHOT
Task: [action précise en 1 ligne]
Context: [files exacts, ou snippet]
Output: [format imposé: diff / json / table]
Règle: aucune question. Si ambiguïté, choisis la convention standard du projet et note-la en 1 ligne.
```

---

## Anti-patterns à bannir

À ne plus jamais écrire :

| Phrase bateau | Pourquoi c'est cher | Remplacer par |
|---|---|---|
| "Continue d'améliorer le design" | Subjectif, infini | UI-3 ITERATE avec direction précise |
| "Vérifie tout" | Scope infini | AUDIT-1 avec module + P0/P1/P2 |
| "Termine les phases suivantes" | Pas de critère done | PHASE-3 EXEC PHASE N avec done |
| "Corrige tous les bugs" | Peut refactor opportunément | FIX-1 ciblé + AUDIT préalable |
| "Améliore les modules" | Trop vague | REFACTOR-1 ciblé avec objectif |
| "Fais en sorte que ce soit propre" | Définition variable | DEBT-KILL avec checklist |
| "Optimise" | Sans métrique = sur-ingénierie | PERF-2 avec cible chiffrée |

---

## Combos puissants (workflows complets)

### Combo "Phase Done"
```
1. PLAN  →  2. EXEC PHASE N  →  3. TEST  →  4. PHASE-CHECK  →  5. RESUME N+1
```

### Combo "Feature Sûre"
```
1. AUDIT PRE-FEATURE  →  2. PLAN  →  3. EXEC  →  4. TEST  →  5. SEC-AUDIT
```

### Combo "Bug Fix Propre"
```
1. DIAGNOSE  →  2. FIX  →  3. TEST régression  →  4. DEBT-KILL alentour
```

### Combo "Refactor Sûr"
```
1. AUDIT module  →  2. TEST couverture actuelle  →  3. REFACTOR  →  4. TEST re-run
```

### Combo "Performance Mesurée"
```
1. PERF-AUDIT  →  2. baseline (profile)  →  3. OPTIMIZE itératif  →  4. STOP cible atteinte
```

---

## Bonus : Stop-words magiques

Mots à inclure pour calmer Claude Code et éviter le sur-zèle :

- **"STOP et attends"** : empêche l'exécution sans validation
- **"diff seulement"** : empêche les explications verbeuses
- **"pas de refactor opportuniste"** : empêche les changements hors-scope
- **"si bloqué, demande"** : empêche les devinettes coûteuses
- **"<N lignes"** : impose la concision
- **"format: [structure]"** : impose la structure de sortie
- **"sans toucher au code"** : isole un audit pur

---

## Convention de préfixes (utile pour tes scripts/automations)

| Préfixe | Mode | Crédits |
|---|---|---|
| `AUDIT` | Read-only analyse | $ |
| `DIAGNOSE` | Read-only debug | $ |
| `PLAN` | Read-only stratégie | $ |
| `MAP` | Read-only exploration | $ |
| `FIX` | Write ciblé | $$ |
| `TEST` | Write tests | $$ |
| `REFACTOR` | Write ciblé | $$ |
| `EXEC PHASE` | Write large | $$$ |
| `MIGRATE` | Write large | $$$ |
