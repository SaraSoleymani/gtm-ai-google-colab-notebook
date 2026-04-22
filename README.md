# GTM AI: Fine-Tuning Phi-2 for MEDDIC-R Qualification Extraction

Practical, hands-on Colab notebooks for sales, GTM, and revenue teams building with AI.

This repository is the companion to the **Building with Agentic AI** series published on Medium and LinkedIn — a 10-article arc covering everything from problem selection to multi-agent systems, fine-tuning, MCP, and the real cost of running AI in production.

Each notebook is self-contained, runnable on Google Colab with a free T4 GPU, and anchored to a real GTM use case.

---

### Article 8: Make Your Intelligence Layer Your MOAT: Fine-Tuning LLMs for GTM with a Full Colab Build
##Fine-Tuning Phi-2 for MEDDIC-R Qualification Extraction
**`apex_meddicr_finetune_Phi-2.ipynb`**

Fine-tunes Microsoft's Phi-2 (2.7B parameters) using LoRA to extract structured qualification records from raw sales call transcripts, following a proprietary MEDDIC-R schema that no base model has ever seen.

**Use case:** A fictional company, Apex Revenue Intelligence, runs a revenue intelligence platform where reps need to populate a custom MEDDIC-R qualification record after every call. Standard prompting and RAG produce inconsistent output at scale. Fine-tuning moves the qualification logic into the model weights.

**What the notebook covers:**
- Synthetic dataset generation: 150 transcript/extraction pairs across 5 deal scenarios, 10 companies, and 3 risk levels
- 4-bit quantization with BitsAndBytes to fit Phi-2 on a free T4 GPU
- LoRA adapter configuration targeting attention layers (less than 1% of parameters updated)
- Supervised fine-tuning with Hugging Face TRL SFTTrainer
- Before and after comparison on held-out test examples
- Saving and reloading the LoRA adapter for future use

**Stack:**
- Model: `microsoft/phi-2`
- Libraries: `transformers`, `peft`, `trl`, `bitsandbytes`, `accelerate`, `datasets`
- Environment: Google Colab T4 GPU (free tier)

**Runtime:** Approximately 20 to 30 minutes on a T4 GPU.

**Article:** [Make Your Intelligence Layer Your MOAT — Medium](#) *(link coming)*

---

## The MEDDIC-R Schema

Apex Revenue Intelligence's proprietary qualification framework, used as the fine-tuning target in Article 8.

| Field | Definition |
|---|---|
| **Metrics** | Must include a specific number, percentage, or dollar figure. Vague statements are marked Incomplete. |
| **Economic Buyer** | Full name, title, and engagement status: Engaged or Identified Only. |
| **Decision Criteria** | Top 3 factors ranked in order of importance. |
| **Decision Process** | Steps, owners, timeline, and projected close date. |
| **Identified Pain** | Must be tied to a specific team or business unit. Generic pain is marked Incomplete. |
| **Champion** | Name, title, influence level (Strong / Moderate / Weak), and coaching status. |
| **Risk Score** | Proprietary seventh field. Low / Medium / High based on budget freeze, competing internal initiative, or unengaged economic buyer. |

---

## Pro Tips

Running these notebooks in Colab involves a few common failure points. See the Pro Tips section in each notebook for solutions. Key ones for Article 8:

- `bitsandbytes` CUDA version mismatches — and how to fix them without rebuilding from source
- Why `gradient_checkpointing=True` breaks LoRA training without quantization
- Why `paged_adamw_32bit` requires bitsandbytes and what to use instead
- OOM on T4: sequence length matters more than batch size
- How to detect underfitting vs. overfitting in a small fine-tuning run
- How to benchmark your fine-tuned model against GPT-4o or Claude before declaring success

---

## The Series

This project is part of *Building with Agentic AI*, a 10-article series on building production-grade agentic systems for GTM and sales teams.

- Article 1: How to Pick the Right Problems for AI Agents and Automation
- Article 2: Building AI Agents in Practice: A Sales Outreach Agent with n8n and Claude
- Article 3: Bad Prompt, Good Prompt, Great Prompt: The Practical Guide to Prompt Engineering [+ Sales Agent Example]
- Article 4: The AI Meeting Prep Assistant: From Problem to a Full Product with n8n and v0
- Article 5: RAG for Revenue Teams: From Simple Retrieval to Agentic and Graph RAG
- Article 6: Evals for Agentic AI: How to Know If Your System Actually Works + Hands on n8n JSON Files
- **Article 7: Multi-Agent Systems (this project)**
- **Article 8: Make Your Intelligence Layer Your MOAT: Fine-Tuning LLMs for GTM with a Full Colab Build**
- Article 9: MCP: How Agents Connect to the World | Coming soon |
- Article 10: The Real Cost of Running AI Agents in Production | Coming soon |

---

## How to Run

1. Open the notebook in Google Colab
2. Set runtime to GPU: **Runtime > Change runtime type > T4 GPU**
3. Run all cells in order
4. No local GPU or API key required

---

## About the Series

**Building with Agentic AI** is a practical, builder-focused series for sales, GTM, and marketing practitioners. Each article combines conceptual frameworks with hands-on implementations — no hand-waving, no hypothetical examples.

Follow the series on [Medium](https://sarasoleymani.medium.com/) and [LinkedIn](https://www.linkedin.com/in/sarasoleymani/).

---

## License

MIT
