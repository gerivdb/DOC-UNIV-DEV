# Corpus Chunké RAG - Documentation Technique

## Introduction

Ce document présente la structure et l'organisation du corpus chunké pour optimiser les performances RAG (Retrieval-Augmented Generation) de la base documentaire "Documentaliste Universitaire Dev".

## Structure JSONL Recommandée

### Format Standard
```json
{
  "id": "doc1-0001",
  "text": "contenu du chunk sémantique",
  "metadata": {
    "doc_id": "doc1",
    "section": "intro",
    "tags": ["rag", "ml", "architecture"],
    "source": "md",
    "parent_url": "https://github.com/gerivdb/DOC-UNIV-DEV/blob/main/SRC/glossaire-concepts.md",
    "created_at": "2025-11-03",
    "chunk_type": "definition",
    "domain": "ml"
  }
}
```

### Exemples Concrets par Document

#### Glossaire Concepts
```json
{
  "id": "glossaire-0001",
  "text": "RAG (Retrieval-Augmented Generation) : Architecture combinant retrieval (recherche) et génération pour améliorer précision LLMs via contexte externe. Composantes : Vector database, embeddings, retrieval top-k, prompt augmentation, génération.",
  "metadata": {
    "doc_id": "glossaire-concepts",
    "section": "ml-data-science",
    "tags": ["rag", "llm", "retrieval", "generation"],
    "source": "md",
    "parent_url": "https://github.com/gerivdb/DOC-UNIV-DEV/blob/main/SRC/glossaire-concepts.md",
    "created_at": "2025-11-03",
    "chunk_type": "definition",
    "domain": "ml",
    "concept": "RAG"
  }
}
```

#### Papers Fondamentaux
```json
{
  "id": "papers-0001",
  "text": "Attention Is All You Need (Vaswani et al., 2017) - NeurIPS 2017, 100,000+ citations. Impact : Fondation Transformers, base GPT/BERT/T5. Contribution : Architecture attention sans récurrence/convolution. Concepts clés : Multi-head attention, positional encoding, scaled dot-product.",
  "metadata": {
    "doc_id": "papers-fondamentaux",
    "section": "machine-learning",
    "tags": ["attention", "transformer", "nlp", "architecture"],
    "source": "md",
    "parent_url": "https://github.com/gerivdb/DOC-UNIV-DEV/blob/main/SRC/papers-fondamentaux.md",
    "created_at": "2025-11-03",
    "chunk_type": "paper_summary",
    "domain": "ml",
    "paper_title": "Attention Is All You Need",
    "citations": "100000+",
    "venue": "NeurIPS"
  }
}
```

#### Patterns Anti-Patterns
```json
{
  "id": "patterns-0001",
  "text": "Pattern API Gateway : Problème - Multiples microservices, authentification/rate-limiting répétés, frontends multiples. Solution : Proxy unique centralisant routing, auth, monitoring, transformation. Implémentation : Kong, AWS API Gateway, Traefik, Nginx.",
  "metadata": {
    "doc_id": "patterns-antipatterns",
    "section": "architecture-patterns",
    "tags": ["api-gateway", "microservices", "proxy", "routing"],
    "source": "md",
    "parent_url": "https://github.com/gerivdb/DOC-UNIV-DEV/blob/main/SRC/patterns-antipatterns.md",
    "created_at": "2025-11-03",
    "chunk_type": "pattern",
    "domain": "architecture",
    "pattern_name": "API Gateway",
    "pattern_type": "architectural"
  }
}
```

## Stratégies de Chunking par Type

### 1. Définitions (Glossaire)
- **Taille** : 200-400 caractères
- **Overlap** : 0 (définitions autonomes)
- **Splitter** : Par concept/terme
- **Tags requis** : concept, domain, definition_type

### 2. Papers Académiques
- **Taille** : 400-600 caractères
- **Overlap** : 50 caractères
- **Splitter** : Par section (abstract, contribution, impact)
- **Tags requis** : paper_title, venue, citations, domain

### 3. Patterns/Anti-Patterns
- **Taille** : 300-500 caractères
- **Overlap** : 30 caractères
- **Splitter** : Par pattern complet (problème+solution)
- **Tags requis** : pattern_name, pattern_type, domain

### 4. Ressources/Liens
- **Taille** : 250-400 caractères
- **Overlap** : 0 (ressources indépendantes)
- **Splitter** : Par ressource
- **Tags requis** : resource_type, priority, domain

## Filtres Recommandés

### Filtres Principaux
- `domain` : ["ml", "architecture", "frontend", "devops", "security"]
- `chunk_type` : ["definition", "paper_summary", "pattern", "resource", "methodology"]
- `tags` : Array de mots-clés spécifiques
- `created_at` : Date de création/mise à jour
- `source` : Type de document source

### Filtres Avancés
- `priority` : ["CRITIQUE", "HAUTE", "MOYENNE", "BASSE"]
- `citations` : Nombre de citations (pour papers)
- `pattern_type` : ["architectural", "data", "ml", "frontend", "devops"]
- `concept` : Nom du concept principal

## Métriques de Qualité

### Critères de Validation
- **Cohérence sémantique** : Chunk contient une idée complète
- **Taille optimale** : 200-600 caractères selon le type
- **Métadonnées complètes** : Tous les champs obligatoires renseignés
- **Tags pertinents** : 3-6 tags par chunk
- **Liens traçables** : parent_url valide et accessible

### Métriques de Performance
- **Recall@k** : Capacité à retrouver l'information pertinente
- **Precision@k** : Précision des résultats retournés
- **Diversity** : Variété des sources dans les top-k résultats
- **Latency** : Temps de réponse du retrieval

## Organisation des Fichiers

### Structure Recommandée
```
CORPUS/
├── chunks/
│   ├── glossaire-chunks.jsonl        # Définitions et concepts
│   ├── papers-chunks.jsonl           # Résumés académiques
│   ├── patterns-chunks.jsonl         # Patterns et anti-patterns
│   ├── resources-chunks.jsonl        # Ressources et liens
│   └── methodology-chunks.jsonl      # Guides méthodologiques
├── manifests/
│   ├── index-config.yaml            # Configuration index vectoriel
│   ├── chunking-rules.yaml          # Règles de découpage
│   └── quality-metrics.yaml         # Métriques qualité
└── evaluation/
    ├── golden-set.jsonl             # Dataset de référence
    ├── test-queries.jsonl           # Requêtes de test
    └── performance-benchmarks.json  # Benchmarks performance
```

## Bonnes Pratiques

### Création des Chunks
1. **Contextualisation** : Chaque chunk doit être compréhensible isolément
2. **Granularité** : Un concept/pattern/paper par chunk principal
3. **Enrichissement** : Métadonnées complètes pour filtrage précis
4. **Traçabilité** : Liens vers source originale toujours présents

### Maintenance
1. **Versionning** : Horodatage des chunks pour suivi évolution
2. **Validation** : Tests réguliers de pertinence et qualité
3. **Mise à jour** : Synchronisation avec modifications des sources
4. **Archivage** : Conservation des versions pour analyse diachronique

## Conclusion

Cette structure de corpus chunké optimise les performances RAG en garantissant :
- **Pertinence** : Retrieval précis grâce aux métadonnées riches
- **Traçabilité** : Liens directs vers sources GitHub
- **Scalabilité** : Structure extensible pour nouveaux domaines
- **Qualité** : Métriques de validation continues

La base documentaire DOC-UNIV-DEV devient ainsi une ressource RAG de référence pour le développement Full-Stack ML/IA.