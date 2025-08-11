
flowchart LR
  subgraph Actors
    A[Publisher/Author]
    Q[QAU Member]
    QE[QAU Editor]
    CS[Curriculum Specialist]
    EV[Evaluator]
    PO[Planning Officer/Manager]
    DG[Director General]
    REG[Registry]
    SA[System Admin]
  end

  subgraph System[Educational Material Submission & Evaluation System]
    UC1(Submit Materials & Required Docs)
    UC2(Confirm Submission & Assign Specialist)
    UC3(Upload Pre‑Evaluation Report & Files)
    UC4(Edit Report & Prepare Dispatch)
    UC5(Sign & Upload Dispatch Letter)
    UC6(Download Reports & Dispatch)

    UC7(Extended Submission for Evaluation)
    UC8(Assign Evaluators & Budget Workflow)
    UC9(Evaluator Uploads Reports & Manuscript)
    UC10(Calculate Average & Verdict)
    UC11(Compile Multi‑Evaluator Report)
    UC12(Attach Reports to Dispatch)

    UC13(Manage Users/Roles & Visibility)
    UC14(Notifications & Deadlines)
    UC15(Audit Trail & Versioning)
  end

  A -- uses --> UC1
  Q -- uses --> UC2
  CS -- uses --> UC3
  QE -- uses --> UC4
  DG -- uses --> UC5
  A -- uses --> UC6

  A -- uses --> UC7
  Q -- uses --> UC8
  PO -- uses --> UC8
  EV -- uses --> UC9

  UC9 --> UC10
  UC9 --> UC11
  Q -- uses --> UC12
  DG -- uses --> UC12

  SA -- uses --> UC13
  A & Q & CS & EV & DG & REG -- uses --> UC14
  SA & Q & DG -- uses --> UC15
