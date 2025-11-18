---
name: data-science
description: Master machine learning, AI, data science, and GenAI applications. Learn ML engineering, prompt engineering, data pipelines, model deployment, and LLM fine-tuning. Use when building AI/ML systems, working with data science, or implementing generative AI.
---

# Data Science & AI Skill

## Quick Start

Build AI and machine learning systems from data pipeline to production deployment.

### Fastest Path: Prompt Engineering (2-4 months) → AI Engineer

```python
# Python ML Pipeline with Scikit-learn
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

# Load and split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Create pipeline
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier(n_estimators=100))
])

# Train
pipeline.fit(X_train, y_train)

# Evaluate
accuracy = pipeline.score(X_test, y_test)
print(f"Accuracy: {accuracy:.2%}")
```

## What You'll Learn

### Foundation Level (Weeks 1-12) - FASTEST TRACK
- **Prompt Engineering** - LLM mastery, few-shot learning, RAG (2-4 months)
- **Python Fundamentals** - Data types, libraries, scripting
- **SQL Basics** - Querying, analysis, data exploration
- **Statistics** - Probability, hypothesis testing, distributions

### Intermediate Level (Weeks 13-32)
- **Data Processing:** Pandas, NumPy, data cleaning, ETL
- **Machine Learning:** Scikit-learn, model evaluation, hyperparameter tuning
- **Data Visualization:** Matplotlib, Seaborn, interactive dashboards
- **Databases:** SQL optimization, data warehousing concepts
- **GenAI:** LLM fine-tuning, prompt engineering at scale, RAG systems

### Advanced Level (Weeks 33-52+)
- **Deep Learning:** TensorFlow, PyTorch, neural networks
- **MLOps:** Model deployment, monitoring, A/B testing
- **Distributed Systems:** Spark, Hadoop, cloud computing
- **Advanced NLP:** Transformers, BERT, LLM applications
- **Production ML:** Model serving, inference optimization

## AI/ML Technologies

**Programming:** Python, SQL, R, Scala

**Data Processing:**
- Pandas, NumPy, Polars
- Apache Spark, Dask
- SQL (PostgreSQL, BigQuery)

**Machine Learning:**
- Scikit-learn, XGBoost, LightGBM
- TensorFlow, PyTorch, JAX
- Hugging Face Transformers

**LLM & GenAI:**
- OpenAI (GPT-4, GPT-4o)
- Anthropic Claude
- Open-source (Llama, Mistral, Llama 2)
- Vector DBs (Pinecone, Weaviate, Milvus)
- LangChain, LlamaIndex

**MLOps:**
- MLflow, Weights & Biases
- Docker, Kubernetes
- AWS SageMaker, Vertex AI, Modal
- Airflow, Prefect, Dagster

**Analytics & BI:**
- Tableau, Power BI, Looker
- Metabase, Apache Superset
- Plotly, Dash

## Learning Paths

**Fastest Route (2-4 months):** Prompt Engineering → AI Applications
**ML Route (12-18 months):** Data Analyst → Data Engineer → ML Engineer
**Enterprise Route (18-24 months):** Full-stack ML engineering with MLOps

```python
# LLM Integration with LangChain
from langchain.llms import OpenAI
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

llm = OpenAI(temperature=0.7)

template = """Question: {question}

Answer:"""

prompt = PromptTemplate(template=template, input_variables=["question"])
chain = LLMChain(prompt=prompt, llm=llm)

result = chain.run(question="What is machine learning?")
print(result)
```

## Learning Outcomes

After completing this skill:

✅ Build end-to-end ML pipelines
✅ Master prompt engineering and LLMs
✅ Implement data processing and analysis
✅ Train and evaluate ML models
✅ Deploy models to production
✅ Build RAG and GenAI applications
✅ Optimize model performance
✅ Monitor and maintain models
✅ Work with big data systems
✅ Implement MLOps practices

## Project Examples

1. **Predictive Analytics** - Classification/regression models
2. **Chatbot with RAG** - LLM with custom data retrieval
3. **Image Classification** - Deep learning with CNNs
4. **Time Series Forecasting** - ARIMA, Prophet, LSTM
5. **Recommendation System** - Collaborative filtering, embeddings
6. **Sentiment Analysis** - NLP with transformers
7. **Multi-Agent System** - Autonomous AI agents

## When to Use This Skill

- Building AI/ML applications
- Data analysis and storytelling
- LLM and GenAI applications
- Model training and evaluation
- MLOps and model deployment
- Big data processing
- BI and analytics
- Team ML training

## Salary Insights

| Role | Salary | Time | Demand |
|------|--------|------|--------|
| Prompt Engineer | $80K-200K | 2-4 mo | 🔥 Highest |
| AI Engineer | $120K-250K | 6-12 mo | 🔥 Highest |
| ML Engineer | $130K-280K | 18-24 mo | 🔥 Very High |
| Data Engineer | $110K-240K | 12-18 mo | 🔥 Very High |
| Data Scientist | $100K-220K | 12-18 mo | ✅ Stable |

## Related Agents

- **Backend Agent** - Model serving APIs
- **Infrastructure Agent** - GPU clusters, Kubernetes
- **Database Agent** - Data warehouse design

## Resources

**Official Docs:**
- Scikit-learn: https://scikit-learn.org
- PyTorch: https://pytorch.org
- TensorFlow: https://tensorflow.org
- HuggingFace: https://huggingface.co

**Books:**
- *Hands-On Machine Learning* (Aurélien Géron)
- *Deep Learning* (Goodfellow, Bengio, Courville)
- *Designing Machine Learning Systems* (Chip Huyen)

**Courses:**
- Andrew Ng ML Specialization
- Fast.ai
- Coursera ML courses
- DeepLearning.AI

---

**Status:** Comprehensive AI/ML skill covering 10 roles and 1,000+ skills
