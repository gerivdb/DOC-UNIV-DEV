# ECOYSTEM-1 — Intégration documentaire inter-dépôts (17 dépôts)

Statut: actif | Portée: cross-repo | Responsable: DOC-UNIV-DEV | Bridge: BRAIN ↔ ECOYSTEM

## 1) Objectifs
- Unifier la stratégie documentaire sur 17 dépôts ECOYSTEM-1
- Assurer la propagation cohérente des patterns, décisions, et standards
- Rendre reproductible la veille, la R&D et l’implémentation via un RAG documentaire
- Réduire la dérive documentaire, accélérer l’onboarding, améliorer la qualité

Indicateurs clés:
- Taux de couverture README/ADR/CHANGELOG ≥ 95%
- Latence de propagation d’un pattern ≤ 48h
- Endettement documentaire (lint) = 0 critique / sprint

## 2) Périmètre des 17 dépôts et rôles
- Core Knowledge: DOC-UNIV-DEV (source of truth documentaire)
- Intelligence: BRAIN (insights, expériences, boucles d’évaluation)
- Implémentations: 17 dépôts ECOYSTEM-1 (services, libs, front, ops)
- Ponts: index-github-space.md, brain-doc-intelligence-bridge.md, manifeste-index-rag.yaml

Chaque dépôt doit exposer:
- README.md (narratif, run, arch, liens de décision)
- ADR/ (Architecture Decision Records)
- /docs/ (guides, how-to, références API)
- CHANGELOG.md (Keep a Changelog)
- .clinerules et lint-doc pour qualité

## 3) Gouvernance documentaire (modèle RACI)
- Owner: DOC-UNIV-DEV
- Accountable: Maintainers de chaque dépôt
- Consulted: BRAIN (research), FLUENCE (innovation), Security, Ops
- Informed: Stakeholders projet

Rituels:
- Weekly Doc Sync (30 min): décisions, patterns, endettement
- Monthly Pattern Review: consolidation cross-repo
- Quarterly Doc Audit: conformité, gaps, obsolescence

## 4) Artefacts standards et structure
- README.md: Purpose, Quickstart, Architecture, Observability, Security, Links
- ADR-YYYYMMDD-<slug>.md: Contexte, Décision, Alternatives, Conséquences
- CONTRIBUTING.md: conventions, outillage, test, doc build
- CHANGELOG.md: SemVer, sections Added/Changed/Fixed/Removed/Deprecated/Security
- docs/:
  - guides/: tutoriels orientés tâche
  - references/: API/CLI contracts
  - patterns/: playbooks, best-practices
  - operations/: runbooks, SLO/SLA, incident handbook

## 5) Pipeline de propagation des patterns (PatternOps)
1. Origination (BRAIN insights, incidents, audits, PoC)
2. Normalisation (DOC-UNIV-DEV: ADR + pattern.md)
3. Publication (manifestes, index, liens bidirectionnels)
4. Propagation (PRs automatisées multi-repo)
5. Adoption (merge, release, doc site regénéré)
6. Vérification (lint-doc, checks CI, qualité)
7. Rétroaction (metrics, feedback, boucle RAG)

Automatisation:
- GitHub Actions reusable workflows: lint-doc.yml, adr-check.yml, changelog-guard.yml
- Templates ISSUE/PR: bug.md, feature.md, doc-update.md
- CODEOWNERS pour docs/ et ADR/

## 6) Stratégie RAG documentaire unifiée
- Sources: DOC-UNIV-DEV (glossaire, patterns, papers), dépôts ECOYSTEM-1 (README, ADR, docs/)
- Manifeste: manifeste-index-rag.yaml (sélecteurs de fichiers, poids, fraîcheur)
- Chunking: guide-chunking.md (titres sémantiques, fenêtres contextuelles, liens croisés)
- Ontologie: ontologie-rag.yaml (Concept ↔ Pattern ↔ ADR ↔ Implémentation ↔ Runbook)
- Indexation: corpus-chunke-rag.md (JSONL + métadonnées repo, version, hash)
- Bridge: index-github-space.md (navigation bidirectionnelle, Space ↔ GitHub)

Qualité RAG:
- Couverture concepts ≥ 90%
- Drift ≤ 2% / trimestre (détecté par evals sémantiques)
- Grounding strict sur sources versionnées

## 7) Taxonomie des patterns et anti-patterns
Catégories principales:
- RAG Production, LLM Orchestration/Eval, Vector DB, Embeddings
- EDA/CQRS, Microservices, Distributed Systems, Clean Architecture
- CI/CD, Observability, Security, Performance
- Frontend/UX, State Management, PWA

Format pattern.md:
- Problème, Contexte, Forces/Contraintes
- Solution (diagrammes, variantes), Trade-offs
- Implémentations de référence (liens code)
- Checklist d’adoption
- Indicateurs de succès
- Anti-patterns associés

## 8) Coordination inter-dépôts (Cross-Repo)
- Board unique: Projet GitHub « ECOYSTEM-1 DocOps » avec colonnes (Backlog, Doing, Review, Adopted)
- Labels harmonisés: documentation, architecture, research, security, breaking-change
- Milestones synchronisées par release train (mensuel)
- Liaisons bidirectionnelles: Issue master DOC-UNIV-DEV ↔ Issues enfants par dépôt
- Backports et forward-ports documentés (ADR-Backport, ADR-Forward)

Escalation paths:
- Bloqueur d’adoption > 48h → Maintainer + Owner DOC-UNIV-DEV
- Divergence ADR entre dépôts → RFC de convergence sous 5 jours

## 9) Qualité et conformité
- Lint-doc: titres, TOC, orthographe, liens valides, images alt, schémas vérifiés
- CI checks obligatoires pour merge: lint-doc, adr-check, changelog-guard
- Security: classification des docs, secrets scanning, SBOM docs/operations/sbom.md
- Accessibilité: WCAG pour docs web, contrastes, navigation clavier
- Internationalisation: fr/en avec indicateurs de parité

## 10) Observabilité documentaire
- Metrics: nb ADR par dépôt, adoption rate pattern, temps propagation, erreurs lint
- Tableaux de bord: Insights → Dashboards « Doc Quality »
- Alerting: GitHub Checks + notifications (maintainers)

## 11) Plan de déploiement
Phase 0 (Semaine 0): cadrage, modèles templates, workflows réutilisables
Phase 1 (Semaines 1-2): instrumentation lint-doc + adr-check sur 5 dépôts pilotes
Phase 2 (Semaines 3-4): propagation à 12 dépôts restants + RAG initial
Phase 3 (Semaine 5): audit, correctifs, documentation finale, baseline metrics

Critères de succès:
- 17/17 dépôts avec README/ADR/CHANGELOG conformes
- 100% workflows docs actifs, 0 échec critique
- Recherche RAG répondante (< 1.5s P95) sur 80% queries internes

## 12) Playbooks clés
- Mise à jour pattern: créer ADR, PR multi-repo, mettre à jour pattern.md, bump versions
- Nouvel ADR transversal: RFC → discussion → vote → propagation
- Incident doc: ouvrir issue « doc-incident », post-mortem en 48h, action items tracés

## 13) Annexes et ressources
- Modèles: templates/adr.md, templates/pattern.md, templates/changelog.md
- Références: papers-fondamentaux.md, patterns-antipatterns.md, glossaire-concepts.md
- Bridges: brain-doc-intelligence-bridge.md, index-github-space.md

---
Dernière mise à jour: auto via CI (commit hash et date)
