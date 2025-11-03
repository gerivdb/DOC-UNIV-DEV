# Brain ↔ DOC-UNIV-DEV — Intelligence Bridge

Résumé exécutif
Le présent document définit l’architecture, les flux, les métriques et la feuille de route qui instaurent une boucle d’intelligence bidirectionnelle entre le dépôt BRAIN (recherche empirique, cognition opérationnelle) et DOC-UNIV-DEV (base documentaire académique et de production). Objectif : transformer continuellement les insights du terrain en standards documentés et, symétriquement, convertir la connaissance structurée en accélérateurs d’implémentation mesurables.

1) Principes directeurs
- Symbiose théorie ↔ pratique : toute découverte (BRAIN) devient un artefact documentaire actionnable (DOC), toute structure documentaire (DOC) devient hypothèses/expériences et outillage (BRAIN).
- RAG-first & reproductibilité : chaque artefact est indexable (manifeste, métadonnées) et testable (playbooks, jeux d’essai) pour alimenter un pipeline RAG/évaluation.
- Traçabilité bout-en-bout : « du commit à la citation » — lien systématique entre expérimentations, références, décisions et implémentations.
- Minimal coupling, maximal leverage : contrats clairs (schemas, API, formats), surfaces de changement réduites, réutilisation élevée.

2) Architecture logique de la symbiose
Couches et contrats
- Source empirique (BRAIN)
  - Insights expérimentaux : notebooks, scripts, rapports d’expériences, benchmarks, prototypes.
  - Énoncés de patterns/antipatterns issus d’observation, checklists d’opérabilité.
  - Sorties normalisées : JSON de résultats, tableaux de métriques, traces, manifestes d’expérimentation.
- Base documentaire (DOC-UNIV-DEV)
  - Canon documentaire : glossaire-concepts.md, papers-fondamentaux.md, patterns-antipatterns.md, ressources-50-complet.md.
  - Extension RAG : corpus-chunke-rag.md (JSONL), manifeste-index-rag.yaml, guide-chunking.md, ontologie-rag.yaml.
  - Bridge symbiose : index-github-space.md, brain-doc-intelligence-bridge.md (présent), ecoystem-doc-integration.md, research-implementation-loop.md.
- Plan de contrôle (Control Plane)
  - Governance : conventions de nommage, schémas de métadonnées, politiques de revue et de validation.
  - Automation : workflows CI/CD GitHub (lint docs, valider schémas, construire index RAG, publier artefacts), jobs de sync Space↔GitHub.
  - Observabilité : métriques de couverture, freshness, réutilisation, qualité RAG, latence de propagation.

Interfaces et formats
- Manifeste d’expérimentation (BRAIN → DOC)
  - brain_experiment.yaml
    - id, titre, domaines, hypothèses, protocole, datasets, paramètres, artefacts, sorties, métriques, verdicts, liens PR/issues.
- Carte de connaissance (DOC → BRAIN)
  - doc_knowledge_card.yaml
    - id, concepts, références, patterns, anti-patterns, questions ouvertes, playbooks, slots d’expérimentation proposés.
- Corpus RAG (bidirectionnel)
  - JSONL chunké avec : id, source, domaine, granularité, embeddings_policy, citations, tags qualité, version.

3) Flux de travail (workflows) bidirectionnels
Flux A — Insight-to-Documentation (BRAIN → DOC)
1. Expérimentation BRAIN produit brain_experiment.yaml, résultats JSON, notebooks, tableaux.
2. CI « Extract+Normalize » : 
   - Valider schémas, extraire métriques clés, générer fiches synthèses.
   - Ouvrir PR sur DOC avec : mise à jour patterns-antipatterns.md, ajout de fiches dans corpus-chunke-rag.md, enrichissement glossaire/papers.
3. Revue documentaire (DOC) : 
   - Alignement ontologie-rag.yaml, référencement croisé, qualité éditoriale, niveau d’évidence.
4. Intégration : 
   - Build index RAG, bump manifeste-index-rag.yaml, publier artefacts, tag release documentaire.

Flux B — Knowledge-to-Implementation (DOC → BRAIN)
1. Détection d’écarts/leviers depuis DOC (gaps, TODO, opportunités patterns).
2. Génération doc_knowledge_card.yaml (slots d’expérimentation avec hypothèses et critères d’acceptation).
3. CI « Seed Experiments » : créer issues/branches templates dans BRAIN avec playbooks, datasets de départ et métriques cibles.
4. Exécution expérimentale, itérations, retour vers Flux A.

Flux C — Sync Space ↔ GitHub (pont navigation)
- Job planifié : 
  - Pousser index RAG vers Space, remonter signaux Space (search logs, feedback) dans GitHub issues.
  - Maintenir parité index, détecter drift entre ontologie et usages réels.

4) Métriques et SLO d’excellence
Couverture et fraicheur
- Coverage_concepts = |concepts documentés| / |concepts cibles| (objectif ≥ 0,8 trimestriel).
- Freshness_90p = âge P90 des artefacts critiques (objectif ≤ 45 jours).
Qualité recherche→doc
- Traceability_rate = % d’items DOC avec lien expérimentation BRAIN (objectif ≥ 0,9).
- Evidence_score = pondération (paper, benchmark, prod signal) par item (objectif ≥ 0,7).
Qualité doc→implémentation
- Adoption_rate = nb d’expériences BRAIN déclenchées depuis fiches DOC / trimestre (objectif croissant).
- Pattern_success = % de patterns validés en prod/bench (objectif ≥ 0,7).
Qualité RAG
- Retrieval@K (gold QA), Faithfulness (judge), Context-Utilization, Hallucination rate, Time-to-Answer.
- Ontology_coverage = % des relations de l’ontologie supportant des réponses correctes.
Flux et cadence
- Lead time Insight→Doc (P50/P90), Lead time Doc→Experiment, Cycle time PR Docs.
- PR throughput, Review latency, Change failure rate documentaire (reverts).

5) Gouvernance et rôles
- Mainteneur DOC (Editor-in-Chief) : cohérence éditoriale, ontologie, releases documentaire.
- Mainteneur BRAIN (Research Lead) : qualité méthodologique, reproductibilité, intégrité des datasets.
- Owner Bridge (Integrator) : CI/CD cross-repos, schémas, politiques de synchronisation, observabilité.
- Contributeurs (Authors/Reviewers) : règles de PR, checklist de qualité (liens, citations, tests RAG).

6) Implémentation technique
Dossiers et fichiers (résumé)
- DOC-UNIV-DEV/
  - glossaire-concepts.md, papers-fondamentaux.md, patterns-antipatterns.md, ressources-50-complet.md
  - corpus-chunke-rag.md (JSONL), manifeste-index-rag.yaml, guide-chunking.md, ontologie-rag.yaml
  - bridge/
    - brain-doc-intelligence-bridge.md (ce fichier)
    - ecoystem-doc-integration.md
    - research-implementation-loop.md
- BRAIN/
  - experiments/<area>/<id>/brain_experiment.yaml, results.json, notebook.ipynb
  - seeds/doc_knowledge_card.yaml, playbooks/, datasets/

CI/CD (exemples de jobs)
- validate-docs: lint Markdown, vérifier liens/citations, valider schémas YAML.
- build-index-rag: chunking, embeddings, construction manifeste-index-rag.yaml, publication index.
- sync-bridge: synchronisation Space↔GitHub (index, feedback), mise à jour ecoystem-doc-integration.
- seed-experiments: à partir de doc_knowledge_card.yaml, générer issues/branches dans BRAIN.

Schémas (extraits)
- brain_experiment.yaml
  id: BE-YYYY-NNN
  domain: [RAG, LLM, VDB, Embeddings, …]
  hypothesis: …
  protocol: …
  datasets: …
  parameters: …
  metrics: [retrieval@k, faithfulness, latency, cost]
  artifacts: [notebook, results.json, plots]
  decisions: [accepted, rejected, partial]
  links: { pr: …, issue: … }
- doc_knowledge_card.yaml
  id: DK-YYYY-NNN
  concepts: [ … ]
  references: [doi/url]
  patterns: [ … ]
  anti_patterns: [ … ]
  open_questions: [ … ]
  playbooks: [ … ]
  acceptance_criteria: { metrics: …, thresholds: … }

7) Roadmap d’implémentation (90 jours)
Phase 0 — Mise en place (Semaine 1–2)
- Créer bridge/ et fichiers seed. Définir schémas YAML. Configurer linters et validations.
- Mettre en place workflows validate-docs, build-index-rag, seed-experiments.

Phase 1 — Première boucle (Semaine 3–6)
- Ingest de 10 expérimentations BRAIN (RAG/LLM/VDB). Générer PR DOC correspondantes.
- Construire l’index RAG initial. Activer Space bridge et feedback loop.

Phase 2 — Extension & Quality (Semaine 7–10)
- Couverture glossaire 150+ concepts, 20+ papers annotés, 40+ patterns.
- Bench RAG avec panel de 100 requêtes or, mise en place judge auto.

Phase 3 — Industrialisation (Semaine 11–13)
- SLO/alerting sur freshness, traceability, retrieval@k. Dashboards.
- Génération systématique des slots d’expérimentation depuis gaps DOC.

8) Checklists qualité
PR DOC
- [ ] Traçabilité vers brain_experiment.yaml et résultats.
- [ ] Citations et liens vérifiés, taxonomie conforme ontologie.
- [ ] Mise à jour manifeste-index-rag.yaml si impact.
PR BRAIN
- [ ] Protocole reproductible, seeds/datasets versionnés, métriques minimales.
- [ ] Export résultats normalisés, artefacts publiés.
- [ ] Lien retour vers items DOC impactés.

9) Risques & atténuations
- Drift entre ontologie et usages : monitoring ontology_coverage + revue mensuelle.
- Dette éditoriale : freshness SLO + rotation d’Editor duty.
- Fragmentation formats : schémas versionnés + tests de validation CI.
- Hallucinations RAG : garde-fous (retrieval strict, citations, judges) et boucles d’évaluation.

10) Definition of Done (Bridge)
- CI verte (validate-docs, build-index-rag, sync-bridge, seed-experiments).
- Métriques de base en place, dashboards, alerting.
- Au moins 5 cycles complets A→B et B→A exécutés, documentés et traçables.

Annexes
- Référentiels : glossaire-concepts.md, papers-fondamentaux.md, patterns-antipatterns.md.
- Contrats : brain_experiment.yaml, doc_knowledge_card.yaml.
- Opérations : guide-chunking.md, manifeste-index-rag.yaml, ontologie-rag.yaml.
