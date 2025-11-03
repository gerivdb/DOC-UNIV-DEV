```json
{
  "metadata": {
    "version": "1.0",
    "date": "2025-11-03",
    "role": "Documentaliste Universitaire Full-Stack ML",
    "total_resources": 50,
    "sources_prioritaires": {
      "academique": "40%",
      "implementation": "40%",
      "veille_expertise": "20%"
    }
  },
  "resources": {
    "academique": [
      {
        "id": "A1",
        "name": "Google Scholar",
        "url": "https://scholar.google.com",
        "priority": "HAUTE",
        "usage": "Papers récents (<3 ans), citation >50, h-index auteurs"
      },
      {
        "id": "A2",
        "name": "ArXiv",
        "url": "https://arxiv.org",
        "priority": "HAUTE",
        "usage": "Preprints ML/CS, front recherche, SOTA"
      },
      {
        "id": "A3",
        "name": "Semantic Scholar",
        "url": "https://semanticscholar.org",
        "priority": "HAUTE",
        "usage": "Citation graph, recommandations contextuelles"
      },
      {
        "id": "A4",
        "name": "Papers with Code",
        "url": "https://paperswithcode.com",
        "priority": "CRITIQUE",
        "usage": "Implémentations officielles + benchmarks"
      },
      {
        "id": "A5",
        "name": "OpenReview",
        "url": "https://openreview.net",
        "priority": "HAUTE",
        "usage": "Peer-review discussions, conférences top"
      },
      {
        "id": "A6",
        "name": "ACM Digital Library",
        "url": "https://dl.acm.org",
        "priority": "HAUTE",
        "usage": "SIGMOD, CHI, ICML proceedings"
      },
      {
        "id": "A7",
        "name": "IEEE Xplore",
        "url": "https://ieeexplore.ieee.org",
        "priority": "MOYENNE",
        "usage": "Engineering, systèmes distribués, IoT"
      },
      {
        "id": "A8",
        "name": "JMLR",
        "url": "https://jmlr.org",
        "priority": "HAUTE",
        "usage": "Machine learning, théorie algorithmique"
      },
      {
        "id": "A9",
        "name": "ResearchGate",
        "url": "https://researchgate.net",
        "priority": "MOYENNE",
        "usage": "Contact auteurs, datasets, discussions"
      },
      {
        "id": "A10",
        "name": "Distill.pub",
        "url": "https://distill.pub",
        "priority": "HAUTE",
        "usage": "Explications visuelles ML/DL, vulgarisation"
      }
    ],
    "implementation": [
      {
        "id": "I1",
        "name": "GitHub",
        "url": "https://github.com",
        "priority": "CRITIQUE",
        "usage": "Repos trending, >500★, issues/discussions"
      },
      {
        "id": "I2",
        "name": "Hugging Face",
        "url": "https://huggingface.co",
        "priority": "CRITIQUE",
        "usage": "Models, datasets, spaces, communauté ML"
      },
      {
        "id": "I3",
        "name": "Kaggle",
        "url": "https://kaggle.com",
        "priority": "HAUTE",
        "usage": "Notebooks, compétitions, analyses exemplaires"
      },
      {
        "id": "I4",
        "name": "Stack Overflow",
        "url": "https://stackoverflow.com",
        "priority": "HAUTE",
        "usage": "Solutions pratiques, edge cases réels"
      },
      {
        "id": "I5",
        "name": "PyPI",
        "url": "https://pypi.org",
        "priority": "MOYENNE",
        "usage": "Packages Python, stats downloads"
      },
      {
        "id": "I6",
        "name": "npm",
        "url": "https://npmjs.com",
        "priority": "MOYENNE",
        "usage": "Packages JavaScript/TypeScript"
      },
      {
        "id": "I7",
        "name": "Docker Hub",
        "url": "https://hub.docker.com",
        "priority": "MOYENNE",
        "usage": "Images officielles, containers"
      },
      {
        "id": "I8",
        "name": "FastAPI Docs",
        "url": "https://fastapi.tiangolo.com",
        "priority": "HAUTE",
        "usage": "Backend async, API REST moderne"
      },
      {
        "id": "I9",
        "name": "React Docs",
        "url": "https://react.dev",
        "priority": "HAUTE",
        "usage": "Frontend moderne, patterns"
      },
      {
        "id": "I10",
        "name": "Awesome Lists",
        "url": "https://github.com/sindresorhus/awesome",
        "priority": "HAUTE",
        "usage": "Listes curées par domaine"
      }
    ],
    "architecture_devops": [
      {
        "id": "AD1",
        "name": "Martin Fowler Blog",
        "url": "https://martinfowler.com",
        "priority": "HAUTE",
        "usage": "Patterns, microservices, refactoring"
      },
      {
        "id": "AD2",
        "name": "Kubernetes Docs",
        "url": "https://kubernetes.io/docs",
        "priority": "HAUTE",
        "usage": "Orchestration, scaling, production"
      },
      {
        "id": "AD3",
        "name": "CNCF",
        "url": "https://cncf.io",
        "priority": "MOYENNE",
        "usage": "Projects cloud-native, landscape"
      },
      {
        "id": "AD4",
        "name": "The New Stack",
        "url": "https://thenewstack.io",
        "priority": "MOYENNE",
        "usage": "Trends DevOps, cloud, architecture"
      },
      {
        "id": "AD5",
        "name": "DDIA Book",
        "url": "https://dataintensive.net",
        "priority": "CRITIQUE",
        "usage": "Bible systèmes distribués"
      }
    ],
    "ml_ai_llms": [
      {
        "id": "ML1",
        "name": "Andrej Karpathy Blog",
        "url": "https://karpathy.github.io",
        "priority": "HAUTE",
        "usage": "Neural networks, LLMs, deep learning"
      },
      {
        "id": "ML2",
        "name": "Chip Huyen Blog",
        "url": "https://huyenchip.com",
        "priority": "HAUTE",
        "usage": "MLOps, ML systems, production"
      },
      {
        "id": "ML3",
        "name": "MLOps Community",
        "url": "https://mlops.community",
        "priority": "HAUTE",
        "usage": "Podcasts, events, best practices"
      },
      {
        "id": "ML4",
        "name": "Google AI Blog",
        "url": "https://ai.googleblog.com",
        "priority": "HAUTE",
        "usage": "Innovations Google, papers vulgarisés"
      },
      {
        "id": "ML5",
        "name": "OpenAI Research",
        "url": "https://openai.com/research",
        "priority": "HAUTE",
        "usage": "LLMs, GPT, safety AI"
      },
      {
        "id": "ML6",
        "name": "Anthropic Research",
        "url": "https://anthropic.com/research",
        "priority": "HAUTE",
        "usage": "Constitutional AI, interpretability"
      },
      {
        "id": "ML7",
        "name": "DeepMind",
        "url": "https://deepmind.google/research",
        "priority": "HAUTE",
        "usage": "RL, AlphaFold, AGI research"
      },
      {
        "id": "ML8",
        "name": "LangChain",
        "url": "https://python.langchain.com",
        "priority": "HAUTE",
        "usage": "LLM applications, agents, chains"
      },
      {
        "id": "ML9",
        "name": "Vector DB Landscape",
        "url": "https://github.com/currentslab/awesome-vector-search",
        "priority": "MOYENNE",
        "usage": "Pinecone, Weaviate, Chroma comparisons"
      }
    ],
    "frontend_ux": [
      {
        "id": "FE1",
        "name": "web.dev",
        "url": "https://web.dev",
        "priority": "HAUTE",
        "usage": "Performance, accessibilité, PWA"
      },
      {
        "id": "FE2",
        "name": "MDN Web Docs",
        "url": "https://developer.mozilla.org",
        "priority": "CRITIQUE",
        "usage": "Référence HTML/CSS/JS standard"
      },
      {
        "id": "FE3",
        "name": "Can I Use",
        "url": "https://caniuse.com",
        "priority": "MOYENNE",
        "usage": "Support navigateurs, features"
      },
      {
        "id": "FE4",
        "name": "Three.js Examples",
        "url": "https://threejs.org/examples",
        "priority": "MOYENNE",
        "usage": "3D web, visualisations"
      },
      {
        "id": "FE5",
        "name": "Smashing Magazine",
        "url": "https://smashingmagazine.com",
        "priority": "MOYENNE",
        "usage": "Design patterns, UX, frontend"
      }
    ],
    "communaute_veille": [
      {
        "id": "CV1",
        "name": "Reddit ML",
        "url": "https://reddit.com/r/MachineLearning",
        "priority": "HAUTE",
        "usage": "Discussions, papers SOTA, trends"
      },
      {
        "id": "CV2",
        "name": "Hacker News",
        "url": "https://news.ycombinator.com",
        "priority": "HAUTE",
        "usage": "Tech news, discussions qualité"
      },
      {
        "id": "CV3",
        "name": "Dev.to",
        "url": "https://dev.to",
        "priority": "MOYENNE",
        "usage": "Tutoriels, retours expérience"
      },
      {
        "id": "CV4",
        "name": "Medium Engineering",
        "url": "https://medium.com/tag/engineering",
        "priority": "MOYENNE",
        "usage": "Architecture decisions, postmortems"
      },
      {
        "id": "CV5",
        "name": "InfoQ",
        "url": "https://infoq.com",
        "priority": "MOYENNE",
        "usage": "Conférences, articles approfondis"
      },
      {
        "id": "CV6",
        "name": "ThoughtWorks Radar",
        "url": "https://thoughtworks.com/radar",
        "priority": "HAUTE",
        "usage": "Technos adopt/trial/assess/hold"
      },
      {
        "id": "CV7",
        "name": "State of JS",
        "url": "https://stateofjs.com",
        "priority": "MOYENNE",
        "usage": "Trends JavaScript annuels"
      },
      {
        "id": "CV8",
        "name": "DORA Report",
        "url": "https://dora.dev",
        "priority": "HAUTE",
        "usage": "Métriques DevOps, best practices"
      }
    ],
    "datasets_benchmarks": [
      {
        "id": "DB1",
        "name": "HF Datasets",
        "url": "https://huggingface.co/datasets",
        "priority": "CRITIQUE",
        "usage": "NLP, vision, multimodal datasets"
      },
      {
        "id": "DB2",
        "name": "Google Dataset Search",
        "url": "https://datasetsearch.research.google.com",
        "priority": "HAUTE",
        "usage": "Recherche datasets open"
      },
      {
        "id": "DB3",
        "name": "UCI ML Repository",
        "url": "https://archive.ics.uci.edu/ml",
        "priority": "MOYENNE",
        "usage": "Benchmarks standards ML"
      }
    ]
  },
  "top_10_links": [
    {
      "rank": 1,
      "name": "Papers with Code",
      "url": "https://paperswithcode.com",
      "reason": "Theory + Implementation"
    },
    {
      "rank": 2,
      "name": "Hugging Face",
      "url": "https://huggingface.co",
      "reason": "Models, datasets, ML community"
    },
    {
      "rank": 3,
      "name": "GitHub",
      "url": "https://github.com",
      "reason": "Production code patterns"
    },
    {
      "rank": 4,
      "name": "Google Scholar",
      "url": "https://scholar.google.com",
      "reason": "Academic papers discovery"
    },
    {
      "rank": 5,
      "name": "ArXiv",
      "url": "https://arxiv.org",
      "reason": "Cutting-edge research preprints"
    },
    {
      "rank": 6,
      "name": "Semantic Scholar",
      "url": "https://semanticscholar.org",
      "reason": "Citation graph analysis"
    },
    {
      "rank": 7,
      "name": "FastAPI Docs",
      "url": "https://fastapi.tiangolo.com",
      "reason": "Modern async backend"
    },
    {
      "rank": 8,
      "name": "Chip Huyen",
      "url": "https://huyenchip.com",
      "reason": "MLOps production expertise"
    },
    {
      "rank": 9,
      "name": "ThoughtWorks Radar",
      "url": "https://thoughtworks.com/radar",
      "reason": "Tech trends quarterly"
    },
    {
      "rank": 10,
      "name": "MLOps Community",
      "url": "https://mlops.community",
      "reason": "Best practices, podcasts"
    }
  ]
}
```
