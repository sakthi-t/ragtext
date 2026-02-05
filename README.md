# RAG Threads - Multi-tenant PDF Chat Application

A production-ready RAG (Retrieval Augmented Generation) web application where users can chat with PDFs, including image content understanding.

## Tech Stack

- **Backend**: Flask, Python
- **Database**: Neon/Railway Postgres (with SQLAlchemy)
- **Vector DB**: Chroma Cloud
- **Object Storage**: Backblaze B2 (S3-compatible)
- **LLM**: OpenAI GPT-4o (multimodal)
- **Embeddings**: 
  - Text: OpenAI text-embedding-3-large
  - Images: CLIP (openai/clip-vit-base-patch32) (not in scope yet)
- **Auth**: Email/Password + GitHub OAuth

## Features

- Multi-tenant architecture with user isolation
- Global documents visible to all users
- Private documents per user
- Admin-only documents
- Full PDF processing with text and image extraction
- RAG-powered chat with citations
- Activity logging
- Admin panel for user/document management

## Setup

### Prerequisites

- Python 3.10+
- PostgreSQL (Neon/Railway)
- Backblaze B2 account
- Chroma Cloud account
- OpenAI API key
- GitHub OAuth app (optional)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd raglocal
```

2. Create virtual environment and install dependencies:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3. Copy `.env.example` to `.env` and configure:
```bash
cp .env.example .env
# Edit .env with your credentials
```

4. Initialize the database:
```bash
flask db init
flask db migrate
flask db upgrade
```

5. Run the development server:
```bash
python app.py
```

The application will be available at `http://localhost:5000`

## Development

### Running with Gunicorn (Production)

```bash
gunicorn -c gunicorn.conf.py run:app
```

### Running Tests

```bash
pytest tests/
```

## Project Structure

```
raglocal/
├── app/                    # Application package
│   ├── models/            # Database models
│   ├── routes/            # API endpoints
│   ├── services/          # Business logic
│   ├── templates/         # Jinja2 templates
│   └── static/            # CSS, JS, images
├── migrations/            # Database migrations
├── workers/               # Background workers
├── tests/                 # Test suite
├── .env                   # Environment variables
├── requirements.txt       # Python dependencies
├── app.py                # Application entry point
└── gunicorn.conf.py      # Gunicorn configuration
```

## License

MIT

## Contributing

Contributions welcome! Please open an issue or PR.
