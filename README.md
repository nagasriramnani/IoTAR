flowchart TB
  %% Client Layer
  subgraph Client["👤 Client (Web Browser)"]
    UI1[Login / Logout]
    UI2[Manage Customers]
    UI3[Create / View Quotations]
    UI4[Dashboard with AI Summary]
  end

  %% Web App Layer
  subgraph Flask["🌐 Flask Web Application (app.py)"]
    R1[Routes & Controllers]
    R2[RBAC Middleware\n(Session + Role Check)]
    R3[Jinja2 Templates + Bootstrap UI]
  end

  %% Database Layer
  subgraph DB["🗄 Data Layer (SQLite + SQLAlchemy ORM)"]
    D1[(Users & Roles)]
    D2[(Customers)]
    D3[(Products)]
    D4[(Quotations)]
    D5[(Quotation Items)]
  end

  %% AI Layer
  subgraph AI["🤖 AI/ML Layer"]
    PRED[Price Predictor\nscikit-learn Linear Regression\n(price_predictor.py)]
    SUMM[Summary Generator\nTransformers (t5-small)\n(summary_generator.py)]
  end

  %% External Services
  subgraph EXT["🌍 External (Optional)"]
    HF[(Hugging Face Hub)\nModel Download/Cache]
  end

  %% Relationships
  UI1 --> R1
  UI2 --> R1
  UI3 --> R1
  UI4 --> R1

  R1 --> R2
  R1 --> R3
  R1 <--> DB
  R1 --> PRED
  R1 --> SUMM

  PRED --> DB
  SUMM --> HF

  %% Styling
  classDef client fill:#E3F2FD,stroke:#1565C0,color:#000
  classDef flask fill:#EDE7F6,stroke:#4527A0,color:#000
  classDef db fill:#E8F5E9,stroke:#2E7D32,color:#000
  classDef ai fill:#FFF3E0,stroke:#EF6C00,color:#000
  classDef ext fill:#FCE4EC,stroke:#AD1457,color:#000

  class Client client
  class Flask flask
  class DB db
  class AI ai
  class EXT ext
