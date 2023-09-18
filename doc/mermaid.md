```mermaid
classDiagram
  class "Request" as RequestClass {
    +ID: string // 送信リクエストID
    +SentDate: date // 送信日時
    +Status: string // ステータス
    +File: File // ファイル
    +ValidationRules: ValidationRule[] // 検証ルール
  }
  
  class "File" as FileClass {
    +FileName: string // ファイル名
    +Size: int // サイズ
    +Format: string // 形式
  }

  class "ValidationRule" as ValidationRuleClass {
    +RuleName: string // ルール名
    +Description: string // 説明
    +Condition: string // 条件
  }

  class "UserAccount" as UserAccountClass {
    +UserID: string // ユーザーID
    +Name: string // 名前
    +EmailAddress: string // メールアドレス
  }

  class "RequestRepository" as RequestRepositoryClass {
    +Save(request: Request): void // 保存
    +Find(ID: string): Request // 検索
  }

  class "FileRepository" as FileRepositoryClass {
    +Save(file: File): void // 保存
    +Get(FileName: string): File // 取得
  }

  class "ValidationRuleRepository" as ValidationRuleRepositoryClass {
    +Save(rule: ValidationRule): void // 保存
    +Get(RuleName: string): ValidationRule // 取得
  }

  class "ApplicationService" as ApplicationServiceClass {
    +CreateRequest(): Request // 送信リクエスト作成
    +StartValidation(request: Request): void // ファイル検証開始
    +MonitorProgress(request: Request): void // 進捗監視
  }

  class "ValidationService" as ValidationServiceClass {
    +Validate(file: File, rule: ValidationRule): bool // 検証
  }

  RequestClass --* FileClass : 包含
  RequestClass --* ValidationRuleClass : 包含
  FileClass --|> FileRepositoryClass : 依存
  ValidationRuleClass --|> ValidationRuleRepositoryClass : 依存
  RequestRepositoryClass --|> RequestClass : 依存
  ApplicationServiceClass --> RequestClass : 使用
  ValidationServiceClass --> FileClass : 使用
  ValidationServiceClass --> ValidationRuleClass : 使用
  ApplicationServiceClass --> RequestRepositoryClass : 使用
  ApplicationServiceClass --> FileRepositoryClass : 使用
  ApplicationServiceClass --> ValidationRuleRepositoryClass : 使用

```
