# Room 1 : AI/ML Security Threats

**Platform:** TryHackMe
- **Path:** AI Security
- **Difficulty:** Medium
- **Status:** ✅ Completed
- **Link:** https://tryhackme.com/room/aimlsecuritythreats

---

## Key concepts

### AI/ML hierarchy
- **AI** - overarching field: machines mimicking human intelligence
- **ML** - subfield of AI: learns from data without explicit instructions
- **DL** - subfield of ML: self-learning via neural networks, no human labeling needed
- **LLMs** - advanced DL models built on transformer neural networks

### ML algorithm categories
- **Supervised** - labeled data, classification/regression tasks
- **Unsupervised** - unlabeled data, finds hidden patterns
- **Semi-supervised** - combines labeled and unlabeled data
- **Reinforcement learning** - rewards correct decisions, penalizes mistakes

### Neural networks
- Input layer → hidden layers → output layer
- Connections = synapses, weighted by importance
- Deep learning = neural network with 3+ layers

### LLMs
- Pre-training phase: processes massive datasets (GPT-3 = 2,600 years of reading)
- Uses backpropagation to fine-tune parameters
- RLHF (Reinforcement Learning from Human Feedback) refines outputs
- Transformer neural networks (Google 2017 - "Attention is All You Need") enable parallel processing

---

## AI security threats

### Vulnerabilities in AI models
| Threat | Description |
|---|---|
| Prompt injection | Overrides original model instructions for malicious purposes |
| Data poisoning | Corrupts training data to produce incorrect/biased outputs |
| Model theft | Clones a model by querying its API and training a replica |
| Privacy leakage | Model inadvertently reveals sensitive training data |
| Model drift | Model performance degrades over time as data changes |

### AI-enhanced attacks
- **Malware** - generative AI enables instant malware generation
- **Deepfakes** - replicates voice/appearance to bypass authentication
- **Phishing** - AI generates fluent, convincing, context-aware phishing emails

---

## Defensive AI

- IBM Cost of Data Breach report: AI saves $2.2M average per breach
- AI cuts breach identification and containment time by **108 days**
- Only **24% of gen AI initiatives are currently secured**

### How AI helps defenders
- **Analysis** - detects anomalies in network traffic (Splunk, Microsoft Defender)
- **Prediction** - automates phishing detection and blocking
- **Summarization** - digests incident reports, draws correlations
- **Investigation** - feeds logs to LLMs for triage and threat hunting

### Securing AI systems
- RBAC and MFA to restrict model access
- Encrypt training data like any sensitive data
- Implement ISO/IEC 27090 for AI-specific security standards
- Monitor models using explainability tools: **SHAP** and **LIME**

---

## MITRE ATLAS framework
- AI-specific version of MITRE ATT&CK
- Maps adversarial techniques targeting AI systems

---

## Questions answered
- Semi-supervised learning combines labeled and unlabeled data
- Input layer handles incoming raw data
- Deep learning doesn't require human-labeled data
- Synapses = weighted connections between nodes
- LLMs are powered by transformer neural networks
- Pre-training = first LLM training stage
- ATLAS = MITRE framework for AI cyber threats
- Model theft = cloning via API queries
- Deepfake = replicates voice/appearance
- AI cuts breach time by 108 days
- Threat hunting benefits from AI imagining attacker behavior
- SHAP and LIME = explainability tools for model monitoring

---

## Connection to KAICSF
- Prompt injection → addressed in KAICSF Pillar 2 (Security Controls)
- Data poisoning → addressed in KAICSF Risk Layer threat taxonomy
- Model drift → KAICSF KPI: accuracy delta week-over-week
- Privacy leakage → KAICSF HIPAA use case: PHI detection in output pipeline
- Model theft → addressed in KAICSF Pillar 1 (AI asset inventory)

---

## Questions to explore further
- How does MITRE ATLAS map to KAICSF threat categories?
- What specific Splunk queries detect model anomalies?
- How does differential privacy work in practice for LLM training data?
