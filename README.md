# README vs Reality

## I built an AI-to-smart-contract system, then audited it as if a stranger had written it

Every README is a claim. The code underneath either enforces that claim or it does not. The gap between the two is invisible from the outside, and it is where production failures live.

This is a forensic review of my own prototype: 104 commits, a full-stack application, 13 Solidity files, 262 test declarations, and a public deployment that was live for months. It was, by the usual signals, a success. I took it apart against the boundaries that actually change state and value, found eight design failures, and concluded it should not be relaunched.

I published the review instead of the relaunch.

## Why the usual signals were not enough

A working demo, a green-looking test suite, an active commit history, a polished README, and a live deployment all answer real questions. None of them answers these:

- Does the contract enforce the identity the API checked?
- Which single key can spend, own, finalize, and act for users?
- Can a legitimate action be replayed, raced, or consumed on someone's behalf?
- Does an observed transfer actually satisfy the obligation?
- Where does off-chain truth come from, and who can contest it?

My prototype passed the first set and failed the second. That is the whole point of this repository.

## What the audit found in my own code

The system took a natural-language request, selected among ten fixed contract templates, normalized the result deterministically, and sponsored gas so users could act without paying. The architecture idea was sound: constrain the model to a finite capability schema, then let typed, testable code decide what is allowed.

The enforcement did not match it.

| What the product claimed | What the code enforced |
|---|---|
| "AI builds a dApp" | AI selected and configured a reviewed template; deterministic code deployed it |
| "Gas-sponsored user actions" | Server-held keys submitted transactions, and several contracts accepted a caller-supplied participant identity |
| "Audited before deployment" | Deterministic compatibility and configuration checks ran; no adversarial contract audit existed |

The factory accepted a creator address from its caller without binding it to `msg.sender`. Campaign clones were initialized with the server's deployer wallet as owner, so one credential concentrated sponsorship, custody, ownership, and lifecycle authority. Signed lifecycle messages carried no nonce, expiry, chain, or domain version. Winner selection derived from recent block data. Bids were declared numbers with no custody of the asset being bid.

Read the full evidence, including the trust-boundary reconstruction and all eight findings, in the **[forensic review](forensic-review.md)**.

## The 262-test trap

Thirteen test files contained 262 static `it(...)` and `test(...)` declarations. That is a real inventory of intent, and it is worth something.

It is not 262 passing tests. I never executed them during the review, so I do not claim they pass. Counting declarations and reporting them as coverage is one of the easiest ways to mislead yourself about a codebase, including your own.

## Why I killed it instead of fixing it

Reusing the application boundary would have preserved the assumptions that were actually wrong: server-centred authority, template behaviours whose economics were descriptive rather than enforceable, and a product framing broader than the implementation. Cosmetic repair does not fix a mismatch between what a system says and what it enforces.

The honest claim is not "built an AI contract platform." It is:

> Built a 104-commit prompt-to-template system, reconstructed its real trust boundaries, refused to treat static declarations as executed proof, rejected the unsafe product boundary, and kept only the reasoning that survived.

That is narrower. It is also true, which the first version was not.

## What you can take from this

| Document | What it gives you |
|---|---|
| **[Forensic review](forensic-review.md)** | The complete technical case: reviewed state, trust-boundary reconstruction, eight findings, claim-to-reality corrections, evidence limits |
| **[Production gates](production-gates.md)** | Twelve review questions with the minimum evidence each needs and the symptom of each failure. Domain-agnostic. Run them on your own repository |
| **[Extraction method](method.md)** | A finite workflow for deciding what to keep, rebuild, preserve, or delete across a portfolio of old projects, and how to close the review instead of letting it run forever |

## Where these gates came from

The twelve gates and the method were not invented at a desk. They are the questions that kept recurring while I worked through a portfolio of old projects, mine and others', deciding what deserved to be rebuilt, preserved, or deleted.

**This repository does not evaluate anyone else's work.** No other project is named, linked, ranked, scored, or characterised, and no event is identified. The only implementation criticised here is my own, because it is the only one I have the standing to criticise.

## Evidence boundary

The review was static and read-only. No dependency installation, build, test run, deployment, signature, or state-changing transaction was executed. The reviewed commit is a research snapshot, not a claim about the state at every historical demo. The source repository is private, and **the application was decommissioned before this review was published**, so nothing here describes a reachable system.

The findings describe one prototype. They support no general claim about AI code generation, template-based deployment, or software at large.

## License

Original prose and diagrams are available under [CC BY 4.0](LICENSE.md). No software and no third-party material is licensed here.
