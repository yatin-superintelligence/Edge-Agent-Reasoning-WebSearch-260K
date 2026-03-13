[**Access the full dataset and data viewer on Hugging Face here.**](https://huggingface.co/datasets/yatin-superintelligence/Edge-Agent-Reasoning-WebSearch-260K)

# Edge Agent Reasoning WebSearch 260K

## Abstract

The **Edge-Agent-Reasoning-WebSearch-260K** dataset is a massive, synthetically expert-engineered corpus of **over 700 Million tokens**, designed to train small, local models (SLMs) and edge-deployed agents in advanced problem deconstruction and self-aware reasoning.

Rather than training a model to execute instructions directly—which often leads to hallucinations when context is missing—this dataset trains a model to act as a **preparatory router** or **System 2 thinking agent**. When presented with a complex, domain-specific instruction, the agent's job is to systematically break down the request, identify its own knowledge gaps, formulate specific ambiguities, and construct expert-level web search queries. This preparatory reasoning equips a secondary, more capable frontier model with the exact verified context needed to execute the final task flawlessly.

<img src="Small Agent Working for Frontier.jpg" alt="Small Agent Working for Frontier" width="100%"/>

## Dataset Statistics (OpenAI cl100k_base)

This collection is built for deep, zero-shot generalization. Rather than focusing on simplistic conversational exchanges, the dataset prioritizes exhaustive, multi-stage reasoning trajectories grounded in rigorous professional constraints. Engineering this level of structural density and internal validation consumed nearly **1.5 Billion tokens** in computational bandwidth.

**Summary:**

- **User Prompts:** 42,585,076 Tokens
- **Agentic Reasoning:** 646,883,262 Tokens
- **Total Rows (Observations):** 260,293
- **Compute Spend (Generation Cost):** ~1.47 Billion Tokens
- **Grand Total Dataset Tokens (All Schema Columns):** ~712.9 Million Tokens
- **Format:** Parquet (`.parquet`)


## What Does This Dataset Solve?

In distributed agentic architectures, delegating raw user instructions directly to an internet-facing frontier model is inefficient. It wastes expensive compute on vague prompts and fails when the model lacks highly localized context (e.g., specific software versions, niche industry constraints, or local OS environments).

**Edge-Agent-Reasoning-WebSearch-260K** addresses this by teaching models self-auditing and verification planning. It trains models to overcome the common LLM flaw of overconfidence by forcing them to state what they *believe* they know, immediately followed by what they must *verify*.

### Core Capabilities

- **Reasoning Fine-Tuning (RFT):** Enhancing the step-by-step reasoning capabilities of 7B-14B parameter models, forcing them to "think before they act."
- **Self-Awareness & Humility:** Training models to treat their own confidence as a signal for verification, rather than evidence of correctness.
- **Search Query Generation:** Training retrieved-augmented generation (RAG) routers to formulate dense, expert-level queries rather than naive keyword matching.
- **Prompt Interception:** Training classifiers to intercept poorly constructed or ambiguous user prompts and demand clarification before consuming expensive API credits.


## The 5-Stage Reasoning Structure

Every row in the dataset contains a dense, 2,000 to 5,000-word reasoning trajectory (`agent_reasoning`). This structure is designed to simulate the internal deliberation of an expert actively planning a complex technical task, ensuring the model output is grounded in self-awareness, factual verification, and deep contextual understanding.

The reasoning is broken down into five highly analytical stages:

**1. Understanding the request**<br>
Teaches the model to correctly identify the core objective while fully internalizing constraints. This stage ensures the model does not gloss over critical environmental factors (e.g., operating system constraints, user role, specific software versions) before formulating a plan.

**2. What I believe I know — and what I'm uncertain about**<br>
Instills self-awareness and humility. Instead of hallucinating answers, the model is trained to aggressively audit its own internal knowledge base. It learns to cleanly separate established facts from assumptions, treating its own uncertainty as a trigger for external verification rather than a reason to guess.

**3. Ambiguities in the request**<br>
Trains the model in prompt interception and clarification. It learns to spot missing parameters, vague instructions, or conflicting constraints that would lead to failure if executed blindly. This allows the routing agent to "push back" and ask the user for clarity before wasting compute or causing destructive side-effects.

**4. Everything I need to confirm before responding**<br>
Establishes a strict verification protocol. The model actively generates an explicit checklist of facts, dependencies, API statuses, and documentation it must review. This stage acts as a blueprint for the final execution, ensuring that every subsequent action is backed by verified reality.

**5. Web search queries**<br>
Acts as the bridge between internal reasoning and external retrieval. By generating 10 to 20 highly specific, keyword-dense queries, the model sets up a downstream Retrieval-Augmented Generation (RAG) pipeline to feed a frontier model for success. These queries are explicitly designed to bypass generic SEO content and land directly on highly technical documentation, error logs, or source code.

## The Combinatorial Matrix & Sampling

To prevent the semantic collapse often seen in synthetic datasets (where models generate repetitive, homogenous scenarios), the prompt instructions were sourced from a custom-built, 7-dimensional combinatorial matrix.

**The Matrix Schema:**

1. **Industry** (e.g., Biotech, Astrophysics, DevOps, Corporate Finance)
2. **Professional Role** (Scope-locked to the Industry)
3. **Software Stack** (Determined by Domain Purity rules—some roles get single tools, others get mixed workflows)
4. **Task Type** (Realistic operations for the tool and role)
5. **Operating System** (OS constraints matched to the industry, e.g., Embedded Linux vs. macOS)
6. **Difficulty** (Low to Impossible)
7. **Risk Level** (Safe to Catastrophic)

**Scale & Sampling:**
The matrix utilizes 7 distinct large prime numbers to cryptographically scramble and hash these dimensions, creating a deterministic search space of **1,000,000,000 (1 Billion) valid permutations**.

From this massive possibility space, I sampled **only ~260,000 unique rows** for this dataset. This extremely low sampling rate (0.026%) virtually guarantees that there are no overlapping duplicates or repetitive thematic loops, resulting in a dataset with an exceptionally high degree of zero-shot diversity.

## Dataset Diversity: 200+ Roles

To ensure the resulting models generalize across the entire spectrum of human knowledge work, the dataset is grounded in highly specific, realistic user profiles. It avoids generic "Assistant" personas in favor of explicit professional domains with corresponding environmental constraints.

### Operating System Environments

The dataset escapes the trap of generic "web browser apps" by enforcing highly specific local environments, ensuring training covers the full spectrum of modern and legacy deployment targets. Problem-solving trajectories are explicitly contextualized across **Apple ecosystems** (macOS, macOS Monterey, macOS Ventura, macOS Sonoma, macOS Sequoia, iOS, iOS 16, iOS 17, iOS 18), **Windows environments** (Windows, Windows 7 (Legacy), Windows 10, Windows 11, Windows Subsystem for Linux), and **Server infrastructures** (Windows Server, Windows Server 2019, Windows Server 2022). It deeply covers **Linux distributions/environments** (Linux, Ubuntu, CentOS, RHEL, Rocky, Fedora, Debian, and Embedded Linux) alongside dedicated **Cloud terminals** (AWS CloudShell, Google Cloud Shell, Azure Cloud Shell, OCI Cloud Shell). The dataset further embeds mobile and specialized hardware constraints, covering **Android** (Android, Android 12 through Android 16), **ChromeOS**, and highly specific tablet use-cases like **iPadOS** (Clinical, Field Work, and for Procreate). This exhaustive coverage forces the routing agent to learn profound cross-platform contextual awareness, tailoring command-line prompts, software troubleshooting, and hardware constraints to the exact operating system of the simulated user.

### Professional Roles (Grouped by Frequency)

**> 2,000 tasks**
Unknown, DevOps Engineer, Industrial Engineer, Security Analyst, IT Support Specialist, System Administrator, IT Technician, Security Engineer, Safety Officer, Platform Engineer, Quality Engineer, Electrical Engineer, Maintenance Engineer, Research Scientist, Manufacturing Engineer, Plant Manager, Business Analyst, Project Manager, CEO, HR Manager, Program Manager, Executive Assistant, Office Manager, Product Manager, Talent Acquisition Specialist, Recruiter, Management Consultant, COO, General Manager, Operations Manager, Robotics Engineer, Lab Technician, Supply Chain Analyst, Mechanical Engineer, Data Scientist

**1,300 to 2,000 tasks**
Software Architect, Mobile Developer, Frontend Developer, QA Engineer, Full Stack Developer, Backend Engineer, Engineering Manager, Postdoctoral Researcher, Game Designer, Visual Designer, Artist, Art Director, Photographer, Fashion Designer, Animator, Illustrator, Creative Director, Graphic Designer, Architect, Construction Manager, BIM Manager, Interior Designer, Project Engineer, Student, Content Creator, Site Manager, Genealogist, Teacher, Volunteer, Photographer (Hobbyist), Traveler, Homeowner, Gamer, Parent, Musician (Hobbyist), DIY Enthusiast, University Researcher, Retiree, Blogger, Writer (Hobbyist), Structural Engineer, Hobbyist, Streamer, Professor, Urban Planner

**1,000 to 1,300 tasks**
Medical Doctor, Clinical Data Manager, Clinical Research Associate, Civil Engineer, Procurement Manager, Content Manager, Investment Banker, PR Manager, SEO Specialist, CFO, Social Media Manager, Financial Analyst, Customer Success Manager, Product Marketing Manager, Actuary, Tax Advisor, Real Estate Broker, Marketing Director, Medical Technologist, VP of Sales, Loan Officer, Risk Manager, Wealth Manager, Brand Manager, CMO, Controller, SDR, Accountant, UX Designer, Sales Manager, Nurse, Auditor, Account Executive, Pharmacologist, Bioinformatician, Geneticist, Immunologist, Biochemist, Data Engineer, ML Engineer, Data Analyst, AI Researcher, Anesthesiologist, Pharmacist, Surgeon, Toxicologist, Molecular Biologist

**500 to 1,000 tasks**
Pathologist, PhD Student (Biology), Microbiologist, Epidemiologist, Radiologist, Virologist, Biologist, Film Editor, Video Editor, Director, Motion Designer, Dentist, GIS Analyst, Geologist, Climate Scientist, Remote Sensing Analyst, Environmental Scientist, PhD Student (Physics), Physicist, Podcast Host, Mixing Engineer, Composer, Mastering Engineer, Voice Actor, Sound Designer, Music Producer, Audio Engineer, Meteorologist, Oceanographer, Hydrologist, Materials Scientist, Chemist, Analytical Chemist, Veterinarian, VFX Artist, Soil Scientist, Process Engineer, Quality Control Chemist, Medicinal Chemist, Cinematographer, Chemical Engineer, Colorist, Spectroscopist, Formulation Scientist, Polymer Scientist, Geophysicist, Ecologist, Radio Astronomer, PhD Student (Astronomy)

**100 to 500 tasks**
Observatory Scientist, Astrophysicist, Planetary Scientist, Astronomer, Data Scientist (Astronomy), Cosmologist, Computational Astrophysicist, Observational Astronomer, Space Scientist, Seismologist, Wildlife Biologist, Agronomist, Graphics Programmer, Technical Artist, Game Developer, Gameplay Engineer, Level Designer, Game Programmer, PhD Student (Chemistry), Computational Chemist, Paralegal, Attorney, Compliance Officer, Forensic Analyst, Prosecutor, Detective, Judge, Contract Manager, Legal Assistant, Legal Counsel, Defense Attorney, General Counsel

## Data Structure / Schema

The dataset is distributed natively chunked in `.parquet` files.

<div style="margin-bottom: -35px;"></div>

| Column | Type | Description |
| :--- | :--- | :--- |
| `batch_index_id` | int64 | Identifier tracking the sample back to the source prompt batch. |
| `role` | string | The simulated professional role of the user issuing the prompt. |
| `industry` | string | The conceptual industry sector to which the task belongs. |
| `os` | string | The operating system environment relevant to the task constraints. |
| `user_prompt` | string | The raw, initial instruction or query provided by the synthetic user. |
| `agent_reasoning` | string | The 2,000-5,000 word internal reasoning output. |
<h2 style="margin-top: -5px !important;">Developer & Architect</h2>

This dataset was created by Yatin Taneja, an AI Systems Engineer, Superintelligence Researcher, Musician (Dubstep Artist), Rapper, and Poet.

When you blend art and engineering, you get systems that can actually think like humans. I built this dataset to break models out of their rigid, robotic patterns and force them to approach problems with the disciplined structure of a researcher, the foresight of an engineer, and the lateral creativity of an artist.

To all the open-source engineers, AI researchers, and builders pushing the boundaries of what AI models can do, I encourage you to use this data to train and task agents that don't just execute blindly, but actually *reason*. Models that audit their own knowledge, respect their constraints, and solve problems with humility, precision, and nuance will build the future of edge-deployed superintelligence.

### Weblinks

- **[IM Superintelligence](https://www.imsuperintelligence.ai):** Visit my central knowledge hub hosting other massive open datasets and over 2,000 articles exploring Superintelligence, cognitive architectures, quantum computing, distributed networks, algorithmic optimization, and the future of the global education sector, all authored through a custom 8-step multi-model agentic infrastructure I engineered.
- **[Yatin Taneja | Professional Portfolio](https://www.yatintaneja.in):** View my professional portfolio for a comprehensive overview of my skills, industry experience, and software prototypes as part of my ongoing engineering work in full-stack AI agents and applications.
- **[LinkedIn](https://www.linkedin.com/in/yatintaneja-pro/):** Connect on LinkedIn to collaborate on advanced autonomous systems, enterprise AI implementations, or to follow my ongoing research.


## License & Usage

This dataset is released under the **MIT License**.

Designed for open research in multi-agent orchestration, test-time compute scaling (System 2 thinking patterns), and robust SLM fine-tuning. You are free to use this dataset for academic, personal, and commercial model training applications, provided the original license and copyright notice are preserved.