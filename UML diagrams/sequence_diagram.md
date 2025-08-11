%%Submission → Pre‑Evaluation → Dispatch
sequenceDiagram
  participant Pub as Publisher
  participant Web as Web App (UI)
  participant API as Backend API
  participant QAU as QAU Member
  participant CS as Curriculum Specialist
  participant QE as QAU Editor
  participant DG as Director General
  participant Store as File Storage

  Pub->>Web: Fill Part A & E + Upload required files
  Web->>API: POST /submissions + files
  API->>Store: Save manuscripts & letters (versioned)
  API-->>Web: 201 Created + Submission ID

  QAU->>Web: Review checklist & confirm
  Web->>API: PATCH /submissions/{id}/confirm + assign CS

  CS->>Web: Download manuscript
  CS->>Web: Upload signed pre‑evaluation report + pre‑evaluated ms
  Web->>API: POST /pre‑evaluation
  API->>Store: Save signed report & files

  QE->>Web: Edit report & prepare dispatch
  Web->>API: POST /dispatch/draft

  DG->>Web: Review & sign dispatch letter
  Web->>API: POST /dispatch/sign
  API->>Store: Save signed dispatch (PDF)

  Pub->>Web: Download pre‑evaluation report + dispatch letter
