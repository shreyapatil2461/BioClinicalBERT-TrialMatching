# **Clinical Trial Matching Using BioClinicalBERT and RAG-Enhanced Retrieval**
## **Introduction**
In recent years, the growth of biomedical research has led to an explosion of clinical trials with increasingly complex eligibility criteria. Identifying the most suitable trial for a patient is a critical but challenging task for clinicians and researchers. The process involves analyzing detailed patient data—including diagnoses, treatment histories, and clinical notes—and matching them with trial descriptions that are often long, unstructured, and written in free text.  

Traditional approaches rely on keyword-based search or rule-based filters, which fail to understand the nuanced semantics of medical language. These methods are not only time-consuming and error-prone but also struggle to scale across large, diverse trial datasets.  
 
To address these challenges, this project proposes an intelligent clinical trial matching system that combines advanced natural language processing (NLP) and information retrieval techniques. The system leverages BioClinicalBERT, a domain-specific language model fine-tuned on clinical text, to semantically encode patient queries and trial descriptions into dense vector representations. Using FAISS (Facebook AI Similarity Search), these embeddings are indexed to enable fast and scalable retrieval of the most relevant trials.  

Further enhancing the system, a Retrieval-Augmented Generation (RAG) pipeline with Flan-T5 generates human-readable explanations for each recommendation, improving interpretability and clinician trust. Additionally, a custom explainability module highlights the most relevant attributes from both the patient profile and trial description, offering deeper insights into the decision-making process.  

This approach enables accurate, efficient, and transparent clinical trial matching, supporting personalized patient care and advancing medical research.  

## **Problem Statement**
Matching patients to appropriate clinical trials is a critical step in advancing medical research and personalized treatment. However, this process is currently manual, time-consuming, and prone to errors. The unstructured nature of eligibility criteria and the complexity of patient records make automated matching challenging. Existing keyword-based systems fail to capture nuanced medical semantics, leading to low accuracy and poor scalability.

## **Objective**

1.To design a semantic, scalable, and explainable system for clinical trial matching.  
2.To improve the accuracy of patient-trial recommendations using domain-specific embeddings.  
3.To enable interpretability through natural language justifications, fostering clinician trust.  

## **Architecture**






The proposed system is built upon a bi-encoder architecture that semantically matches patient queries to clinical trial descriptions. At the core of this system lies the BioClinicalBERT model, a transformer-based language model fine-tuned on large-scale clinical datasets such as MIMIC-III. BioClinicalBERT enables the extraction of deep semantic representations from unstructured clinical text, effectively capturing the nuanced relationships between patient profiles and trial eligibility criteria. The encoding process leverages the [CLS] token output from the final hidden layer to generate a dense, fixed-size vector embedding for each input text. The overall architecture of BERT, used as the foundational model in this work, is illustrated in Figure 1 below.  

Once patient queries and trial descriptions are transformed into embeddings, the system utilizes FAISS (Facebook AI Similarity Search) to perform efficient approximate nearest neighbor (ANN) retrieval. By precomputing and indexing all trial embeddings offline, the system ensures scalable and rapid similarity search even across large databases. When a new patient query is received, it is encoded in real-time and compared against the indexed trial embeddings using cosine similarity. The top-k most relevant trials are then retrieved and ranked based on their similarity scores.  

To improve interpretability and clinician trust, the architecture integrates a Retrieval-Augmented Generation (RAG) module based on Flan-T5. This lightweight generative model generates natural language explanations that justify why each trial is recommended for a specific patient, providing clear and human-understandable rationales. Additionally, an explainability module highlights the most significant tokens or features within both the patient query and the trial text that contributed to the final matching decision.  

This comprehensive architecture combines semantic language understanding, scalable retrieval, and transparent explainability, resulting in a robust and clinically meaningful trial matching system.  
