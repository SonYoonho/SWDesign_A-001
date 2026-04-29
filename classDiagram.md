'''mermaid
classDiagram
    class User {
        - id: String
        - pw: String
        - name: String
        - phone: String
        - address: String
        + registerUser(id: String, pw: String, name: String, phone: String, address: String) Boolean
        + updateUser(id: String, pw: String, name: String, phone: String, address: String) Boolean
        + deleteUser(id: String) Boolean
        + searchUser(id: String) User
    }

    class Account {
        - number: String
        - balance: long
        + deposit(id: String, amount: long) long
        + withdraw(id: String, amount: long) long
        + transfer(id: String, targetAccountNumber: String, amount: long) Boolean
        + computeBalance() long
    }

    class BankUI {
        <<boundary>>
        + displayMenu() void
        + inputTransactionData() void
    }

    %% 연관관계: User(1) <---> Account(1..*)
    User "1" -- "1..*" Account : manages >

    %% 의존관계: BankUI가 Account를 사용함
    BankUI ..> Account : <<User>>