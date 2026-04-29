```mermaid

graph LR
    User((사용자))
    BankSystem[[은행 외부 시스템]]

    subgraph Online_Banking_System [온라인 뱅킹 시스템]
        %% 사용자 관리 영역
        UC4(사용자 조회)
        UC1(사용자 등록) -.&lt;&lt;include&gt;&gt;.-> UC4
        UC2(사용자 정보 수정) -.&lt;&lt;include&gt;&gt;.-> UC4
        UC3(사용자 삭제) -.&lt;&lt;include&gt;&gt;.-> UC4
        
        %% 뱅킹 거래 영역
        UC8(잔액 조회)
        UC5(입금)
        UC6(출금)
        UC7(이체)

        %% 거래 시 조회 및 잔액조회 포함 관계
        UC5 -.&lt;&lt;include&gt;&gt;.-> UC4
        UC5 -.&lt;&lt;include&gt;&gt;.-> UC8
        UC6 -.&lt;&lt;include&gt;&gt;.-> UC4
        UC6 -.&lt;&lt;include&gt;&gt;.-> UC8
        UC7 -.&lt;&lt;include&gt;&gt;.-> UC4
        UC7 -.&lt;&lt;include&gt;&gt;.-> UC8
    end

    %% 액터 연결
    User --- UC1
    User --- UC2
    User --- UC3
    User --- UC5
    User --- UC6
    User --- UC7
    User --- UC8

    %% 외부 시스템 연결 (거래 발생 시 은행 시스템과 연동)
    UC5 --- BankSystem
    UC6 --- BankSystem
    UC7 --- BankSystem
    UC8 --- BankSystem

    %% 스타일링
    style Online_Banking_System fill:#f9f9f9,stroke:#333,stroke-width:2px
    style BankSystem fill:#e1f5fe,stroke:#01579b