# 🔬 Papers Fondamentaux - Sélection Annotée

## Machine Learning & Deep Learning

### "Attention Is All You Need" (Vaswani et al., 2017)
**Venue** : NeurIPS 2017  
**Citations** : 100,000+  
**Impact** : Fondation Transformers, base GPT/BERT/T5.  
**Contribution** : Architecture attention sans récurrence/convolution.  
**Concepts clés** : Multi-head attention, positional encoding, scaled dot-product.  
**Implémentation** : https://github.com/tensorflow/tensor2tensor  
**Lire si** : NLP, LLMs, architectures modernes.

### "BERT: Pre-training of Deep Bidirectional Transformers" (Devlin et al., 2018)
**Venue** : NAACL 2019  
**Citations** : 80,000+  
**Impact** : Transfer learning NLP, fine-tuning paradigm.  
**Contribution** : Pre-training bidirectionnel MLM + NSP.  
**Applications** : Q&A, NER, classification, semantic search.  
**Code** : https://github.com/google-research/bert  
**Lire si** : NLP tasks, embeddings textuels.

### "Deep Residual Learning" (He et al., 2015)
**Venue** : CVPR 2016  
**Citations** : 150,000+  
**Impact** : Réseaux très profonds (>100 layers) viables.  
**Contribution** : Skip connections, identity mappings.  
**Applications** : Vision, classification, detection, segmentation.  
**Architectures** : ResNet-50, ResNet-101, ResNeXt.  
**Lire si** : Computer vision, architectures CNN.

---

## Systèmes Distribués

### "Designing Data-Intensive Applications" (Kleppmann, 2017)
**Type** : Livre (référence majeure)  
**Impact** : Bible architectures distribuées modernes.  
**Chapitres clés** : Replication, Partitioning, Transactions, Consensus.  
**Concepts** : CAP theorem, eventual consistency, linearizability.  
**Cas pratiques** : Cassandra, Kafka, Elasticsearch design decisions.  
**Lire si** : Architecture backend, systèmes scalables.

### "In Search of an Understandable Consensus Algorithm" (Raft, Ongaro & Ousterhout, 2014)
**Venue** : USENIX ATC 2014  
**Citations** : 10,000+  
**Impact** : Alternative Paxos plus simple à comprendre/implémenter.  
**Contribution** : Leader election, log replication, safety.  
**Implémentations** : etcd, Consul, CockroachDB.  
**Lire si** : Distributed consensus, high availability.

### "Dynamo: Amazon's Highly Available Key-value Store" (DeCandia et al., 2007)
**Venue** : SOSP 2007  
**Citations** : 8,000+  
**Impact** : Base Cassandra, Riak, DynamoDB.  
**Contribution** : Consistent hashing, vector clocks, eventual consistency.  
**Trade-offs** : Availability over consistency (AP in CAP).  
**Lire si** : NoSQL, distributed databases.

---

## MLOps & Production ML

### "Hidden Technical Debt in Machine Learning Systems" (Sculley et al., 2015)
**Venue** : NeurIPS 2015  
**Citations** : 5,000+  
**Impact** : Révèle complexité ML en production.  
**Problèmes** : Data dependencies, glue code, configuration debt.  
**Recommandations** : Testing, monitoring, reproducibility.  
**Lire si** : MLOps, déploiement modèles production.

### "Machine Learning: The High-Interest Credit Card" (Sculley et al., 2014)
**Venue** : SE4ML Workshop  
**Impact** : Suite du précédent, focus technical debt.  
**Concepts** : Entanglement, undeclared consumers, pipeline jungles.  
**Solutions** : Abstraction, isolation, versioning.  
**Lire si** : Architecture ML systems, maintenabilité.

---

## Recherche d'Information & RAG

### "Dense Passage Retrieval for Open-Domain QA" (Karpukhin et al., 2020)
**Venue** : EMNLP 2020  
**Citations** : 3,000+  
**Impact** : Retrieval neural vs BM25, base RAG moderne.  
**Contribution** : Dual-encoder architecture, hard negatives mining.  
**Applications** : Q&A systems, semantic search.  
**Code** : https://github.com/facebookresearch/DPR  
**Lire si** : RAG, embeddings, retrieval.

### "Retrieval-Augmented Generation for Knowledge-Intensive NLP" (Lewis et al., 2020)
**Venue** : NeurIPS 2020  
**Citations** : 4,500+  
**Impact** : Formalisation RAG architecture.  
**Contribution** : Retriever + generator end-to-end trainable.  
**Résultats** : Amélioration significative Q&A, fact checking.  
**Code** : https://github.com/huggingface/transformers (RAG models)  
**Lire si** : RAG implementation, knowledge-intensive tasks.

---

## Optimisation & Performance

### "Flash Attention" (Dao et al., 2022)
**Venue** : NeurIPS 2022  
**Citations** : 2,000+  
**Impact** : Attention 3-5x plus rapide, memory efficient.  
**Contribution** : Tiling, recomputation, IO-awareness.  
**Applications** : Long-context LLMs, training efficiency.  
**Code** : https://github.com/Dao-AILab/flash-attention  
**Lire si** : Training LLMs, optimization CUDA.

### "LoRA: Low-Rank Adaptation of Large Language Models" (Hu et al., 2021)
**Venue** : ICLR 2022  
**Citations** : 3,500+  
**Impact** : Fine-tuning efficient LLMs sans retrainer tous poids.  
**Contribution** : Adapter layers low-rank, paramètres réduits 10,000x.  
**Applications** : Customization LLMs, multi-task learning.  
**Code** : https://github.com/microsoft/LoRA  
**Lire si** : Fine-tuning LLMs, resource constraints.

---

## Frontend & Web Performance

### "Reconciliation" (React Fiber Architecture, 2017)
**Type** : Design doc Facebook  
**Impact** : React concurrent mode, priorité updates.  
**Contribution** : Scheduling, time-slicing, interruption renders.  
**Concepts** : Fiber tree, priority lanes, suspense.  
**Ressource** : https://github.com/acdlite/react-fiber-architecture  
**Lire si** : React internals, performance frontend.

---

## Sécurité

### "The Security of Modern Password Expiration" (Zhang et al., 2010)
**Venue** : ACM CCS 2010  
**Impact** : Remet en question politiques expiration mots de passe.  
**Résultat** : Expiration fréquente = patterns prévisibles, sécurité dégradée.  
**Recommandation** : Longueur + complexité > rotation fréquente.  
**Lire si** : Authentication policies, UX security.

### "SoK: SSL and HTTPS Revisited" (Clark & van Oorschot, 2013)
**Venue** : IEEE S&P 2013  
**Impact** : Systematization of Knowledge SSL/TLS.  
**Problèmes** : Certificate validation, downgrade attacks, implementation bugs.  
**Best practices** : Certificate pinning, HSTS, modern TLS configs.  
**Lire si** : Web security, HTTPS deployment.

---

## Bases de Données

### "The Log: What every software engineer should know" (Kreps, 2013)
**Type** : Blog post LinkedIn  
**Impact** : Popularise log-centric architectures.  
**Concepts** : Append-only logs, Kafka design, stream processing.  
**Applications** : Event sourcing, CDC, replication.  
**Ressource** : https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know  
**Lire si** : Distributed systems, event-driven.

### "A Critique of ANSI SQL Isolation Levels" (Berenson et al., 1995)
**Venue** : SIGMOD 1995  
**Citations** : 2,500+  
**Impact** : Révèle ambiguïtés standards SQL isolation.  
**Concepts** : Snapshot isolation, phantom reads, serializability.  
**Recommandations** : Isolation levels clarifiés.  
**Lire si** : Transactions, consistency models.

---

**Usage documentaliste** :  
- Identifier papers fondamentaux par domaine  
- Tracer filiation concepts (Attention → Transformers → GPT)  
- Références pour justifier choix techniques  
- Onboarding équipe sur sujets complexes  

**Méthodologie veille** :  
1. Suivre citations (forward/backward)  
2. Conférences top : NeurIPS, ICML, SIGMOD, OSDI, SOSP  
3. Auteurs influents (h-index >50)  
4. Papers with Code pour reproductibilité
