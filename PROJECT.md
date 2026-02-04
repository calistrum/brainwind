# 🧠 Brainwind Project

**Stop styling pixels. Start styling synapses.**

## Project Overview

Brainwind is a utility-first framework for creating semantically-rich HTML and Markdown that maps directly to RDF (Resource Description Framework). It bridges the gap between human-readable prose and machine-readable knowledge graphs.

## Repository Structure

```
brainwind/
├── README.md                    # Main documentation
├── QUICKSTART.md               # 5-minute getting started guide
├── CONTRIBUTING.md             # Contribution guidelines
├── LICENSE                     # MIT License
├── package.json                # npm package configuration
├── .gitignore                  # Git ignore rules
├── brainwind.css               # Core stylesheet
│
├── docs/
│   └── rdf-mapping.md         # RDF conversion guide
│
└── examples/
    ├── README.md              # Examples overview
    ├── pizza.html             # Complete HTML example
    ├── pizza.md               # Markdown example
    ├── htmx-integration.html  # HTMX interactive demo
    └── system-prompt.md       # LLM system prompt template
```

## Key Features

### 1. **Element-Agnostic Semantic Markup**
- Works with any HTML element (`<span>`, `<div>`, `<a>`, etc.)
- Decorate, don't encapsulate
- No custom elements required

### 2. **RDF-Compatible**
- Direct mapping to RDF triples (Subject-Predicate-Object)
- Compatible with Schema.org, FOAF, and custom ontologies
- Can be converted to JSON-LD, Turtle, N-Triples

### 3. **LLM-Friendly**
- Markdown syntax for AI-generated content
- System prompts for ChatGPT, Claude, Gemini
- Easy for LLMs to produce and parse

### 4. **Framework Integrations**
- HTMX for reactive semantic interactions
- Works with React, Vue, Svelte, plain HTML
- Compatible with existing CSS frameworks

### 5. **Visual Feedback**
- Subtle "ghost UI" styling
- Type-specific colors (optional)
- Dark mode support
- Accessible and keyboard-navigable

## Core Concepts

### The Triple Pattern

Every semantic statement consists of three parts:

```html
<span class="bw-node" data-bw-id="subject">Subject</span>
<span class="bw-edge" data-bw-rel="predicate">relationship</span>
<span class="bw-node" data-bw-id="object">Object</span>
```

### Utility Classes

- `.bw-context` - Semantic container
- `.bw-node` - Entity marker
- `.bw-edge` - Relationship marker
- `.bw-interactive` - HTMX-enabled nodes

### Data Attributes

- `data-bw-vocab` - Ontology/vocabulary URL
- `data-bw-id` - Unique entity identifier
- `data-bw-type` - Entity type (Person, Place, Product, etc.)
- `data-bw-rel` - Relationship type

## Use Cases

1. **Knowledge Management** - Turn documentation into queryable graphs
2. **Scientific Publishing** - Link research entities and citations
3. **Supply Chain** - Track product origins and relationships
4. **Education** - Create linked learning materials
5. **Journalism** - Annotate news with verifiable facts
6. **Legal** - Connect cases, statutes, and precedents

## Getting Started

### 1. Include the CSS

```html
<link rel="stylesheet" href="brainwind.css">
```

### 2. Mark Up Your Content

```html
<div class="bw-context" data-bw-vocab="https://schema.org/">
  <p>
    <span class="bw-node" data-bw-type="Person" data-bw-id="alice">Alice</span>
    <span class="bw-edge" data-bw-rel="worksAt">works at</span>
    <span class="bw-node" data-bw-type="Organization" data-bw-id="acme">ACME</span>
  </p>
</div>
```

### 3. Extract RDF Triples

```javascript
const nodes = document.querySelectorAll('.bw-node');
// Process into RDF format
```

See [QUICKSTART.md](QUICKSTART.md) for detailed instructions.

## Documentation

- **[README.md](README.md)** - Full framework documentation
- **[QUICKSTART.md](QUICKSTART.md)** - Get started in 5 minutes
- **[docs/rdf-mapping.md](docs/rdf-mapping.md)** - RDF conversion guide
- **[examples/](examples/)** - Working examples and demos

## Examples

### HTML Example
[examples/pizza.html](examples/pizza.html) - Interactive demo with JavaScript

### Markdown Example
[examples/pizza.md](examples/pizza.md) - LLM-friendly syntax

### HTMX Integration
[examples/htmx-integration.html](examples/htmx-integration.html) - Reactive semantic UI

### System Prompt
[examples/system-prompt.md](examples/system-prompt.md) - For ChatGPT/Claude/Gemini

## Technical Details

### Compatibility

- **Browsers**: All modern browsers (Chrome, Firefox, Safari, Edge)
- **Frameworks**: React, Vue, Svelte, plain HTML
- **RDF Tools**: Compatible with RDFLib, Apache Jena, Virtuoso
- **Markdown**: Pandoc, CommonMark with attributes extension

### Standards Compliance

- RDF 1.1
- Schema.org vocabularies
- JSON-LD 1.1
- SPARQL 1.1 (via conversion)

## Roadmap

### Version 0.2
- [ ] JavaScript parser library
- [ ] Python parser library
- [ ] npm package
- [ ] Browser extension for visualization

### Version 0.3
- [ ] Visual editor
- [ ] Graph visualization tools
- [ ] SPARQL query interface
- [ ] Wikidata/DBpedia linking

### Future
- [ ] AI-powered entity extraction
- [ ] Collaborative annotation tools
- [ ] Mobile app
- [ ] Integration with knowledge graph databases

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- How to contribute
- Code style guidelines
- Example submission process
- Community guidelines

## Philosophy

Brainwind is built on three core beliefs:

1. **Prose is Data** - Text isn't just for reading; it's for querying
2. **Decorate, Don't Encapsulate** - Enhance existing HTML, don't replace it
3. **Cognitive Lift** - Help users and machines think better together

## Community

- **Discussions**: [GitHub Discussions](#) (coming soon)
- **Issues**: [GitHub Issues](#)
- **Twitter**: [@brainwind](#) (coming soon)

## License

MIT License - see [LICENSE](LICENSE) for details.

## Credits

Inspired by:
- **Tailwind CSS** - Utility-first philosophy
- **HTMX** - HTML-driven interactivity
- **RDF/Semantic Web** - Knowledge representation
- **Schema.org** - Vocabulary standards

## Motto

> "The web was always meant to be a knowledge graph. Brainwind just makes it visible."

---

**Ready to transform your prose into a knowledge graph?**

Start with the [Quick Start Guide](QUICKSTART.md) or explore the [examples](examples/).

🧠 **Happy synapsing!**
