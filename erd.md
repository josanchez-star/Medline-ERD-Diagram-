# Operations Problem Navigator — Entity Relationship Diagram

Data model derived from the Medline Cycle 60 RFP: incidents captured through a common intake, grouped by AI modeling into Problem records with impact, scope, ownership, and resolution tracking.


```mermaid 
erDiagram
INCIDENT }o--|| PROBLEM : "grouped into"
PROBLEM ||--o{ IMPACT : "has"
PROBLEM ||--|| SCOPE : "has"
PROBLEM }o--|| OWNER : "owned by"
PROBLEM ||--o| RESOLUTION : "tracked by"
RESOLUTION }o--|| IT_TEAM : "routed to"
INCIDENT }o--|| BRANCH_METADATA : "occured at"
INCIDENT }o--o| SLA : "measured against"
OWNER }o--|| PERSONA : "holds"

INCIDENT { 
    uuid id PK
    string type
    string source_system
    datetime occured_at
    string description
    uuid branch_id FK
    uuid sla_id FK
    uuid problem_id FK
}

PROBLEM {
    uuid id PK
    string category
    string description
    string predicted_future_impact
    string status
    uuid owner_id FK
}

IMPACT {
    uuid id Pk
    uuid problem_id FK
    string impact_type
    decimal quantified_value
}

SCOPE {
    uuid id PK
    uuid problem_id FK
    string application
    string branch_zone_equipment
    date start_date
}

OWNER {
    uuid id PK
    stirng name
    uuid persona_id FK
    string team
}

PERSONA {
    uuid id PK
    sting role_name
    string responsibility
}

RESOLUTION {
    uuid id PK
    uuid problem_id FK
    uuid it_team_id FK
    string status
    date resolved_at
}

IT_Team {
    uuid id PK
    string name
    string specialty 
}

BRANCH_METADATA {
    uuid id PK
    string branch_name
    string systems
    string process_type
}

SLA {
    uuid id PK
    string customer
    string metric
    decimal threshold
}
```
