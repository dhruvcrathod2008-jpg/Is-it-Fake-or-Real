# ScamShield — Unified Smishing & Document Forgery Detector

> A combined scam-detection system that checks both the *message* and the *document* a scam usually arrives with — because real-world fraud rarely uses just one trick at a time.

## The Problem

SMS and WhatsApp scams in India increasingly combine two tactics at once: an urgent, manipulative text message *and* a fake supporting document — a forged payment receipt, a fabricated offer letter, a doctored government notice — sent to make the scam believable. Most existing tools check only one half of this picture (a spam filter looks at text; a forensic tool looks at images) but nobody validates them together, even though that combination is exactly how these scams are designed to work.

## What This Project Does

ScamShield takes a suspicious message and any document/image attached to it, and analyzes both in a single pass:

- **Text analysis** — classifies the message as legitimate or scam-like using an NLP model trained on labeled smishing data, with explainable flags (urgency language, suspicious links, impersonation patterns).
- **Document analysis** — checks the attached image or PDF for tampering using Error Level Analysis (ELA), metadata forensics (creation/edit timestamps, editing software fingerprints), and visual inconsistency detection.
- **Combined risk score** — instead of two disconnected verdicts, the two signals are weighted together into one trust score, since a borderline-suspicious message *plus* a borderline-suspicious document is a much stronger signal than either alone.

## Why It Matters

Document-backed scams (fake fee receipts, fake offer letters, fake KYC notices) are a growing and under-addressed category of fraud. By validating the message and its "proof" together, this tool models how these scams actually work in practice, rather than treating text and document fraud as separate problems.

## Tech Stack

- **Python** — core logic
- **scikit-learn** — TF-IDF + classification for SMS/text analysis
- **OpenCV / Pillow** — Error Level Analysis and image forensics
- **exifread / pikepdf** — metadata extraction from images and PDFs
- **Gradio** — interactive web interface
- **Hugging Face Spaces** — free deployment

## Status

🚧 Built as a one-week academic cybersecurity project. See [Limitations & Future Work](#limitations--future-work) for known constraints.

## Limitations & Future Work

- Trained on a limited public smishing dataset; real-world coverage of Indian-context scam phrasing is partial.
- Document forensics relies on ELA and metadata heuristics rather than a trained forgery-detection model — effective for common tampering but not exhaustive.
- Risk-score weighting is currently rule-based; a logical next step is learning the weights from labeled combined examples.
