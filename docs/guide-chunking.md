# 🔧 Guide Complet du Chunking pour RAG
## Stratégies Optimales par Type de Contenu

### 🎯 **Objectif du Guide**

Ce guide fournit des **stratégies pratiques et optimisées** pour le chunking de différents types de documents dans le contexte d'un système RAG (Retrieval-Augmented Generation), avec un focus sur la **qualité de la récupération** et la **cohérence sémantique**.

---

## 📋 **Principes Fondamentaux du Chunking**

### **1. Équilibre Taille vs Contexte**
- **Chunks trop petits** : Perte de contexte, information fragmentée
- **Chunks trop grands** : Dilution de l'information pertinente, embedding moins précis
- **Zone optimale** : 200-1000 tokens selon le type de contenu

### **2. Préservation de la Cohérence Sémantique**
- Respecter les unités logiques naturelles (paragraphes, sections, fonctions)
- Éviter de couper au milieu des phrases ou concepts
- Maintenir le contexte nécessaire à la compréhension

### **3. Stratégies d'Overlap**
- **Overlap fixe** : 10-20% pour maintenir la continuité
- **Overlap sémantique** : Basé sur la similarité du contenu
- **Overlap contextuel** : Préservation des références et liens

---

## 📄 **CHUNKING DOCUMENTS PDF**

### **Stratégie Générale PDF**

```python
# Configuration optimale pour PDF
PDF_CHUNKING_CONFIG = {
    "chunk_size": 800,           # Tokens
    "overlap": 150,              # Tokens (18.75%)
    "min_chunk_size": 200,       # Éviter chunks trop petits
    "respect_paragraphs": True,   # Ne pas couper mid-paragraph
    "preserve_structure": True    # Maintenir headers/sections
}
```

### **PDF Académiques (Papers, Thèses)**

**Caractéristiques** : Structure formelle, références, figures, tableaux

```yaml
academic_pdf_strategy:
  chunk_by: "section"           # Respecter la structure académique
  chunk_size: 1000             # Plus grande pour contexte académique
  overlap: 200                 # Overlap plus important
  preserve_elements:
    - headers                  # Titres de sections
    - citations               # Références bibliographiques  
    - figure_captions         # Légendes de figures
    - table_content          # Contenu des tableaux
  special_handling:
    abstract: "single_chunk"   # Abstract toujours dans un seul chunk
    conclusion: "single_chunk" # Conclusion préservée
    references: "separate"     # Bibliographie séparée
```

**Exemple d'implémentation** :

```python
def chunk_academic_pdf(pdf_text, metadata):
    chunks = []
    
    # 1. Extraction des sections
    sections = extract_sections(pdf_text)
    
    for section in sections:
        if section.type == "abstract":
            # Abstract toujours en un seul chunk
            chunks.append({
                "content": section.content,
                "type": "abstract",
                "section": section.title,
                "metadata": metadata
            })
        elif section.type == "content":
            # Chunking normal avec respect des paragraphes
            section_chunks = semantic_split(
                section.content, 
                max_size=1000,
                overlap=200,
                respect_boundaries=True
            )
            for i, chunk in enumerate(section_chunks):
                chunks.append({
                    "content": chunk,
                    "type": "content",
                    "section": section.title,
                    "chunk_index": i,
                    "metadata": metadata
                })
    
    return chunks
```

### **PDF Techniques (Manuels, Documentation)**

**Caractéristiques** : Code snippets, diagrammes, procédures

```yaml
technical_pdf_strategy:
  chunk_size: 600              # Plus petit pour précision technique
  overlap: 100
  preserve_structure: True
  special_elements:
    code_blocks:
      strategy: "complete"      # Ne jamais couper le code
      max_size: 1500           # Taille max pour code blocks
    procedures:
      strategy: "step_by_step"  # Respecter les étapes
    diagrams:
      strategy: "with_caption"  # Inclure légende + description
```

---

## 💻 **CHUNKING CODE SOURCE**

### **Stratégie Générale Code**

```python
CODE_CHUNKING_CONFIG = {
    "chunk_by": "function",      # Unité logique naturelle
    "max_chunk_size": 1200,      # Plus grand pour fonctions complexes
    "min_chunk_size": 100,       # Éviter snippets trop petits
    "include_context": True,     # Inclure imports/classes parentes
    "preserve_completeness": True # Fonctions complètes
}
```

### **Python / JavaScript / TypeScript**

**Stratégies par élément** :

```yaml
python_chunking:
  functions:
    strategy: "complete_function"    # Fonction complète avec docstring
    max_size: 1500
    include_decorators: True
    include_imports: "relevant"      # Seulement imports utilisés
  
  classes:
    strategy: "method_by_method"     # Chaque méthode = chunk
    include_class_context: True     # Docstring classe + __init__
    preserve_inheritance: True
  
  modules:
    strategy: "logical_blocks"       # Groupes de fonctions liées
    respect_comments: True          # Utiliser comments comme séparateurs
```

**Exemple d'implémentation** :

```python
def chunk_python_code(code_content, file_path):
    import ast
    
    chunks = []
    tree = ast.parse(code_content)
    
    # Extraction des imports
    imports = get_imports(tree)
    
    for node in ast.walk(tree):
        if isinstance(node, ast.FunctionDef):
            # Fonction complète avec contexte
            function_code = extract_function_with_context(
                node, code_content, imports
            )
            
            chunks.append({
                "content": function_code,
                "type": "function",
                "name": node.name,
                "file_path": file_path,
                "start_line": node.lineno,
                "docstring": ast.get_docstring(node),
                "complexity": calculate_complexity(node)
            })
        
        elif isinstance(node, ast.ClassDef):
            # Classe : chunk par méthode
            class_chunks = chunk_class_methods(node, code_content, imports)
            chunks.extend(class_chunks)
    
    return chunks
```

### **SQL / Configurations**

```yaml
sql_chunking:
  queries:
    strategy: "complete_statement"   # Query complète
    max_size: 800
    include_comments: True
  
  schemas:
    strategy: "table_by_table"       # Une table par chunk
    include_relationships: True      # Foreign keys contexte
  
  procedures:
    strategy: "complete_procedure"   # Procédure complète
    max_size: 2000
```

---

## 📝 **CHUNKING MARKDOWN**

### **Stratégie Générale Markdown**

```python
MARKDOWN_CHUNKING_CONFIG = {
    "chunk_by": "section",           # Headers comme délimiteurs naturels
    "chunk_size": 600,               # Optimal pour contenu textuel
    "overlap": 100,
    "preserve_hierarchy": True,      # Maintenir H1 > H2 > H3
    "include_headers": True          # Headers dans chaque chunk
}
```

### **Documentation Technique**

**Caractéristiques** : Headers structurés, code blocks, liens

```yaml
tech_markdown_strategy:
  hierarchy_respect: True
  sections:
    h1: "preserve_complete"          # Sections complètes si possible
    h2: "split_if_large"            # Subdiviser si > 1000 tokens
    h3: "keep_together"             # Garder sous-sections ensemble
  
  special_elements:
    code_blocks:
      strategy: "preserve_complete"  # Code jamais coupé
      include_language: True         # Préserver language hints
    
    tables:
      strategy: "complete_table"     # Table jamais coupée
      max_size: 1500                # Limite pour grandes tables
    
    lists:
      strategy: "logical_groups"     # Grouper items liés
      max_items_per_chunk: 10
```

**Exemple d'implémentation** :

```python
def chunk_markdown(md_content, metadata):
    import markdown
    from markdown.treeprocessors import Treeprocessor
    
    chunks = []
    
    # Parse markdown structure
    md = markdown.Markdown(extensions=['toc'])
    html = md.convert(md_content)
    toc = md.toc_tokens
    
    current_chunk = ""
    current_header = ""
    
    for line in md_content.split('\n'):
        if line.startswith('#'):
            # Nouveau header : finaliser chunk précédent
            if current_chunk and len(current_chunk.split()) > 50:
                chunks.append({
                    "content": current_chunk.strip(),
                    "header": current_header,
                    "type": "section",
                    "metadata": metadata
                })
            
            # Commencer nouveau chunk
            current_header = line.strip()
            current_chunk = line + '\n'
        else:
            current_chunk += line + '\n'
            
            # Vérifier taille chunk
            if len(current_chunk.split()) > 600:
                # Chercher point de coupure naturel
                split_point = find_natural_split(current_chunk)
                if split_point:
                    chunks.append({
                        "content": current_chunk[:split_point],
                        "header": current_header,
                        "type": "section_part",
                        "metadata": metadata
                    })
                    current_chunk = current_chunk[split_point:]
    
    # Dernier chunk
    if current_chunk.strip():
        chunks.append({
            "content": current_chunk.strip(),
            "header": current_header,
            "type": "section",
            "metadata": metadata
        })
    
    return chunks
```

### **Articles de Blog / Content Marketing**

```yaml
blog_markdown_strategy:
  chunk_size: 400                    # Plus petit pour contenu web
  overlap: 80
  respect_elements:
    - paragraphs                     # Paragraphes complets
    - quotes                         # Citations préservées
    - image_captions                 # Légendes avec images
  
  seo_preservation:
    include_title: True              # Titre dans chaque chunk
    preserve_keywords: True          # Maintenir mots-clés importants
```

---

## 🧠 **CHUNKING SÉMANTIQUE AVANCÉ**

### **Segmentation par Similarité**

```python
def semantic_chunking(text, embedding_model, similarity_threshold=0.8):
    """
    Chunking basé sur la similarité sémantique entre phrases
    """
    sentences = split_into_sentences(text)
    embeddings = [embedding_model.encode(s) for s in sentences]
    
    chunks = []
    current_chunk = [sentences[0]]
    
    for i in range(1, len(sentences)):
        # Calculer similarité avec chunk actuel
        chunk_embedding = mean(embeddings[:i])
        sentence_embedding = embeddings[i]
        similarity = cosine_similarity(chunk_embedding, sentence_embedding)
        
        if similarity >= similarity_threshold:
            current_chunk.append(sentences[i])
        else:
            # Nouvelle section sémantique : finaliser chunk
            chunks.append(' '.join(current_chunk))
            current_chunk = [sentences[i]]
    
    # Dernier chunk
    if current_chunk:
        chunks.append(' '.join(current_chunk))
    
    return chunks
```

### **Chunking Hiérarchique**

```python
def hierarchical_chunking(document, levels=["section", "paragraph", "sentence"]):
    """
    Chunking multi-niveau avec préservation hiérarchie
    """
    hierarchy = {}
    
    # Level 1: Sections
    sections = split_by_sections(document)
    for i, section in enumerate(sections):
        section_id = f"sec_{i}"
        hierarchy[section_id] = {
            "content": section,
            "level": "section",
            "children": {}
        }
        
        # Level 2: Paragraphes
        paragraphs = split_by_paragraphs(section)
        for j, paragraph in enumerate(paragraphs):
            para_id = f"para_{i}_{j}"
            hierarchy[section_id]["children"][para_id] = {
                "content": paragraph,
                "level": "paragraph",
                "parent": section_id,
                "children": {}
            }
            
            # Level 3: Phrases (si nécessaire)
            if len(paragraph.split()) > 200:
                sentences = split_by_sentences(paragraph)
                for k, sentence in enumerate(sentences):
                    sent_id = f"sent_{i}_{j}_{k}"
                    hierarchy[section_id]["children"][para_id]["children"][sent_id] = {
                        "content": sentence,
                        "level": "sentence",
                        "parent": para_id
                    }
    
    return hierarchy
```

---

## ⚡ **OPTIMISATIONS DE PERFORMANCE**

### **Chunking Parallèle**

```python
from concurrent.futures import ThreadPoolExecutor
import multiprocessing

def parallel_chunking(documents, chunking_strategy, max_workers=None):
    """
    Chunking parallèle pour traitement de gros volumes
    """
    if max_workers is None:
        max_workers = multiprocessing.cpu_count()
    
    with ThreadPoolExecutor(max_workers=max_workers) as executor:
        futures = []
        for doc in documents:
            future = executor.submit(chunking_strategy, doc)
            futures.append(future)
        
        results = []
        for future in futures:
            try:
                chunks = future.result(timeout=60)  # 1 min timeout
                results.extend(chunks)
            except Exception as e:
                print(f"Erreur chunking: {e}")
        
        return results
```

### **Cache Intelligent**

```python
class ChunkingCache:
    def __init__(self, cache_size=1000):
        self.cache = {}
        self.cache_size = cache_size
        self.access_order = []
    
    def get_chunks(self, content_hash, chunking_params):
        cache_key = (content_hash, str(chunking_params))
        
        if cache_key in self.cache:
            # Move to end (most recently used)
            self.access_order.remove(cache_key)
            self.access_order.append(cache_key)
            return self.cache[cache_key]
        
        return None
    
    def store_chunks(self, content_hash, chunking_params, chunks):
        cache_key = (content_hash, str(chunking_params))
        
        # Éviction LRU si cache plein
        if len(self.cache) >= self.cache_size:
            oldest_key = self.access_order.pop(0)
            del self.cache[oldest_key]
        
        self.cache[cache_key] = chunks
        self.access_order.append(cache_key)
```

---

## 📊 **ÉVALUATION QUALITÉ CHUNKING**

### **Métriques d'Évaluation**

```python
def evaluate_chunking_quality(chunks, ground_truth=None):
    """
    Évaluation de la qualité du chunking
    """
    metrics = {}
    
    # 1. Cohérence de taille
    sizes = [len(chunk["content"].split()) for chunk in chunks]
    metrics["size_consistency"] = {
        "mean": np.mean(sizes),
        "std": np.std(sizes),
        "coefficient_variation": np.std(sizes) / np.mean(sizes)
    }
    
    # 2. Couverture du contenu
    total_content = " ".join([chunk["content"] for chunk in chunks])
    original_content = ground_truth if ground_truth else total_content
    metrics["content_coverage"] = len(total_content) / len(original_content)
    
    # 3. Cohérence sémantique interne
    if len(chunks) > 1:
        coherence_scores = []
        for chunk in chunks:
            sentences = split_into_sentences(chunk["content"])
            if len(sentences) > 1:
                # Cohérence interne du chunk
                sentence_embeddings = [embed_sentence(s) for s in sentences]
                coherence = calculate_coherence(sentence_embeddings)
                coherence_scores.append(coherence)
        
        metrics["semantic_coherence"] = np.mean(coherence_scores)
    
    # 4. Qualité de l'overlap
    if len(chunks) > 1:
        overlap_quality = []
        for i in range(len(chunks) - 1):
            current = chunks[i]["content"]
            next_chunk = chunks[i + 1]["content"]
            overlap_score = calculate_overlap_quality(current, next_chunk)
            overlap_quality.append(overlap_score)
        
        metrics["overlap_quality"] = np.mean(overlap_quality)
    
    return metrics
```

### **Tests de Régression**

```python
def chunking_regression_test(test_cases, chunking_function):
    """
    Tests de non-régression pour chunking
    """
    results = {}
    
    for test_name, test_data in test_cases.items():
        input_text = test_data["input"]
        expected_chunks = test_data["expected_chunks"]
        
        # Chunking actuel
        actual_chunks = chunking_function(input_text)
        
        # Comparaison
        results[test_name] = {
            "passed": compare_chunks(expected_chunks, actual_chunks),
            "expected_count": len(expected_chunks),
            "actual_count": len(actual_chunks),
            "quality_score": evaluate_chunking_quality(actual_chunks)
        }
    
    return results
```

---

## 🎯 **RECOMMANDATIONS PAR CAS D'USAGE**

### **Documentation Technique**
- **Taille** : 600-800 tokens
- **Overlap** : 15-20%
- **Stratégie** : Section-based + code preservation
- **Métrique clé** : Completeness + Contextual coherence

### **Code Source**
- **Taille** : 800-1200 tokens  
- **Overlap** : 10-15%
- **Stratégie** : Function/class-based
- **Métrique clé** : Syntactic completeness + Logical unity

### **Contenu Académique**
- **Taille** : 800-1000 tokens
- **Overlap** : 20-25%
- **Stratégie** : Section-based + citation preservation
- **Métrique clé** : Semantic coherence + Reference integrity

### **Articles Web**
- **Taille** : 400-600 tokens
- **Overlap** : 15-20%
- **Stratégie** : Paragraph-based + keyword preservation
- **Métrique clé** : Readability + SEO value retention

---

## 🛠️ **OUTILS ET IMPLÉMENTATION**

### **Librairies Recommandées**

```bash
# Installation des dépendances
pip install langchain-text-splitters
pip install semantic-text-splitter
pip install nltk spacy
pip install sentence-transformers
pip install tiktoken  # Pour tokenization OpenAI
```

### **Pipeline de Production**

```python
class ProductionChunkingPipeline:
    def __init__(self, config):
        self.config = config
        self.cache = ChunkingCache()
        self.metrics_collector = MetricsCollector()
    
    def process_document(self, document, doc_type):
        # 1. Détection du type si non spécifié
        if not doc_type:
            doc_type = self.detect_document_type(document)
        
        # 2. Sélection stratégie
        strategy = self.get_strategy_for_type(doc_type)
        
        # 3. Cache check
        content_hash = self.hash_content(document.content)
        cached_chunks = self.cache.get_chunks(content_hash, strategy.params)
        if cached_chunks:
            return cached_chunks
        
        # 4. Chunking
        chunks = strategy.chunk(document)
        
        # 5. Post-processing
        chunks = self.post_process_chunks(chunks, doc_type)
        
        # 6. Quality check
        quality_score = self.evaluate_quality(chunks)
        if quality_score < self.config.min_quality_threshold:
            # Retry avec stratégie alternative
            chunks = self.fallback_chunking(document, doc_type)
        
        # 7. Cache storage
        self.cache.store_chunks(content_hash, strategy.params, chunks)
        
        # 8. Metrics collection
        self.metrics_collector.record_chunking(doc_type, quality_score, len(chunks))
        
        return chunks
```

---

## 📈 **MONITORING ET AMÉLIORATION CONTINUE**

### **Métriques de Production**

```yaml
chunking_monitoring:
  performance_metrics:
    - "chunking_latency_p95"      # 95e percentile latence
    - "chunks_per_document_avg"   # Nombre moyen chunks/doc
    - "chunk_size_distribution"   # Distribution tailles
    - "quality_score_avg"         # Score qualité moyen
  
  quality_metrics:
    - "semantic_coherence_avg"    # Cohérence sémantique
    - "content_coverage_ratio"    # Couverture contenu
    - "overlap_quality_score"     # Qualité overlap
    
  business_metrics:
    - "retrieval_accuracy"        # Précision récupération
    - "user_satisfaction_score"   # Satisfaction utilisateurs
    - "false_positive_rate"       # Taux faux positifs
```

### **Optimisation Continue**

```python
class ChunkingOptimizer:
    def __init__(self):
        self.experiments = {}
        self.baseline_metrics = {}
    
    def run_ab_test(self, strategy_a, strategy_b, test_documents):
        """
        A/B test entre deux stratégies de chunking
        """
        results_a = self.evaluate_strategy(strategy_a, test_documents)
        results_b = self.evaluate_strategy(strategy_b, test_documents)
        
        # Statistical significance test
        p_value = self.statistical_test(results_a, results_b)
        
        return {
            "strategy_a": results_a,
            "strategy_b": results_b,
            "winner": "A" if results_a["score"] > results_b["score"] else "B",
            "confidence": 1 - p_value,
            "significant": p_value < 0.05
        }
```

---

**Status** : ✅ **PRODUCTION READY**  
**Version** : 1.0.0  
**Dernière mise à jour** : 2025-11-03

Ce guide constitue la **référence complète** pour l'implémentation de stratégies de chunking optimales dans l'écosystème DOC-UNIV-DEV, garantissant une qualité maximale de récupération et de cohérence sémantique.