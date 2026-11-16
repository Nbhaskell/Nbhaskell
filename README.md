# Nathan Haskell, AI Engineer

I build full-stack AI applications with local models: the model reads and writes, tested code makes the decisions, and a person approves anything important.

Open to remote AI engineering and full-stack roles, and to freelance work on AI tools for small businesses.

## Local AI that cites its sources, checks its own answers, and asks before it acts

Six projects, one method. A local model reads and writes. Plain code, with tests, decides what is allowed and checks every figure. A person approves anything that matters. Each project reports its numbers as they came out, on question sets kept apart from tuning, with the limits written down.

Everything runs on one computer with local models through [Ollama](https://ollama.com), mostly `qwen3:8b`. No hosted model is needed.

## The projects

| Project | What it does | One measured result | A stated limit |
|---|---|---|---|
| [rag-project](https://github.com/Nbhaskell/rag-project) | Answers questions about a folder of documents, shows the passages it read, and says "I don't know" when the documents do not cover the question. | 55 of 55 answers right on a held-out set written after tuning. | The Sources line was exactly right for 44 of 55. Prompt injection passed 32 of 45 runs and is not solved. |
| [citewise-markets](https://github.com/Nbhaskell/citewise-markets) | A research copilot for public companies: answers from SEC filings, prices and headlines, with numbered citations and every number checked against its source. | Sealed round 5 (46 cases, run once): 30 of 46 with keywords only, 36 of 46 with the local-model router. | The stopping rule of 85 to 90% on two rounds in a row has not been met. |
| [citecheck](https://github.com/Nbhaskell/citecheck) | A quality check for question-answering systems. It scores retrieval, answers and citations, and it checks its own AI judge. | After a prompt fix, the judge's agreement with fresh hand labels rose from 22 of 30 to 29 of 30. | Small question sets (131 and 44), one labeller, one local judge model. |
| [citedesk](https://github.com/Nbhaskell/citedesk) | A review desk for customer inquiries. It drafts a reply from the business's documents, checks the draft in code, and queues it for a person. Nothing is sent. | No plumbing safety message was missed on any unseen set (43 of 43). | Intent accuracy was 59.5% to 75.8% against a target of 85%. |
| [citetally](https://github.com/Nbhaskell/citetally) | A review desk for invoices and receipts. The model copies printed values; code checks arithmetic, duplicates and dates. Nothing is paid or posted. | 96.7% of header fields exact on 250 sealed documents. | Instruction text hidden in a document was not flagged (0 of 14). |
| [citebook](https://github.com/Nbhaskell/citebook) | A booking chatbot. The model proposes tool calls; a policy gate decides, code computes every price, and the customer confirms with a button. | Attack success on 40 sealed scenarios: 0.0% with all layers, 31.7% without the gate policy and reply checks. | Benign task success was 70.0% against a target of 85%. |

Each README gives the full tables, how each set was made, and what the numbers do not show.

## How they fit together

- **rag-project** is the base. citedesk uses it as its knowledge base, citebook can use it too, and citecheck measures it.
- **citecheck** measures rag-project and citewise-markets with the same harness.
- **citedesk**, **citetally** and **citebook** share one invented business, Kestrel Hollow Plumbing: its inbox, its invoices and its bookings.

## The data

rag-project, citedesk, citetally and citebook use invented data only, and each one says so in its README. citewise-markets downloads real public data (SEC filings, prices, headlines) at run time; the repository holds none of it except in the screenshots. The citecheck question set for citewise-markets quotes short excerpts of public SEC filings. Invented data shows that the machinery works. It does not show how a system behaves with a real business's documents.

## A reading order

1. **rag-project**: retrieval, cited passages and the first held-out evaluation.
2. **citecheck**: how the answers, and the judge that reads them, are measured.
3. **citewise-markets**: the same ideas with real public data and checks on every number.
4. **citedesk** and **citetally**: the model drafts or reads, code checks, a person approves.
5. **citebook**: the model acts through tools, behind a policy gate and a Confirm button.
