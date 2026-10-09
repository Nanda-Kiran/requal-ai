# Requal

**Automated eval infrastructure for critical AI systems, from building golden datasets to gating releases.**

[requal.ai](https://requal.ai): see how it works and book a demo

## Why

AI systems now take actions as well as answer questions: they issue refunds and credits, place orders and change accounts. Teams change the model, prompt or tools often, and any change can break behaviour that used to work. Requal evaluates a candidate release by what it actually did (the actions it took and the state it left behind, not its own account of them) and turns the result into a signed release authorisation that a gate in the deployment pipeline checks before the release goes out.

## What is built

The platform source is private (`Requal-Inc/requal-platform`). It includes:

- **Evaluation engine (`rq`)**: statistics, verdicts, sealed runs, and `rq verify` to re-check them.
- **Versioned contracts**, a **qualification-policy evaluator**, and a standalone **verifier** (`requal-verify`) that recomputes the engine verdict and the policy decision from the full evidence.
- **Agent test environments**: resettable state, sandboxed tools, a tool gateway, fault injection and assertions.
- **Runner (`rqr`)** with a signer (Ed25519-signed statements) and a **deployment gate** (`rqr authorize-check`), with pipeline examples for GitHub, GitLab and generic CI.
- **Control plane** and **web app**.
- **Chaos suite** and **recovery drills**.

## How it works: the end-to-end demo

```
candidate release
  -> rq evaluates it in an agent test environment
  -> the qualification policy decides
  -> rqr signs the statement (Ed25519)
  -> named approvers authorise the release
  -> the deployment gate admits or blocks it
```

In the demo, a faulty support-agent release is caught: it issues a duplicate refund after a timeout and attempts a refund it is not entitled to make. Its fix is qualified, named approvers authorise it in the web app, and the deployment gate admits the fix and blocks the faulty release. Support agents that take account actions are the first worked example, not the limit: Requal is designed for critical AI systems in general.

## Status

Requal is pre-launch.

- The platform was built Oct 1–4, 2026 (244 commits) around Requal's evaluation engine, which came from its own earlier repository. The founder built it by running AI coding agents as his engineering team.
- So far the platform has run only on the build machine, with scripted models.
- Not yet done: cloud staging deployment, real sign-in, and independent reviews.

## Roadmap

- Hosted execution on Requal's cloud as the default, with the runner (`rqr`), already built to run in a customer's own cloud, as the enterprise option.
- An agentic harness that turns a team's production data into a private benchmark (golden datasets).
- A library of test environments.

## Founder

**Nanda Kiran Velaga**: MS in Applied Machine Learning, University of Maryland, College Park (2026). As an AI intern at Ford's AI Advancement Center (summer 2025), he built and deployed an LLM agent for Ford's vehicle shopping experience, and built the evaluation and observability harness for it (automated test suites, trajectory tracing), which cut evaluation time by about 60%. That harness is where he first ran into the problem Requal works on.

[GitHub](https://github.com/Nanda-Kiran) · [LinkedIn](https://www.linkedin.com/in/nandakiranvelaga)

## This repository

This repository holds Requal's static pages (hand-written HTML with inline CSS, no dependencies), which GitHub Pages publishes from the root of `main`. The product site is [requal.ai](https://requal.ai).
