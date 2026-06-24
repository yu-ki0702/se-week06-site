graph LR
    %% アクターの定義
    subgraph アクター
        User((就活生))
    end

    %% アプリケーション境界とユースケース
    subgraph 就活特化予定管理アプリ
        UC1(アプリを起動する)
        UC2(1週間の予定を確認する)
        UC3(締切間近のリマインドを確認する)
        
        UC4(予定を登録・編集する)
        UC5(予定を削除・完了する)
        
        UC6(カレンダー表示を切り替える)
        
        %% 内部的なシステムユースケース
        UC_Save((ローカルにデータを保存する))
    end

    %% アクターとユースケースの接続
    User --> UC1
    User --> UC4
    User --> UC5
    User --> UC6

    %% 関係性（include / extend）の定義
    
    %% アプリ起動時に必ず1週間予定とリマインドが表示される (include)
    UC1 -.->|<< include >>| UC2
    UC1 -.->|<< include >>| UC3

    %% 登録・編集・削除時には必ずローカル保存が走る (include)
    UC4 -.->|<< include >>| UC_Save
    UC5 -.->|<< include >>| UC_Save

    %% 予定登録時に、条件（締切が近い）を満たした場合のみリマインドに反映される (extend)
    UC3 -.->|<< extend >>| UC4

    %% スタイル定義（見やすさのため）
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style UC_Save fill:#e1f5fe,stroke:#0288d1,stroke-width:1px,stroke-dasharray: 5 5
