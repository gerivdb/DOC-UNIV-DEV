# 📚 Glossaire Documentaliste R&D - Concepts Clés

## ML & Data Science

### Retrieval-Augmented Generation (RAG)
**Définition** : Architecture combinant retrieval (recherche) et génération pour améliorer précision LLMs via contexte externe.  
**Composantes** : Vector database, embeddings, retrieval (top-k), prompt augmentation, génération.  
**Use cases** : Q&A sur corpus privé, documentation technique, knowledge bases.  
**Alternatives** : Fine-tuning, prompt engineering pur, knowledge graphs.

### Embeddings
**Définition** : Représentation vectorielle dense de texte/images/audio dans espace latent sémantique.  
**Modèles** : BGE, E5, OpenAI ada-002, Sentence-BERT, CLIP (multimodal).  
**Métriques** : Cosine similarity, dot product, euclidean distance.  
**Best practices** : Normalisation, dimension 384-1536, chunking cohérent.

### MLOps
**Définition** : DevOps appliqué au machine learning (versioning, CI/CD, monitoring modèles).  
**Stack typique** : MLflow, Weights & Biases, DVC, Airflow, Kubeflow.  
**Problématiques** : Data drift, model decay, reproducibilité, scalabilité inference.  
**Métriques** : Latency p95, throughput, accuracy in production, drift detection.

### Transfer Learning
**Définition** : Réutilisation connaissances pré-entraînées sur tâche proche.  
**Approches** : Fine-tuning, feature extraction, adapter layers, LoRA.  
**Modèles fondation** : BERT, GPT, T5, LLaMA, Stable Diffusion.  
**Trade-offs** : Coût compute vs performance, catastrophic forgetting.

---

## Architecture & Backend

### Event-Driven Architecture
**Définition** : Communication asynchrone via événements entre services découplés.  
**Patterns** : Event Sourcing, CQRS, Saga pattern, Event Notification.  
**Technologies** : Kafka, RabbitMQ, AWS EventBridge, NATS.  
**Avantages** : Scalabilité, résilience, découplage temporel.  
**Challenges** : Eventual consistency, debugging distribué, ordering.

### CQRS (Command Query Responsibility Segregation)
**Définition** : Séparation read/write models pour optimiser chaque use case.  
**Composantes** : Command handlers, query handlers, projections, event store.  
**Use cases** : Systèmes haute scalabilité, audit trail, analytics complexes.  
**Complexité** : Synchronisation read/write, eventual consistency.

### Microservices
**Définition** : Architecture décomposée en services indépendants déployables.  
**Patterns** : API Gateway, Service Mesh, Circuit Breaker, Sidecar.  
**Technologies** : Kubernetes, Docker, Istio, Kong, Consul.  
**Trade-offs** : Overhead opérationnel vs scalabilité/agilité.

### API REST vs GraphQL
**REST** : Endpoints fixes, over-fetching/under-fetching, stateless, cache HTTP.  
**GraphQL** : Schema-driven, requêtes flexibles, single endpoint, N+1 problem.  
**Choix** : REST = APIs publiques simples ; GraphQL = frontends complexes, agrégation.

---

## Frontend & UX

### Server-Side Rendering (SSR)
**Définition** : Génération HTML côté serveur pour SEO et performance initial load.  
**Frameworks** : Next.js, Nuxt.js, SvelteKit, Remix.  
**Trade-offs** : TTFB vs interactivité, hydration cost, complexité cache.

### Progressive Web Apps (PWA)
**Définition** : Web apps offline-first avec service workers, installables.  
**Composantes** : Service worker, manifest.json, cache strategies, push notifications.  
**Use cases** : Apps mobiles low-budget, connectivité instable.

### WebAssembly (WASM)
**Définition** : Format binaire portable haute-performance pour le web.  
**Langages** : Rust, C++, Go, AssemblyScript.  
**Use cases** : Gaming, traitement image/vidéo, crypto, edge computing.

---

## DevOps & Infrastructure

### Infrastructure as Code (IaC)
**Définition** : Gestion infra via code versionné (déclaratif ou impératif).  
**Outils** : Terraform, Pulumi, CloudFormation, Ansible.  
**Best practices** : Modules réutilisables, state management, drift detection.

### Kubernetes
**Définition** : Orchestrateur containers pour déploiement, scaling, management.  
**Concepts** : Pods, Services, Deployments, StatefulSets, Ingress, Operators.  
**Écosystème** : Helm, ArgoCD, Prometheus, Istio, Kustomize.  
**Complexité** : Courbe apprentissage, overhead small apps.

### Observability (O11y)
**Définition** : Mesurer état interne via outputs externes (logs, metrics, traces).  
**Piliers** : Logs (ELK), Metrics (Prometheus), Traces (Jaeger/Tempo).  
**Outils** : Datadog, New Relic, Grafana, OpenTelemetry.  
**KPIs** : Latency, error rate, saturation, traffic (RED/USE methods).

---

## Sécurité

### Zero Trust Architecture
**Définition** : Principe "never trust, always verify" pour chaque requête.  
**Composantes** : Identity verification, least privilege, micro-segmentation.  
**Technologies** : OAuth2, mTLS, service mesh policies, RBAC.

### Supply Chain Security
**Définition** : Sécurisation dépendances et build pipeline.  
**Outils** : Dependabot, Snyk, SBOM, Sigstore, cosign.  
**Menaces** : Dependency confusion, typosquatting, compromised packages.

---

## Recherche & Veille

### h-index
**Définition** : Métrique impact chercheur (h papers avec ≥h citations chacun).  
**Usage** : Identifier auteurs influents, évaluer output recherche.  
**Limites** : Bias domaines, favorise ancienneté, gaming possible.

### Peer Review
**Définition** : Évaluation par pairs experts avant publication.  
**Types** : Single-blind, double-blind, open review.  
**Plateformes** : OpenReview, Publons, PeerJ.

### Preprint
**Définition** : Version paper avant peer-review pour dissémination rapide.  
**Serveurs** : ArXiv, bioRxiv, SSRN, OSF Preprints.  
**Trade-off** : Vitesse vs validation qualité.

---

## Performance & Optimisation

### Caching Strategies
**Types** : CDN, browser cache, application cache, database query cache.  
**Patterns** : Cache-aside, write-through, write-behind, refresh-ahead.  
**Invalidation** : TTL, event-driven, LRU, manual purge.

### Database Indexing
**Types** : B-tree, Hash, GiST, GIN, full-text, vector (HNSW, IVF).  
**Trade-offs** : Read speed vs write overhead, storage cost.  
**Best practices** : Covering indexes, partial indexes, analyze query plans.

---

**Usage** : Référence rapide concepts clés, alignement vocabulaire équipe, onboarding nouveaux devs.
