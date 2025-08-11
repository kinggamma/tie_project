classDiagram
  class User {
    +uuid id
    +string name
    +string email
    +Role[] roles
    +bool isActive
  }
  class Role {
    +string code  // PUBLISHER, QAU, CS, EVALUATOR, DG, PO, REG, ADMIN
    +Permission[] permissions
  }
  class Submission {
    +uuid id
    +string title
    +Level level
    +string subjectOrCompetency
    +string classLevel
    +MaterialType type
    +string isbn
    +int pages
    +Status status
    +datetime createdAt
    +datetime updatedAt
  }
  class FileAsset {
    +uuid id
    +FileType fileType // manuscript_full, manuscript_anon, submission_letter, editing_cert, licence, tin, preeval_report_signed, eval_form, eval_report_pdf, eval_report_docx, evaluated_ms, compiled_report, dispatch_letter
    +string path
    +int version
    +datetime uploadedAt
    +User uploadedBy
    +Visibility visibility // role‑based tags
  }
  class PreEvaluation {
    +uuid id
    +datetime receivedAt
    +datetime completedAt
    +string remarks
  }
  class EvaluationAssignment {
    +uuid id
    +int sequence // evaluator 1..n
    +datetime assignedAt
    +datetime dueAt
    +EvaluationStatus status
  }
  class Evaluation {
    +uuid id
    +float scorePercent
    +datetime submittedAt
  }
  class ReportCompilation {
    +uuid id
    +datetime compiledAt
    +string method // auto, manual
  }
  class BudgetApproval {
    +uuid id
    +Money amount
    +datetime approvedAt
    +User approvedBy
  }
  class Dispatch {
    +uuid id
    +datetime signedAt
    +DispatchAttachmentMode mode // compiled_only | compiled+individual | manual
  }
  class Notification {
    +uuid id
    +string channel // email, sms
    +string template
    +datetime sentAt
  }
  class AuditLog {
    +uuid id
    +string action
    +User actor
    +datetime at
    +string target
  }

  User "1" -- "*" Submission : createdBy
  Submission "1" -- "*" FileAsset : contains
  Submission "1" -- "0..1" PreEvaluation : preEval
  Submission "1" -- "*" EvaluationAssignment : has
  EvaluationAssignment "1" -- "1" User : evaluator
  EvaluationAssignment "1" -- "0..1" Evaluation : result
  Evaluation "1" -- "*" FileAsset : uploads
  Submission "0..1" -- "1" ReportCompilation : compiledReport
  Submission "0..1" -- "1" BudgetApproval : budget
  Submission "0..1" -- "1" Dispatch : dispatch
  Submission "*" -- "*" Notification : notifies
  Submission "*" -- "*" AuditLog : logs

  enum Status { Draft Submitted PreEvaluating PreEvaluated Evaluating Evaluated Dispatched Closed }
  enum MaterialType { Supplementary Reference Storybook Literary ETLC Video Audio Module }
  enum Level { PrePrimary Primary OLevel ALevel DTE }
  enum EvaluationStatus { Assigned InReview Submitted }
  enum FileType { manuscript_full manuscript_anon submission_letter editing_cert licence tin preeval_report_signed eval_form eval_report_pdf eval_report_docx evaluated_ms compiled_report dispatch_letter }
  enum DispatchAttachmentMode { compiled_only compiled_and_individual manual }
  enum Visibility { publisher qau cs evaluator dg registry admin }
