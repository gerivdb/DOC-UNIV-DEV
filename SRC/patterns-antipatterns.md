# 🎯 Patterns & Anti-Patterns - Guide Pratique Dev

## Architecture Patterns

### Pattern: API Gateway
**Problème** : Multiples microservices, authentification/rate-limiting répétés, frontends multiples.  
**Solution** : Proxy unique centralisant routing, auth, monitoring, transformation.  
**Implémentation** : Kong, AWS API Gateway, Traefik, Nginx.  
**Anti-pattern** : Gateway devient monolithe logique, single point of failure.

### Pattern: Circuit Breaker
**Problème** : Service downstream fail → cascade failures.  
**Solution** : Détection failures, ouverture circuit, fallback, tentatives progressives.  
**Implémentation** : Resilience4j, Hystrix, Polly, Envoy.  
**Métriques** : Error rate threshold, timeout, half-open retry.

### Pattern: Saga Pattern
**Problème** : Transactions distribuées sans 2PC.  
**Solution** : Séquence transactions locales + compensation en cas d'échec.  
**Types** : Choreography (events), Orchestration (coordinator).  
**Exemple** : Order → Payment → Inventory → Shipping (rollback si Payment fail).

### Anti-Pattern: Distributed Monolith
**Symptômes** : Microservices couplés, déploiements synchronisés, shared database.  
**Impact** : Complexité microservices sans bénéfices découplage.  
**Solution** : Bounded contexts clairs, communication async, database per service.

---

## Data Patterns

### Pattern: Event Sourcing
**Problème** : Perte historique états, audit trail, debug difficile.  
**Solution** : Stocker événements immuables, reconstruire état via replay.  
**Technologies** : EventStore, Kafka, Axon Framework.  
**Trade-offs** : Complexité, projections asynchrones, storage croissant.

### Pattern: CQRS
**Problème** : Read/write conflits, scaling différencié.  
**Solution** : Modèles séparés optimisés (write = normalized, read = denormalized).  
**Use case** : Analytics lourdes + writes fréquents.  
**Couplage** : Souvent avec Event Sourcing.

### Anti-Pattern: God Object
**Symptômes** : Classe/table contenant trop responsabilités, méthodes/colonnes >20.  
**Impact** : Maintenance cauchemar, couplage fort, tests difficiles.  
**Solution** : Décomposition SRP (Single Responsibility Principle), refactoring.

### Pattern: Repository Pattern
**Problème** : Logique persistence éparpillée, tests difficiles.  
**Solution** : Abstraction accès données, interface unique par aggregate.  
**Implémentation** : `UserRepository`, `OrderRepository` avec interface.  
**Bénéfices** : Testabilité (mock), changement DB transparent.

---

## ML Patterns

### Pattern: Feature Store
**Problème** : Features calculées multiples fois, inconsistance train/serve.  
**Solution** : Centralisation features réutilisables avec versioning.  
**Technologies** : Feast, Tecton, AWS Feature Store, Hopsworks.  
**Composantes** : Offline store (training), online store (inference), registry.

### Pattern: Model Registry
**Problème** : Versions modèles perdues, déploiements opaques.  
**Solution** : Catalog centralisé avec metadata, lineage, versions.  
**Outils** : MLflow, Weights & Biases, Neptune.ai.  
**Metadata** : Metrics, hyperparams, dataset version, artifacts.

### Anti-Pattern: Hidden Technical Debt in ML
**Symptômes** : Data dependencies non-documentées, glue code, pipeline fragiles.  
**Sources** : Google paper "Machine Learning: The High-Interest Credit Card".  
**Solutions** : Tests data quality, monitoring drift, refactoring régulier.

### Pattern: A/B Testing for Models
**Problème** : Déploiement modèle = risque dégradation UX.  
**Solution** : Split traffic, métriques business comparées, rollback automatique.  
**Implémentation** : Feature flags, canary deployment, shadow mode.

---

## Frontend Patterns

### Pattern: Compound Components
**Problème** : Props drilling, composants trop configurables.  
**Solution** : Composants parent/enfants partageant state implicite.  
**Exemple** : `<Tabs><Tab>...</Tab><Tab>...</Tab></Tabs>`.  
**Framework** : React Context, Vue provide/inject.

### Pattern: Render Props / Hooks
**Problème** : Réutilisation logique sans héritage.  
**Solution** : Fonction recevant render function ou custom hooks.  
**Exemple** : `useFetch`, `useAuth`, `useLocalStorage`.  
**Évolution** : Hooks remplacent HoC et render props en React.

### Anti-Pattern: Prop Drilling
**Symptômes** : Props passées 3+ niveaux sans usage intermédiaire.  
**Impact** : Maintenance difficile, couplage implicite.  
**Solutions** : Context API, state management (Redux, Zustand), composition.

### Pattern: Optimistic UI
**Problème** : Latency réseau dégrade UX.  
**Solution** : Update UI immédiat + rollback si erreur serveur.  
**Use case** : Likes, comments, drag-and-drop.  
**Complexité** : Gestion conflits, states temporaires.

---

## DevOps Patterns

### Pattern: Blue-Green Deployment
**Problème** : Downtime pendant déploiement.  
**Solution** : Deux environnements identiques, switch traffic instantané.  
**Avantages** : Rollback rapide, testing production-like.  
**Coût** : Infrastructure doublée.

### Pattern: Canary Deployment
**Problème** : Déploiement risqué sur 100% traffic.  
**Solution** : Déploiement progressif (5% → 25% → 50% → 100%).  
**Monitoring** : Error rate, latency, business metrics.  
**Rollback** : Automatique si seuils dépassés.

### Anti-Pattern: Configuration Drift
**Symptômes** : Environnements prod/staging/dev divergent.  
**Impact** : Bugs environment-specific, debugging difficile.  
**Solutions** : IaC (Terraform), immutable infrastructure, GitOps.

### Pattern: Sidecar Container
**Problème** : Cross-cutting concerns (logging, monitoring, proxy).  
**Solution** : Container auxiliaire dans même pod.  
**Use case** : Service mesh (Envoy), log shipping, secrets injection.  
**K8s** : Native avec pod multi-containers.

---

## Security Patterns

### Pattern: Defense in Depth
**Principe** : Multiples couches sécurité (réseau, app, data, identity).  
**Exemple** : Firewall + WAF + RBAC + encryption at rest + MFA.  
**Philosophie** : Pas de single point of failure sécurité.

### Pattern: Principle of Least Privilege
**Définition** : Accès minimum nécessaire pour fonctionner.  
**Implémentation** : RBAC granulaire, temporary credentials, scope limité.  
**Outils** : AWS IAM, Kubernetes RBAC, Vault.

### Anti-Pattern: Security by Obscurity
**Symptômes** : Cacher endpoints, encoder ≠ chiffrer, secret hardcodés.  
**Impact** : Fausse sécurité, vulnérabilités découvertes rapidement.  
**Solution** : Crypto forte, auth robuste, audit externe.

---

## Performance Patterns

### Pattern: Database Connection Pooling
**Problème** : Overhead création connexions DB.  
**Solution** : Pool connexions réutilisables, idle timeout.  
**Config** : Min/max connections, timeout, validation query.  
**Outils** : HikariCP, PgBouncer, Redis connection pooling.

### Pattern: Lazy Loading
**Problème** : Chargement données inutiles.  
**Solution** : Chargement à la demande (images, modules, data).  
**Frontend** : React.lazy, intersection observer, code splitting.  
**Backend** : JPA lazy fetching, pagination.

### Anti-Pattern: N+1 Query Problem
**Symptômes** : 1 query + N queries en boucle (ORM naïf).  
**Impact** : Performance catastrophique à grande échelle.  
**Solutions** : Eager loading, join queries, DataLoader (GraphQL).

### Pattern: Caching Strategy
**Layers** : CDN → Browser → Application → Database query cache.  
**Invalidation** : TTL, cache-aside, write-through, event-driven.  
**Trade-offs** : Freshness vs performance, memory cost.

---

**Usage** : Référence décisions architecture, code reviews, mentoring juniors, éviter erreurs classiques.
