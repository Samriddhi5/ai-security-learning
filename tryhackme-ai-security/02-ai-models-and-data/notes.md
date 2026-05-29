# Room 2 - AI Models & Data

**Platform:** TryHackMe
- **Path:** AI Security
- **Difficulty:** Medium
- **Status:** ✅ Completed
- **Link:** https://tryhackme.com/room/aimodelsdata

---

## Key concepts

### Training data sources
| Source | Trust profile |
|---|---|
| Web scraping | Low - no curator, content changes after collection |
| Licensed datasets | Medium - terms often unclear, users rarely consented |
| Synthetic data | Variable - ~12% of fine-tuning datasets contain LLM-generated content |
| Internal corpora | Higher - direct control, but direct liability if mishandled |

- Most widely used corpus: **Common Crawl** (free, public web crawl archive)
- GPT-3: 60% tokens from filtered Common Crawl
- LLaMA 4: 40 trillion tokens across 200 languages

### Data provenance
Three questions provenance must answer:
1. Where did it come from?
2. When was it collected?
3. Has it been modified since?

- Data Provenance Initiative audited 1,800+ datasets
- 70%+ of licenses listed as "Unspecified"
- 66% of labeled licenses were miscategorised

### ML-BOM (Machine Learning Bill of Materials)
- AI equivalent of SBOM (Software Bill of Materials)
- Documents: dataset sources, licenses, PII categories, filtering decisions
- Adoption still early - most orgs deploying third-party models have none

### PII in training data
- Truffle Security scanned Dec 2024 Common Crawl (400TB, 2.67B web pages)
- Found ~12,000 live, verified API keys and passwords
- Once baked into model weights - cannot be patched out post-deployment

---

## Model building concepts

### Epochs and overfitting
- **Epoch** - one complete pass of training algorithm through entire dataset
- **Overfitting** - model memorises training data instead of learning general patterns
- Security risk: overfit models more likely to reproduce sensitive training data verbatim

### Model validation
- Validation set = held-back data never used for training
- Catches overfitting early - if training accuracy climbs but validation plateaus = overfitting
- Skipping validation = unknown real-world behaviour = security risk

### Post-training optimisation
| Technique | What it does | Security risk |
|---|---|---|
| Pruning | Removes low-contribution parameters | Changes model behaviour post-training, rarely documented |
| Quantisation | Reduces weight precision (32-bit → 8-bit) | Degrades safety alignment; backdoor defences may fail |

- Quantisation often applied by third-party team after training
- Organisation downloading quantised model inherits unknown behaviour modifications

### Federated learning
- Model trained across decentralised devices - only weight updates sent centrally, not raw data
- Privacy benefit: no raw data leaves participants
- Security risk: participants can submit poisoned local updates (manipulated gradients)
- Shifts question from "who controls the data?" to "who controls the aggregation?"

---

## Pre-trained models and fine-tuning

### Fine-tuning
- Take pre-trained base model → continue training on smaller task-specific dataset
- Changes: task-specific behaviour, tone, domain knowledge
- Does NOT change: base model weights shaped by pre-training data you never audited

### The inheritance problem
Three concrete risks when fine-tuning:

**1. Safety alignment erodes**
- Stanford/Princeton: safety mechanisms compromised by fine-tuning on as few as 10 adversarial examples (cost: under $0.20)
- Even benign fine-tuning on legitimate data degrades safety as side effect
- Safety alignment doesn't snap - it wears down gradually

**2. Specialisation increases attack surface**
- Cisco: fine-tuned models measurably more susceptible to prompt injection than base models
- Narrowed focus reduces resilience to unexpected tokens

**3. Version is rarely tracked**
- Fine-tuning targets a specific base model checkpoint
- If that checkpoint contained a backdoor, every derivative inherits it

---

## Models as black boxes

- Model weights = billions of floating-point numbers
- Cannot be read, disassembled, or audited like source code
- Security testing = sampling behaviour, not auditing it
- Cannot tell you what model will do on inputs you haven't tried yet

### Model cards
Structured documentation accompanying a model:
| Section | What it should tell you |
|---|---|
| Training data | Sources, filtering, known gaps |
| Intended use | What it was designed for (and wasn't) |
| Evaluation results | Performance across conditions |
| Known limitations | Where it underperforms |
| Bias assessment | Where skew was introduced |
| Licence | What you're legally permitted to do |

**The gaps:**
- Model cards are voluntary - no regulatory requirement
- Frequently incomplete, vague, or absent
- Sparse/missing model card = warning sign, not inconvenience
- "In security, hope is not a control"

---

## Questions answered
- Data Provenance = ability to answer where data came from, when collected, whether modified
- Common Crawl = most widely used public corpus
- ML-BOM = AI equivalent of SBOM
- Epoch = one complete pass through entire dataset
- Overfitting = memorising training data vs learning general patterns
- Quantisation = reduces numerical precision of weights
- Federated Learning = trains across decentralised devices, sends only weight updates
- Fine-tuning = continuing to train pre-trained model on task-specific dataset
- Pre-trained Model = already trained on large general-purpose dataset
- Model Card = documentation artifact describing model, build process, limitations
- Weights = billions of floating-point numbers making up a trained model

---

## Connection to KAICSF
- Data provenance → KAICSF Pillar 1: AI asset inventory includes dataset sources
- PII in training data → KAICSF HIPAA use case: PHI detection and data minimisation
- Quantisation security risk → KAICSF Pillar 4: supply chain safeguards
- Fine-tuning inheritance → KAICSF vendor risk assessment checklist
- Model cards → KAICSF compliance layer: evidence collection guide for auditors
- Federated learning poisoning → KAICSF threat taxonomy: training data poisoning

---

## Questions to explore further
- How do you detect poisoned gradient updates in federated learning?
- What tools exist to scan model weights for embedded PII or credentials?
- How does NIST AI RMF address the model card gap?
- What does a well-formed ML-BOM actually look like in practice?
