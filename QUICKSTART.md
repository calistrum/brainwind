# Quick Start Guide

Get up and running with Brainwind in 5 minutes.

## What is Brainwind?

Brainwind is a **semantic markup pattern**, not a framework. It's a simple convention for adding meaning to your HTML using `data-*` attributes and class names.

Instead of just styling how text *looks*, you describe what it *means*. This creates machine-readable documents that can be:

- Queried like a database
- Converted to knowledge graphs
- Enhanced with AI
- Linked to external data sources

**No dependencies. No build step. Just semantic HTML.**

## Basic Usage

### 1. Wrap Your Content

Start with a context wrapper that defines your vocabulary:

```html
<div class="bw-context" data-bw-vocab="https://schema.org/">
  <!-- Your semantic content goes here -->
</div>
```

### 2. Mark Entities

Wrap important nouns with `.bw-node`:

```html
<span class="bw-node" data-bw-type="Person" data-bw-id="alice">Alice</span>
```

The attributes:
- `data-bw-type`: What kind of thing is this? (Person, Place, Product, etc.)
- `data-bw-id`: A unique identifier

### 3. Connect with Relationships

Mark the words that connect entities with `.bw-edge`:

```html
<span class="bw-edge" data-bw-rel="worksAt">works at</span>
```

### 4. Put It Together

```html
<div class="bw-context" data-bw-vocab="https://schema.org/">
  <p>
    <span class="bw-node" data-bw-type="Person" data-bw-id="alice">Alice</span>
    <span class="bw-edge" data-bw-rel="worksAt">works at</span>
    <span class="bw-node" data-bw-type="Organization" data-bw-id="acme">ACME Corp</span>
    in
    <span class="bw-node" data-bw-type="Place" data-bw-id="nyc">New York</span>.
  </p>
</div>
```

## Common Entity Types

Use these Schema.org types for `data-bw-type`:

| Type | Use For |
|------|---------|
| `Person` | People, individuals |
| `Organization` | Companies, groups, institutions |
| `Place` | Locations, cities, countries |
| `Product` | Items, goods, services |
| `Event` | Happenings, occurrences |
| `Concept` | Ideas, theories, abstractions |

[See full list in the README](README.md#common-entity-types)

## Common Relationships

Use these for `data-bw-rel`:

- `worksAt`, `employedBy`
- `locatedIn`, `basedIn`
- `createdBy`, `producedBy`
- `uses`, `contains`
- `memberOf`, `partOf`

## For LLM Users

Want ChatGPT to output Brainwind content?

1. Copy the [system prompt](examples/system-prompt.md)
2. Paste it into your conversation
3. Ask ChatGPT to write about anything
4. Get semantically-annotated content!

Example prompt:
```
Use Brainwind syntax to write about the invention of the telephone.
```

## Next Steps

### Learn More
- Read the [full README](README.md)
- Check out [examples](examples/)
- Understand [RDF mapping](docs/rdf-mapping.md)

### Try It Out
- Open [pizza.html](examples/pizza.html) in your browser
- Modify it with your own content
- See the semantic highlighting in action

### Build Something
- Add Brainwind to your blog
- Annotate documentation
- Create knowledge-rich content
- Integrate with HTMX for interactivity

## Troubleshooting

**Q: How do I add visual styling?**
- Brainwind doesn't include CSS
- Add your own styles to `.bw-node` and `.bw-edge` as needed:
  ```css
  .bw-node { border-bottom: 1px dashed blue; }
  .bw-edge { font-style: italic; color: gray; }
  ```

**Q: How do I make IDs unique?**
- Use descriptive kebab-case: `chef-alice-waters`
- Or use UUIDs for guaranteed uniqueness
- Stay consistent within a document

**Q: Can I use my own vocabulary?**
- Yes! Change `data-bw-vocab` to your ontology URL
- Document your custom types and relationships

**Q: Does this work with existing HTML?**
- Absolutely! Add Brainwind attributes to any HTML
- Works with React, Vue, plain HTML, etc.

## Get Help

- [Open an issue](https://github.com/yourusername/brainwind/issues)
- Read [contributing guidelines](CONTRIBUTING.md)
- Check [examples](examples/)

## Philosophy

> "Stop styling pixels. Start styling synapses."

Brainwind transforms documents from static pages into **living knowledge graphs**. Every highlighted term is a neuron, every relationship is a synapse, and your document becomes part of the web's collective intelligence.

Ready to make your content smarter? Start annotating! 🧠
