INX: The File That Decides

Challenge

Organizations receive documents every day, including applications, invoices, certificates, forms, and other records.

The challenge is not always reading the document. A document may be incomplete, contain a missing required field, include conflicting values, or belong to the wrong category. Someone still needs to determine what the document means and what should happen next.

Manual review can handle these cases, but it does not scale. Fully automated systems can scale, but may make decisions that are difficult to explain.

Build a document intelligence system that sits between these two approaches.

The system should take a document, extract useful information, check what it found, identify uncertainty, and route the document to an appropriate next action.

A typical flow is:

DOCUMENT
   ↓
UNDERSTAND
   ↓
EXTRACT
   ↓
CHECK
   ↓
DECIDE
   ↓
ROUTE

The system should produce an actionable and traceable decision, not just extracted text.

What to Build

1. Document Input

The system must accept document files such as:

* PDF
* Image

The exact document types are up to your team. Define the scenario your system is designed around.

Examples include:

* Applications
* Invoices
* Certificates
* Registration forms
* Claims
* Internal forms

You do not need to support every possible document type.

2. Document Classification

The system should determine what type of document it has received.

For example:

Input
  ↓
Application
  ↓
Application Processing Workflow

Or:

Input
  ↓
Invoice
  ↓
Invoice Verification Workflow

The classification approach is up to your team.

3. Information Extraction

Extract the information required by your chosen scenario.

The extracted information should be represented in a structured form rather than only as raw text.

For example:

{
  "document_type": "...",
  "applicant": "...",
  "date": "...",
  "reference_number": "...",
  "amount": "...",
  "status": "..."
}

The exact schema is up to you.

4. Missing and Uncertain Information

The system must identify information that is:

* Missing
* Unclear
* Conflicting
* Potentially unreliable

For example:

Required field: Application ID
Status: Missing

Or:

Amount on page 1: ₹12,500
Amount on page 2: ₹15,200
Status: Conflict

Uncertainty must be visible. The system must not silently guess.

5. Decision and Routing

After processing the document, the system should determine what happens next.

For example:

COMPLETE
   ↓
APPROVE / PROCESS

Or:

MISSING INFORMATION
   ↓
REVIEW REQUIRED

Or:

CONFLICT DETECTED
   ↓
MANUAL VERIFICATION

The routing logic should be defined by your team.

6. Workflow Status

A user should be able to understand where a document currently stands.

For example:

Received
   ↓
Processing
   ↓
Verified
   ↓
Approved

Or:

Received
   ↓
Review Required
   ↓
Awaiting Information

The exact workflow is up to you.

Constraints

Document Integrity

The original document must remain accessible.

The processing pipeline must not replace the original document with only the extracted information.

No Silent Decisions

If the system does not have enough information to make a reliable decision, it must communicate that uncertainty.

Do not turn:

Unknown

into:

Approved

simply because the system needs an answer.

Dataset

ARC will not provide a custom document dataset or document-processing server.

You are responsible for providing suitable demonstration inputs.

You may:

* Create synthetic documents.
* Use legally usable public or sample documents.
* Create your own test documents.

Do not use confidential or private documents.

Secrets

Do not commit:

* API keys
* Access tokens
* Passwords
* Private credentials
* .env files containing secrets

Use .env.example when configuration needs to be documented.

Technology

There is no prescribed technology stack.

You may use:

* OCR
* Document parsing
* Computer vision
* Rules
* NLP
* Machine learning
* LLMs
* Local models
* External APIs
* Hybrid approaches

You may use handwriting recognition if you choose.

You do not have to use AI.

The objective is to build a reliable document-to-decision system, not to use the most advanced model available.

Evaluation

Extraction

Can the system reliably obtain the information it needs?

Validation

Can it distinguish valid information from missing, unclear, or conflicting information?

Decision Quality

Does the resulting action follow a clearly defined policy?

Traceability

Can a user understand why a document was routed a certain way?

Human Oversight

Does the system know when it should stop and ask for human review?

Engineering

Can the team explain the architecture, trade-offs, and limitations?

Implementation Choices

The following are deliberately left open:

* Document types
* Field schema
* OCR approach
* Extraction method
* Classification method
* Validation rules
* Confidence strategy
* Workflow design
* User interface
* Storage approach
* Technology stack
* AI usage

There is no prescribed implementation.

Optional Enhancements

The following features are optional:

* OCR for scanned documents
* Handwriting recognition
* Field-level confidence scores
* Human verification interface
* Automatic notifications
* Document comparison
* Duplicate document detection
* Audit trail
* Multi-document processing
* Explainable routing
* Reviewer feedback loop

Core reliability matters more than feature count.

Acceptance Criteria

Your solution must demonstrate all of the following:

* [ ]	A PDF and/or image can be submitted.
* [ ]	The document can be classified or routed according to a defined document type.
* [ ]	Required information can be extracted into structured data.
* [ ]	Missing information is identified.
* [ ]	Uncertain or conflicting information is identified.
* [ ]	A document can be assigned a workflow status.
* [ ]	A next action or route is produced.
* [ ]	The original document remains accessible.
* [ ]	The system can explain the important reason behind its decision.
* [ ]	At least one deliberately incomplete or ambiguous document is handled.
* [ ]	The complete flow can be demonstrated.

Submission Requirements

The repository must contain enough information for another developer to understand and run the solution.

At minimum, include:

README.md
ARCHITECTURE.md
DECISIONS.md
TESTING.md

ARCHITECTURE.md

Document:

* System components
* Document processing pipeline
* Data flow
* Storage
* Models and services used
* Important design decisions

Include an architecture diagram.

DECISIONS.md

Document important engineering decisions and trade-offs.

For example:

* Why this OCR approach?
* Why this extraction method?
* Why this schema?
* How is uncertainty handled?
* Why does the workflow route documents this way?

TESTING.md

Document:

* Normal document cases
* Missing-field cases
* Conflicting-field cases
* Invalid input cases
* Important edge cases
* Known limitations

Demo Expectations

The demonstration should show the complete path from document to decision.

A recommended flow is:

1. Introduce the scenario.
2. Submit a normal document.
3. Show extraction.
4. Show validation.
5. Show the resulting decision.
6. Submit an incomplete or ambiguous document.
7. Show how the system handles the uncertainty.
8. Show the workflow status.
9. Explain the architecture.
10. Defend the design.

The judges should be able to distinguish between a system that extracted information and a system that had enough information to decide what should happen next.

Event-Day Challenge

During evaluation, judges may introduce a document containing:

* A missing required field
* Conflicting information
* An unclear value
* An unexpected document variation

Your system should not require the judges to tell it what is wrong.

The demonstration should show how the system discovers the problem and determines whether it can continue or requires human review.

Rules

* Build your own solution.
* AI-assisted development is allowed.
* Public tools and libraries are allowed.
* Do not submit private credentials or confidential data.
* Do not rely on an ARC-owned backend or private dataset.
* Be prepared to explain your implementation.
* A feature the team cannot explain may be questioned during defense.
* Core requirements take priority over optional features.

Final Checklist

Before submission, verify the following:

* [ ]	Document upload works.
* [ ]	Document classification or routing works.
* [ ]	Required fields are extracted.
* [ ]	Structured output is produced.
* [ ]	Missing information is detected.
* [ ]	Uncertainty and conflicts are detected.
* [ ]	Workflow status is visible.
* [ ]	A next action is produced.
* [ ]	The original document remains accessible.
* [ ]	A human-review path exists where appropriate.
* [ ]	Normal and difficult cases have been tested.
* [ ]	No secrets are committed.
* [ ]	Architecture is documented.
* [ ]	Technical decisions are documented.
* [ ]	Testing is documented.
* [ ]	The demo is ready.

INNOVEX | ARC Club