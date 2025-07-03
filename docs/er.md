```mermaid
---
title: Entity Relation
---
erDiagram
    transactions ||--o{ transaction_allocations : links
    subcategories ||--o{ transactions : uses
    subcategories ||--|| categories : belongs_to
    currencies ||--o{ transactions : has
    movement_entries ||--|{ transaction_allocations : originates_from
    movement_entries ||--|| movement_foreign_origins : has
    currencies ||--o{ movement_foreign_origins : has
    transaction_sources ||--|{ movement_entries : source_of
    currencies ||--o{ transaction_sources : has

    transactions {
        uuid id
        string description
        decimal amount
        subcategories subcategory_id
        currencies currency_id
    }
    movement_entries {
        uuid id
        string name
        decimal amount
        transaction_sources transaction_source_id
        timestamptz occurred_at
    }
    movement_foreign_origins {
        uuid id
        movement_entries movement_entry_id
        decimal foreign_amount
        currencies foreign_currency_id
    }
    transaction_allocations {
        transactions transaction_id
        movement_entries movement_entry_id
    }
    categories {
        uuid id
        string name
    }
    subcategories {
        uuid id
        string name
        categories category_id
    }
    currencies {
        uuid id
        string code
        string name
    }
    transaction_sources {
        uuid id
        string entity
        string name
        string identifier
        currencies default_currency_id
        date valid_from
        date valid_to
    }
```
