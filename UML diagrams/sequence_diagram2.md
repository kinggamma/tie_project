sequenceDiagram
  participant Pub as Publisher
  participant QAU as QAU
  participant PO as Planning Officer
  participant API as Backend
  participant EVA1 as Evaluator #1
  participant EVA2 as Evaluator #2
  participant EVA3 as Evaluator #3
  participant RCE as Report Compilation Engine

  Pub->>API: Extended submission + anonymized/full manuscripts + fees receipt
  QAU->>API: Assign 3–7 evaluators
  PO->>API: Approve evaluators' budget

  par Evaluators work in parallel
    EVA1->>API: Upload form, report (docx+pdf), evaluated manuscript + score
    EVA2->>API: Upload form, report (docx+pdf), evaluated manuscript + score
    EVA3->>API: Upload form, report (docx+pdf), evaluated manuscript + score
  end

  API->>API: Calculate average score + verdict
  API->>RCE: Trigger compile after last upload
  RCE-->>API: Compiled report stored & linked to submission

  QAU->>API: Choose dispatch attachments (compiled only / compiled+individual / manual)
