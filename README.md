erDiagram
    USER {
        int user_id PK
        string email
        string password_hash
        string full_name
        string address
    }

    CATEGORY {
        int category_id PK
        string name
        string description
    }

    PRODUCT {
        int product_id PK
        string name
        string description
        decimal price
        int stock_quantity
        int category_id FK
    }

    CART {
        int cart_id PK
        int user_id FK
    }

    CART_ITEM {
        int cart_item_id PK
        int cart_id FK
        int product_id FK
        int quantity
    }

    ORDER {
        int order_id PK
        int user_id FK
        datetime order_date
        string status
        decimal total_amount
        string shipping_address
    }

    ORDER_ITEM {
        int order_item_id PK
        int order_id FK
        int product_id FK
        int quantity
        decimal unit_price
    }

    PAYMENT {
        int payment_id PK
        int order_id FK
        datetime payment_date
        decimal amount
        string payment_method
        string status
    }

    USER ||--o{ CART : has
    USER ||--o{ ORDER : places
    CART ||--o{ CART_ITEM : contains
    CART_ITEM }o--|| PRODUCT : refers_to
    CATEGORY ||--o{ PRODUCT : belongs_to
    ORDER ||--o{ ORDER_ITEM : contains
    ORDER_ITEM }o--|| PRODUCT : includes
    ORDER ||--|| PAYMENT : has
