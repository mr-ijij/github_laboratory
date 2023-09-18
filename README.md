```mermaid
classDiagram
  class "送信リクエスト (Request)" as RequestClass {
    +ID: string // 送信リクエストID
    +送信日時 (SentDate): date
    +ステータス (Status): string
    +ファイル (File): File
    +検証ルール (ValidationRules): ValidationRule[]
  }
  
  class "ファイル (File)" as FileClass {
    +ファイル名 (FileName): string
    +サイズ (Size): int
    +形式 (Format): string
  }

  class "検証ルール (ValidationRule)" as ValidationRuleClass {
    +ルール名 (RuleName): string
    +説明 (Description): string
    +条件 (Condition): string
  }

  class "ユーザーアカウント (UserAccount)" as UserAccountClass {
    +ユーザーID (UserID): string
    +名前 (Name): string
    +メールアドレス (EmailAddress): string
  }

  class "送信リクエストリポジトリ (RequestRepository)" as RequestRepositoryClass {
    +保存 (Save)(request: Request): void
    +検索 (Find)(ID: string): Request
  }

  class "ファイルリポジトリ (FileRepository)" as FileRepositoryClass {
    +保存 (Save)(file: File): void
    +取得 (Get)(ファイル名: string): File
  }

  class "検証ルールリポジトリ (ValidationRuleRepository)" as ValidationRuleRepositoryClass {
    +保存 (Save)(rule: ValidationRule): void
    +取得 (Get)(ルール名: string): ValidationRule
  }

  class "アプリケーションサービス (ApplicationService)" as ApplicationServiceClass {
    +送信リクエスト作成 (CreateRequest)(): Request
    +ファイル検証開始 (StartValidation)(request: Request): void
    +進捗監視 (MonitorProgress)(request: Request): void
  }

  class "ファイル検証サービス (ValidationService)" as ValidationServiceClass {
    +検証 (Validate)(file: File, rule: ValidationRule): bool
  }
```

