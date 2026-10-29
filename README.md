# Knowledge Graph Workshop

A hands-on workshop for exploring knowledge graphs and OWL ontologies. The project includes a retail-domain ontology, sample Turtle data, an AI assistant that queries that data with SPARQL, and a browser-based Turtle editor with a live graph preview.

## What's included

- **Ontology:** [`ontology/ontology.owl.ttl`](ontology/ontology.owl.ttl) defines a supermarket and retail vocabulary.
- **Sample knowledge graph:** [`data/mock_data.ttl`](data/mock_data.ttl) contains example records described using that vocabulary.
- **AI assistant:** Ask questions about the schema or sample records. For data questions, the assistant uses the ontology to compose SPARQL queries and runs them against the local sample graph.
- **Web interface:** Chat with the assistant and see the schema and the graph path used to answer a data question.
- **Turtle editor:** Open [`graph-view/live-editor.html`](graph-view/live-editor.html) in a browser to edit or open a `.ttl` file and see its graph update as you type. Filter schema and data, switch to a tree layout, and save your edits.
- **Practice ontology:** [`ontology/your_own_ontology.owl.ttl`](ontology/your_own_ontology.owl.ttl) is a starter file for creating an ontology of your own.

## Requirements

- Python 3.13 or later
- [uv](https://docs.astral.sh/uv/)
- An [OpenRouter](https://openrouter.ai/) API key to use the AI assistant

## Get started

Install the dependencies:

```bash
uv sync
```

Set your OpenRouter key in a `.env` file at the project root:

```env
OPENROUTER_API_KEY=your_key_here
```

Alternatively, export `OPENROUTER_API_KEY` in your shell. Keep your key private; `.env` is gitignored and should not be committed.

Optionally, choose a different OpenRouter model by setting `OPENROUTER_MODEL`. If unset, the assistant uses `anthropic/claude-5.5-sonnet`.

## Use the assistant

Start the web app:

```bash
uv run python -m src.server
```

Open <http://localhost:5000> in your browser. The app reads the ontology and sample data from the project directories and sends assistant requests to OpenRouter.

Ask a one-off question from the terminal:

```bash
uv run python -m src.ontology_agent "What classes exist for pricing?"
```

Or start a multi-turn terminal conversation:

```bash
uv run python -m src.ontology_agent
```

Use `Ctrl-D` to exit the interactive session.

## Explore and edit Turtle

Open `graph-view/live-editor.html` directly in a modern browser. It starts with an example ontology; use **Open .ttl** to load `ontology/ontology.owl.ttl` or another Turtle file. The graph updates as you edit, and **Save** downloads the current text. The editor loads CodeMirror from a CDN, so an internet connection is required.

## Project layout

```text
.
├── data/
│   └── mock_data.ttl            # Example retail records
├── graph-view/
│   ├── live-editor.html         # Browser-based Turtle editor and graph preview
│   └── vis-network.min.js       # Graph visualization library
├── ontology/
│   ├── ontology.owl.ttl         # Retail-domain ontology
│   └── your_own_ontology.owl.ttl # Blank practice ontology
├── src/
│   ├── ontology_agent.py        # Terminal assistant and SPARQL agent
│   ├── server.py                # Flask web app
│   └── ui/
│       └── index.html           # Assistant web interface
├── .env                         # Local OpenRouter key (not committed)
├── pyproject.toml
└── uv.lock
```
