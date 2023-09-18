```mermaid
classDiagram
  class "送信リクエスト" as Request {
    +ID: string
    +送信日時: date
    +ステータス: string
    +ファイル: File
    +検証ルール: ValidationRule[]
  }
  
  class "ファイル" as File {
    +ファイル名: string
    +サイズ: int
    +形式: string
  }

  class "検証ルール" as ValidationRule {
    +ルール名: string
    +説明: string
    +条件: string
  }

  class "ユーザーアカウント" as UserAccount {
    +ユーザーID: string
    +名前: string
    +メールアドレス: string
  }

  class "送信リクエストリポジトリ" as RequestRepository {
    +保存(送信リクエスト): void
    +検索(ID: string): Request
  }

  class "ファイルリポジトリ" as FileRepository {
    +保存(ファイル): void
    +取得(ファイル名: string): File
  }

  class "検証ルールリポジトリ" as ValidationRuleRepository {
    +保存(検証ルール): void
    +取得(ルール名: string): ValidationRule
  }

  class "アプリケーションサービス" as ApplicationService {
    +送信リクエスト作成(): Request
    +ファイル検証開始(送信リクエスト): void
    +進捗監視(送信リクエスト): void
  }

  class "ファイル検証サービス" as ValidationService {
    +検証(ファイル, 検証ルール): bool
  }

  Request --* File : 包含
  Request --* ValidationRule : 包含
  File --|> FileRepository : 依存
  ValidationRule --|> ValidationRuleRepository : 依存
  RequestRepository --|> Request : 依存
  ApplicationService --> Request : 使用
  ValidationService --> File : 使用
  ValidationService --> ValidationRule : 使用
  ApplicationService --> RequestRepository : 使用
  ApplicationService --> FileRepository : 使用
  ApplicationService --> ValidationRuleRepository : 使用
```
