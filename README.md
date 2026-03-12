# AWS Certified Generative AI Developer - Professional (DEV-P01)

## GUÍA COMPLETA DE SUBSERVICIOS: Amazon Bedrock & Amazon SageMaker AI

> Documento de referencia para estudio del examen
> Preparado por: @diegoinoca | Marzo 2026

---

# PARTE 1: AMAZON BEDROCK

Amazon Bedrock es la plataforma fully managed de AWS para construir aplicaciones de IA generativa. Proporciona acceso a foundation models (FMs) de múltiples proveedores a través de una API unificada, junto con herramientas para personalización, orquestación, seguridad y despliegue de agentes.

---

## 1.1 Foundation Models (Acceso a Modelos)

Bedrock ofrece acceso serverless a ~100 modelos de múltiples proveedores a través de una API unificada. El desarrollador no gestiona infraestructura.

| Proveedor | Modelos Clave | Fortaleza | Keyword Examen |
|---|---|---|---|
| **Amazon** | Nova Pro, Nova Lite, Nova Micro, Nova Premier, Titan Text/Image/Embed | Costo-efectivo, multimodal, familia completa | "cost-effective", "Amazon model" |
| **Anthropic** | Claude 4.5, Claude Sonnet/Haiku/Opus | Razonamiento avanzado, coding, largo contexto | "advanced reasoning", "complex tasks" |
| **Meta** | Llama 3.x, Llama 4 | Open-weight, customizable | "open source", "self-hosted" |
| **Mistral AI** | Mistral Large, Ministral family | Eficiente, multilingual | "efficient", "multilingual" |
| **Cohere** | Command R/R+, Embed | RAG optimizado, embeddings | "enterprise search", "RAG" |
| **Stability AI** | SDXL, SD3 | Generación de imágenes | "image generation" |
| **AI21 Labs** | Jamba Instruct | Procesamiento largo contexto | "long context" |

---

## 1.2 Model Customization (Personalización)

Bedrock permite personalizar modelos sin gestionar infraestructura de entrenamiento.

| Técnica | Descripción | Cuándo Usar | Keyword |
|---|---|---|---|
| **Fine-Tuning (SFT)** | Supervised Fine-Tuning: entrena con pares input/output etiquetados para adaptar estilo, tono o formato | Cambiar COMPORTAMIENTO del modelo (no datos factuales) | "style", "tone", "format" |
| **Continued Pre-Training** | Entrena el modelo con datos no etiquetados de tu dominio para expandir su conocimiento base | Dominio técnico especializado (legal, médico) | "domain knowledge", "specialized" |
| **Reinforcement Fine-Tuning (RFT)** | Usa feedback/reward functions para mejorar automáticamente sin datasets etiquetados masivos | Mejorar accuracy sin datos etiquetados, optimizar decisiones | "reward function", "feedback-driven" |
| **Prompt Engineering** | Instrucciones en el prompt sin modificar el modelo (zero-shot, few-shot, CoT) | Ajustes rápidos, sin entrenamiento | "no training", "instructions" |

---

## 1.3 Model Inference (Invocación)

### Modos de Invocación

| Modo | Descripción | Keyword Examen |
|---|---|---|
| **On-Demand** | Pago por token, sin compromiso. Modo default. | "flexible", "no commitment" |
| **Batch Inference** | Procesamiento masivo offline, más barato que on-demand | "large volume", "offline", "cost-effective" |
| **Provisioned Throughput** | Capacidad reservada con throughput garantizado | "consistent latency", "SLA", "predictable" |
| **Cross-Region Inference** | Routing global automático para evitar limitaciones regionales | "availability", "capacity", "global" |
| **Service Tiers** | Priority (25% menos latencia), Standard, Flex (50% menos costo) | "latency-sensitive" → Priority, "background" → Flex |
| **Prompt Caching** | Cachea prompts largos frecuentes, reduce costos hasta 90% | "repeated prompts", "cost reduction" |

### Parámetros de Inferencia (CLAVE PARA EXAMEN)

| Parámetro | Función | Bajar → | Subir → |
|---|---|---|---|
| **Temperature** | Forma de la distribución de probabilidad | Más determinístico, preciso | Más creativo, diverso |
| **Top_K** | Número FIJO de tokens candidatos | Menos candidatos (determinístico) | Más candidatos |
| **Top_P** | Probabilidad acumulada DINÁMICA de candidatos | Menos candidatos (variable) | Más candidatos |
| **Max Tokens** | Límite de tokens en la respuesta | Respuestas más cortas | Respuestas más largas |
| **Stop Sequences** | Secuencias donde el modelo deja de generar | N/A | N/A |

>  **REGLA:** Determinismo = Temperature baja + Top_K bajo. Top_K > Top_P para determinismo porque Top_K es fijo, Top_P es dinámico.

---

## 1.4 Knowledge Bases (RAG)

Servicio managed para implementar Retrieval-Augmented Generation sin gestionar vector stores ni pipelines de embedding.

| Componente | Descripción | Keyword Examen |
|---|---|---|
| **Data Sources** | S3 buckets, Confluence, SharePoint, Salesforce, Web Crawler | "internal documents", "enterprise data" |
| **Chunking** | Estrategias: fixed-size, semantic, hierarchical, none | "chunk strategy", "document splitting" |
| **Embedding** | Convierte chunks a vectores (Titan Embeddings, Cohere Embed) | "semantic search", "vector" |
| **Vector Store** | OpenSearch Serverless (default), Pinecone, Redis, MongoDB Atlas, Aurora PostgreSQL | "vector database", "similarity search" |
| **Retrieval** | Búsqueda semántica + hybrid search (keyword + semantic) | "relevant context", "retrieve" |
| **Citations** | Source attribution — indica qué documento respaldó la respuesta | "cite sources", "traceability", "grounding" |
| **Sync Schedule** | Programable para re-ingestar datos actualizados | "data changes frequently", "weekly updates" |

>  **REGLA:** Datos que cambian → RAG. Cambio de estilo/tono → Fine-Tuning. Instrucciones simples → Prompt Engineering.

---

## 1.5 Bedrock Agents

Agentes autónomos que razonan, planifican y ejecutan acciones usando foundation models. Orquestación nativa sin código custom.

| Feature | Descripción | Keyword Examen |
|---|---|---|
| **Action Groups** | Conjuntos de APIs/Lambda que el agente puede invocar para ejecutar acciones | "execute actions", "API calls" |
| **User Confirmation** | Human-in-the-loop: pide aprobación antes de ejecutar acciones sensibles | "confirm before executing", "sensitive action" |
| **Knowledge Base Integration** | El agente consulta Knowledge Bases para responder con contexto | "answer from documents" |
| **Multi-Agent Collaboration** | Supervisor agent orquesta agentes especializados (cada uno con su propio scope) | "different permissions", "modular", "specialized" |
| **Code Interpreter** | Ejecuta código Python para cálculos, visualizaciones, análisis | "calculate", "data analysis", "generate chart" |
| **Return of Control** | El agente devuelve control a la aplicación en puntos específicos | "application decides", "custom logic" |
| **Prompt Management** | Gestión centralizada de prompts con versioning | "standardize prompts", "versioning" |

---

## 1.6 Guardrails for Amazon Bedrock

Mecanismos de seguridad y control de contenido que filtran inputs y outputs del modelo. Operan a nivel de CONTENIDO (qué dice el modelo).

| Política | Descripción | Keyword Examen |
|---|---|---|
| **Content Filters** | Filtra contenido en categorías: hate, insults, sexual, violence, misconduct, prompt attack | "toxic content", "inappropriate" |
| **Denied Topics** | Bloquea temas específicos que no debe discutir el modelo | "restricted topics", "forbidden subjects" |
| **Word Filters** | Bloquea palabras/frases específicas y profanity | "blocked words", "profanity" |
| **Sensitive Info Filters** | Detecta/redacta PII (nombres, SSN, emails) y regex patterns custom | "PII in responses", "mask sensitive data" |
| **Contextual Grounding** | Verifica que la respuesta esté fundamentada en el contexto proporcionado (anti-hallucination) | "hallucination", "factual", "grounded" |
| **Automated Reasoning** | Usa lógica formal para validar claims contra políticas definidas | "policy compliance", "logical validation" |

>  **REGLA:** Guardrails filtra CONTENIDO (qué dice). User Confirmation controla ACCIONES (qué hace).

---

## 1.7 Amazon Bedrock AgentCore

Plataforma agnóstica para construir, desplegar y operar agentes a escala con cualquier framework y modelo. GA desde octubre 2025.

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **Runtime** | Entorno serverless para ejecutar agentes. Soporte para code zip y containers. Hasta 8 horas de ejecución. | "deploy agent", "serverless", "8 hours" |
| **Gateway** | Capa de routing que conecta agentes con tools/APIs/MCP servers de forma segura | "routing", "which model/tool", "connect tools" |
| **Policy** | Políticas determinísticas en Cedar, ejecutadas FUERA del LLM loop. Bloquea acciones no autorizadas. | "deterministic enforcement", "Cedar", "boundaries" |
| **Memory** | Memoria persistente: contexto entre sesiones + episódica (aprende de experiencias) | "persistent context", "continuity", "episodic" |
| **Identity** | AuthN/AuthZ para agentes. OAuth, API Keys, vault seguro. User-level context. | "permissions", "roles", "identity-driven" |
| **Observability** | Trazabilidad completa via CloudWatch + OTEL. Compatible con Datadog, LangSmith, etc. | "monitor", "trace", "metrics" |
| **Evaluations** | Testing continuo de calidad del agente basado en comportamiento real | "quality", "test agent", "judge" |
| **Code Interpreter** | Ejecución segura de código en sandbox | "execute code", "calculations" |
| **Browser Tool** | Runtime de navegador para automatizar workflows web | "web automation", "browser tasks" |

>  **REGLA:** Bedrock Agents = agente llave en mano. AgentCore = plataforma para gobernar agentes a escala con cualquier framework.

---

## 1.8 Otros Servicios de Bedrock

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **Bedrock Flows** | Orquestación visual de workflows GenAI con nodos conectados (prompt → condition → action) | "visual workflow", "deterministic flow" |
| **Model Evaluation** | Evalúa modelos con métricas automáticas (accuracy, toxicity, robustness) y humanas | "compare models", "evaluate", "benchmark" |
| **Bedrock Marketplace** | 100+ modelos adicionales más allá del catálogo base | "specialized models", "third-party" |
| **Bedrock Data Automation (BDA)** | Procesamiento automático de documentos, imágenes, audio/video multilingüe | "document processing", "multimodal extraction" |
| **Prompt Management** | Versionamiento y gestión centralizada de prompts | "standardize", "version prompts" |
| **Nova Forge** | Servicio para construir modelos Nova custom ($100K/año) | "custom Nova model" |

---
---

# PARTE 2: AMAZON SAGEMAKER AI

Amazon SageMaker AI es la plataforma completa de AWS para el ciclo de vida de ML: preparación de datos, entrenamiento, despliegue, monitoreo y operaciones (MLOps). Incluye entornos de desarrollo, algoritmos built-in, infraestructura de training/inference, y herramientas de governance.

> *Nota: En 2024, el SageMaker original fue renombrado a "SageMaker AI" y se creó la nueva generación de SageMaker como plataforma unificada de datos, analytics e IA.*

---

## 2.1 Entornos de Desarrollo

| Entorno | Descripción | Keyword Examen |
|---|---|---|
| **SageMaker Studio** | IDE web completo con JupyterLab, Code Editor (VS Code), RStudio. Hub central para ML. | "ML development", "IDE", "notebooks" |
| **SageMaker Canvas** | Herramienta no-code/low-code para crear modelos ML con interfaz visual. AutoML. | "no coding experience", "visual", "business analyst" |
| **SageMaker Unified Studio** | Plataforma unificada nueva generación: datos + analytics + ML + GenAI en un solo entorno | "unified", "data + AI", "single environment" |
| **Bedrock IDE** | Dentro de Unified Studio: construye apps GenAI con Knowledge Bases, Agents, Guardrails, Flows | "GenAI app development", "low-code GenAI" |
| **SageMaker Notebooks** | Notebooks Jupyter serverless para experimentación rápida | "quick experiment", "prototype" |

---

## 2.2 Preparación de Datos

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **Data Wrangler** | Preparación y transformación visual de datos con 300+ transformaciones predefinidas | "prepare data", "transform", "visual" |
| **Processing Jobs** | Ejecuta scripts de procesamiento (Spark, scikit-learn) en infraestructura managed | "preprocessing", "feature engineering", "SMOTE" |
| **Feature Store** | Repositorio centralizado de features reutilizables para ML, online + offline store | "reusable features", "feature sharing", "consistency" |
| **Ground Truth / GT Plus** | Servicio de etiquetado de datos con workforce humana o automática (active learning) | "labeling", "annotation", "human labelers" |
| **SageMaker Lakehouse** | Acceso unificado a data lakes (S3) + data warehouses (Redshift) con Apache Iceberg | "unified data access", "lakehouse" |
| **SageMaker Catalog** | Descubrimiento y governance de assets de datos y ML (basado en DataZone) | "discover data", "governance", "catalog" |

---

## 2.3 Entrenamiento de Modelos

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **Training Jobs** | Entrenamiento managed en instancias GPU/CPU. Spot training para ahorro. Distributed training. | "train model", "GPU", "distributed" |
| **HyperPod** | Clusters resilientes always-on para entrenar LLMs y modelos grandes. Auto-recovery de nodos. | "large model training", "LLM training", "resilient cluster" |
| **Training Plans** | Reservas de capacidad GPU con pricing predecible para entrenamiento a gran escala | "reserved capacity", "predictable cost", "GPU" |
| **Automatic Model Tuning** | Hyperparameter optimization (HPO) automático: random, bayesian, hyperband | "hyperparameter", "optimize", "tuning" |
| **Experiments** | Tracking y comparación de múltiples training runs con métricas y parámetros | "compare runs", "track experiments" |
| **Debugger & Profiler** | Detecta problemas de entrenamiento en tiempo real (vanishing gradients, overfitting, bottlenecks) | "training issues", "debug", "profile" |
| **Serverless Customization** | Fine-tuning serverless (SFT, RL, DPO) para Nova, DeepSeek, Llama, Qwen sin gestionar infra | "serverless fine-tuning", "no infrastructure" |

---

## 2.4 Algoritmos Built-in (CLAVE PARA EXAMEN)

SageMaker incluye algoritmos optimizados para tipos específicos de problemas. El examen evalúa si sabes cuál usar para cada problemática.

| Algoritmo | Tipo de Problema | Caso de Uso | Keyword Examen |
|---|---|---|---|
| **DeepAR** | Time-Series Forecasting | Predicción de demanda, ventas, tráfico. Cold-start con multi-series. | "forecast", "predict future", "no history" → DeepAR |
| **XGBoost** | Clasificación / Regresión | Datos tabulares generales. El más versátil para problemas estructurados. | "tabular data", "classification", "structured" |
| **Linear Learner** | Clasificación / Regresión | Regresión lineal y clasificación binaria/multiclase | "linear", "simple prediction" |
| **Random Cut Forest** | Anomaly Detection | Detectar outliers en datos: fraude, fallas, comportamiento anómalo | "anomaly", "outlier", "unusual" |
| **K-Means** | Clustering | Segmentación de clientes, agrupación de documentos | "segment", "group", "cluster" |
| **BlazingText** | NLP | Clasificación de texto y word embeddings optimizados | "text classification", "word vectors" |
| **Seq2Seq** | Sequence-to-Sequence | Traducción, resumen, generación de texto | "translate", "summarize" |
| **IP Insights** | Anomaly (IP) | Detectar accesos sospechosos por dirección IP | "suspicious IP", "access pattern" |
| **Object2Vec** | Embeddings | Genera embeddings para objetos arbitrarios (pares de entidades) | "entity similarity", "pair embeddings" |
| **Neural Topic Model** | Topic Modeling | Descubrir temas latentes en corpus de texto | "discover topics", "theme extraction" |
| **LDA** | Topic Modeling | Latent Dirichlet Allocation para documentos | "document topics" |
| **Semantic Segmentation** | Computer Vision | Segmentación pixel-a-pixel en imágenes | "pixel classification", "image segmentation" |
| **Image Classification** | Computer Vision | Clasificación de imágenes completas | "what is in this image" |
| **Object Detection** | Computer Vision | Detectar y localizar objetos dentro de imágenes | "find objects", "bounding box" |

>  **REGLA:** Primero identifica el PROBLEMA, después elige el ALGORITMO. Forecasting → DeepAR. Anomalías → RCF. Tabular → XGBoost/LL. Clustering → K-Means.

---

## 2.5 Despliegue e Inferencia

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **Real-Time Endpoints** | Inferencia síncrona con baja latencia. Auto-scaling configurable. | "real-time", "low latency", "synchronous" |
| **Serverless Inference** | Endpoints serverless que escalan a cero. Pago por uso. | "intermittent traffic", "scale to zero", "cost savings" |
| **Async Inference** | Para predicciones largas (hasta 1 hora). Cola + procesamiento. Respuesta en S3. | "large payload", "long processing", "async" |
| **Batch Transform** | Procesamiento masivo offline de datasets completos | "bulk predictions", "offline", "full dataset" |
| **Inference Components** | Unidades modulares de inferencia en un endpoint. Multi-modelo, multi-AZ. | "multiple models", "modular", "shared endpoint" |
| **Multi-Adapter Inference** | Carga dinámica de LoRA adapters en un solo base model endpoint | "LoRA", "multiple fine-tuned variants" |
| **Speculative Decoding (EAGLE-3)** | Aumenta throughput de inferencia sin sacrificar calidad | "faster inference", "throughput" |

---

## 2.6 SageMaker JumpStart

Hub de modelos pre-entrenados, soluciones pre-construidas y notebooks de ejemplo. Permite desarrollo acelerado sin experiencia profunda en ML.

| Feature | Descripción | Keyword Examen |
|---|---|---|
| **Foundation Models** | Acceso a modelos open-source: Llama, Falcon, Mistral, Stability, Hugging Face | "pre-trained model", "quick start" |
| **Solution Templates** | Soluciones end-to-end pre-construidas para fraud detection, churn, demand forecasting | "pre-built solution", "template" |
| **One-Click Deploy** | Deploy modelos con un click en endpoints de SageMaker | "accelerate", "limited experience" |
| **Fine-Tuning** | Fine-tune modelos de JumpStart con datos propios | "customize pre-trained model" |

>  **REGLA:** JumpStart CONSTRUYE rápido (principiante). Pipelines AUTOMATIZA (MLOps). Clarify AUDITA (fairness).

---

## 2.7 MLOps & Operaciones

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **SageMaker Pipelines** | Orquestación CI/CD para ML. Define workflows multi-paso programáticamente. | "automate", "CI/CD", "MLOps", "pipeline" |
| **Model Registry** | Repositorio centralizado de versiones de modelos con aprobaciones y lineage | "versioning", "model catalog", "approval workflow" |
| **Model Monitor** | Detecta data drift, model drift y bias drift en producción continuamente | "drift", "degradation", "production monitoring" |
| **Model Cards** | Documentación estandarizada del modelo: uso previsto, métricas, limitaciones | "documentation", "transparency", "intended use" |
| **Model Dashboard** | Vista consolidada de health de todos los modelos desplegados | "overview", "all models", "health status" |
| **SageMaker Projects** | Templates MLOps con repositorios, pipelines y deployment automático integrado | "MLOps template", "end-to-end automation" |

---

## 2.8 Responsible AI & Seguridad

| Servicio | Descripción | Keyword Examen |
|---|---|---|
| **SageMaker Clarify** | Detección de bias en datos/modelo + explicabilidad (SHAP values, feature importance). PRE-DEPLOY. | "bias", "fairness", "explainability", "SHAP" |
| **Amazon A2I** | Human-in-the-loop: crea workflows de revisión humana para predicciones de baja confianza. POST-DEPLOY. | "human review", "low confidence", "review workflow" |
| **SageMaker Role Manager** | Gestión de permisos IAM específicos para ML con roles predefinidos y custom | "ML permissions", "least privilege" |
| **VPC Configuration** | Ejecución de training/inference dentro de VPC sin acceso a internet | "network isolation", "private", "no internet" |

>  **REGLA:** Clarify revisa el MODELO (¿es justo? pre-deploy). A2I revisa las PREDICCIONES (¿es correcta? post-deploy).

---
---

# PARTE 3: SERVICIOS AWS AI/ML COMPLEMENTARIOS

Servicios de IA pre-entrenados que aparecen frecuentemente en el examen como opciones correctas o distractores.

### Procesamiento de Texto / NLP

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **Comprehend** | Texto | NLP: sentimiento, entidades, PII (DetectPiiEntities), idioma, toxicidad, frases clave | "PII text", "sentiment", "entities" |
| **Translate** | Texto | Traducción automática entre idiomas | "translate", "multilingual" |

### Procesamiento de Documentos

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **Textract** | Docs/PDF/Img | OCR: extrae texto, tablas, key-value pairs de documentos e imágenes | "extract from PDF", "OCR", "forms" |
| **Kendra** | Docs/Web | Búsqueda empresarial inteligente (Enterprise Search) | "search documents", "enterprise FAQ" |

### Procesamiento de Audio

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **Transcribe** | Audio | Speech-to-Text: convierte audio a texto | "transcribe", "speech recognition" |
| **Polly** | Texto | Text-to-Speech: genera voz desde texto | "read aloud", "voice", "TTS" |

### Procesamiento de Imágenes / Video

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **Rekognition** | Img/Video | Visión: caras, objetos, moderación visual, texto en imágenes, PII visual | "image analysis", "faces", "content moderation" |

### Conversación

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **Lex V2** | Texto/Voz | Chatbot basado en intents/slots (pre-GenAI). IVR, flujos estructurados. | "intent", "slot filling", "IVR" |

### Monitoreo

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **CloudWatch** | Métricas | Monitoreo de RENDIMIENTO: métricas, logs, alarmas, dashboards | "performance", "metrics", "alarms" |
| **CloudTrail** | API Calls | Auditoría de ACCESOS: quién hizo qué, cuándo, desde dónde | "audit", "who accessed", "compliance" |

### Seguridad de Datos

| Servicio | Input | Función | Keywords |
|---|---|---|---|
| **Macie** | S3 Buckets | Detecta exposición de datos sensibles en S3 (PII, credenciales) | "sensitive data exposure", "S3 scanning" |
| **KMS** | Encryption Keys | Gestión de llaves de cifrado para encryption at rest | "encryption at rest", "key management" |

---
---

# PARTE 4: FRAMEWORK DE DECISIÓN PARA EL EXAMEN

## 4.1 Reglas de Oro (Mnemotécnicas)

| # | Regla | Contexto |
|---|---|---|
| 1 | **Comprehend LEE, Rekognition VE, Textract EXTRAE, Transcribe ESCUCHA** | Servicios AI pre-entrenados |
| 2 | **Guardrails filtra PALABRAS, Confirmation controla ACCIONES** | Seguridad en Agents |
| 3 | **CloudTrail rastrea PERSONAS, CloudWatch rastrea MÁQUINAS** | Monitoreo |
| 4 | **Clarify revisa el MODELO, A2I revisa las PREDICCIONES** | Responsible AI |
| 5 | **RAG para DATOS, Fine-Tune para TONO** | Customización |
| 6 | **JumpStart CONSTRUYE, Pipelines AUTOMATIZA, Clarify AUDITA** | SageMaker |
| 7 | **Lex CONVERSA, un Agent ACTÚA** | Conversación vs Agentes |
| 8 | **Para determinismo: K es King** (Top_K > Top_P) | Inference Parameters |
| 9 | **Bedrock Agents = llave en mano. AgentCore = plataforma enterprise** | Agentes |
| 10 | **Primero el PROBLEMA, después el ALGORITMO** | Algoritmos Built-in |

---

## 4.2 Señales Clave en Enunciados del Examen

| Si ves en el enunciado... | Entonces piensa en... |
|---|---|
| "datos que cambian frecuentemente" | RAG / Knowledge Bases (NO fine-tuning) |
| "limited experience" / "accelerate development" | SageMaker JumpStart |
| "minimize custom orchestration code" | Bedrock Agents / Multi-Agent Collaboration |
| "reasoning, planning, executing" | Bedrock Agents (NO Lex) |
| "deterministic" / "consistent" / "less random" | Temperature baja + Top_K bajo |
| "ALL text-based communications" | Comprehend (alcance universal, no solo Lex) |
| "fair and unbiased" / "bias detection" | SageMaker Clarify |
| "human review" / "low confidence predictions" | Amazon A2I |
| "hallucinations" / "verify against sources" | Grounding con RAG / Knowledge Bases |
| "no sales history" / "new product" | DeepAR (cold-start multi-series) |
| "detect anomalies" / "outliers" | Random Cut Forest (NO forecasting) |
| "encryption at rest" + "key control" | SSE-KMS |
| "audit" / "who accessed what" | CloudTrail |
| "model performance" / "metrics" / "alarms" | CloudWatch |
| "different permissions per step" / "modular" | Multi-Agent Collaboration |
| "any framework" / "framework agnostic" | Bedrock AgentCore |
| "PII" + "images/video" | Rekognition |
| "PII" + "text" | Comprehend (DetectPiiEntities) |
| "extract text from documents" | Textract |
| "intent-based" / "slot filling" | Amazon Lex (NO Agents) |

---

## 4.3 Parejas Trampa del Examen

| Par confuso | Servicio A → | Servicio B → |
|---|---|---|
| **CloudTrail vs CloudWatch** | ¿QUIÉN hizo qué? (audit) | ¿CÓMO RINDE? (metrics) |
| **Clarify vs A2I** | ¿El MODELO es justo? (pre-deploy) | ¿La PREDICCIÓN es correcta? (post-deploy) |
| **Lex vs Agents** | Chatbot RÍGIDO (intents/slots) | Agente AUTÓNOMO (reasoning/actions) |
| **Textract vs Comprehend** | EXTRAER texto de docs (OCR) | ANALIZAR texto existente (NLP) |
| **Guardrails vs User Confirmation** | Filtra CONTENIDO | Controla ACCIONES |
| **Knowledge Bases vs Agents** | BUSCAR información (RAG) | RAZONAR y ACTUAR |
| **JumpStart vs Pipelines** | CONSTRUIR rápido | AUTOMATIZAR CI/CD |
| **Rekognition vs Comprehend** | Analiza IMÁGENES | Analiza TEXTO |
| **Transcribe vs Polly** | Audio → Texto (STT) | Texto → Audio (TTS) |
| **Bedrock Agents vs AgentCore** | Llave en mano (solo Bedrock) | Plataforma abierta (cualquier framework) |

---
