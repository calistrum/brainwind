# 🧠 Brainwind

**Stop styling pixels. Start styling synapses.**

Brainwind is a **semantic markup pattern** for creating Relational HTML. It provides a simple attribute convention that transforms flat prose into machine-readable knowledge graphs—no framework, no dependencies, just semantic HTML.

While **Tailwind** manages the _Eyes_ and **HTMX** manages the _Server_, **Brainwind** manages the _Mind_.

👉 **[See it in action: Interactive Demo](https://brainwind.pages.dev/)** - Pharmaceutical research example with 30+ entities and live queries

> **Note**: Brainwind is fundamentally a markup convention and RDF mapping pattern. The CSS file is **entirely optional**—use it only for development/debugging to visualize your semantic annotations.

---

## 🧐 The Problem

Most web content is "dead." To a computer, a recipe, a research paper, or a financial report is just a string of characters. Even "Semantic HTML" (`<article>`, `<section>`) only describes the **layout geometry**, not the **intellectual relationships** within the text.

Traditional RDF solutions (RDFa, Microdata) are verbose, break the flow of writing, and provide no immediate value to developers or users.

---

## ✨ Key Features

1. **🔗 RDF-Compatible**: Direct 1:1 mapping to Subject-Predicate-Object triples. Generate JSON-LD, Turtle, or N-Triples from your HTML.

2. **🎯 Element-Agnostic**: Works with any HTML element (`<span>`, `<div>`, `<a>`, etc.). Decorate, don't encapsulate.

3. **🤖 LLM-Friendly**: Built-in Markdown syntax perfect for AI-generated content. ChatGPT, Claude, and Gemini can output Brainwind natively.

4. **⚡ HTMX Ready**: Designed for reactive semantic interactions. Click an entity to fetch its knowledge graph data.

5. **🌐 Standards-Based**: Uses Schema.org, FOAF, and other standard vocabularies familiar to the RDF community.

---

## 💡 The Solution: Relational HTML

Brainwind provides a set of **attributes** and **utility classes** that map directly to **RDF (Resource Description Framework)** semantics. It treats the DOM as a **Synaptic Map**.

### The Core Principle: The Triple

The foundation of RDF is the **Subject-Predicate-Object** triple. In Brainwind:

- **Subject** (`.bw-node`): The entity the statement is about
- **Predicate** (`.bw-edge`): The property or relationship
- **Object** (`.bw-node`): The value or target entity

---

## 🚀 Quick Start

Brainwind is **element-agnostic**. You can apply it to `<span>`, `<div>`, `<td>`, or any tag that fits your layout.

**No installation required.** Just add the attributes to your HTML.

### Basic Example (No CSS Needed)

```html
<p class="bw-context" data-bw-vocab="https://schema.org/">
  The 
  <span class="bw-node" data-bw-type="Product" data-bw-id="san-marzano">
    San Marzano Tomatoes
  </span> 
  are
  <i class="bw-edge" data-bw-rel="grownIn">harvested from</i> 
  the volcanic soil of 
  <span class="bw-node" data-bw-type="Place" data-bw-id="mount-vesuvius">
    Mount Vesuvius
  </span>.
</p>
```

**What this creates:**
- **Subject**: San Marzano Tomatoes (Product)
- **Predicate**: grownIn
- **Object**: Mount Vesuvius (Place)

---

## 🛠 Utility Classes & Attributes

### Core Classes

| Class | Role | Description |
|-------|------|-------------|
| `.bw-context` | Container | Defines a semantic context/scope |
| `.bw-node` | Entity | Marks an element as a "Noun" in your ontology |
| `.bw-edge` | Relation | Marks the "Verb" or link between two nodes |

### Data Attributes

| Attribute | RDF Equivalent | Purpose |
|-----------|----------------|---------|
| `data-bw-vocab` | `@vocab` in JSON-LD | The base vocabulary/ontology URL |
| `data-bw-id` | `rdf:about` | Unique URI or identifier for the node |
| `data-bw-type` | `rdf:type` | The ontological class (Person, Place, Product, etc.) |
| `data-bw-rel` | `rdf:predicate` | The specific relationship type |

---

## 🧠 Brainwind + HTMX: The "Thinking" UI

Brainwind is designed to be the **data-source** for HTMX. Because the HTML is self-describing, your UI can "react" to the **meaning** of the text.

No special setup needed—just combine Brainwind attributes with HTMX directives:

```html
<span 
  class="bw-node bw-interactive" 
  data-bw-type="Concept"
  data-bw-id="umami"
  hx-get="/api/ontology/explain/umami"
  hx-trigger="click"
  hx-target="#definition-panel">
    Umami
</span>
```

When a user clicks "Umami," they aren't just clicking text—they're **interacting with a concept** defined in your knowledge graph.

---

## 📡 RDF Compatibility

Brainwind is **1:1 compatible with RDF**. A simple crawl of a Brainwind-enabled page can generate valid **JSON-LD**, **Turtle**, or **N-Triples**.

### Mapping to RDF

```html
<p class="bw-context" data-bw-vocab="https://schema.org/">
  <span class="bw-node" data-bw-type="Person" data-bw-id="chef-rossi">
    Chef Rossi
  </span>
  <span class="bw-edge" data-bw-rel="uses">employs</span>
  <span class="bw-node" data-bw-type="Technique" data-bw-id="high-heat">
    high-heat fermentation
  </span>.
</p>
```

**RDF Triple Output:**
```turtle
@prefix schema: <https://schema.org/> .

<chef-rossi> a schema:Person ;
    schema:uses <high-heat> .

<high-heat> a schema:Technique .
```

---

## 📝 Markdown Support (LLM-Friendly)

Most LLMs output Markdown. Brainwind provides a **Markdown syntax** that can be easily converted to Brainwind HTML.

### Brainwind Markdown Syntax

#### Option 1: Link-as-Node (Standard Markdown Compatible)

```markdown
The [Chef Rossi](node:chef-01 "Person") prepares the 
[San Marzano Tomatoes](node:tomato-99 "Product").
```

#### Option 2: Attribute Syntax (Extended Markdown)

```markdown
The [Chef Rossi]{.bw-node data-bw-type="Person" data-bw-id="chef-01"} 
uses {.bw-edge data-bw-rel="employsTechnique"} 
[high-heat fermentation]{.bw-node data-bw-type="Technique" data-bw-id="technique-01"}.
```

### LLM System Prompt

You can instruct LLMs to output Brainwind-ready content:

```
Output your response using Brainwind Markdown syntax. 
For entities (people, places, concepts), use: [Entity Name]{.bw-node data-bw-id="unique-id" data-bw-type="Type"}
For relationships, use: {.bw-edge data-bw-rel="relationshipType"}
```

See [`examples/system-prompt.md`](examples/system-prompt.md) for a complete prompt template.

---

##  Beyond the Spreadsheet: Real-World Examples

Brainwind turns any "wall of text" into a navigable map. Whether you're documenting a recipe, a supply chain, a medical study, or a legal contract, the relational HTML remains the same.

### Example: Culinary Knowledge

```html
<article class="bw-context" data-bw-vocab="https://schema.org/">
  <p>
    When 
    <span class="bw-node" data-bw-type="Person" data-bw-id="chef-rossi">
      Chef Rossi
    </span> 
    <i class="bw-edge" data-bw-rel="uses">applies</i> 
    <span class="bw-node" data-bw-type="Technique" data-bw-id="fermentation">
      high-heat fermentation
    </span>, 
    the 
    <span class="bw-node" data-bw-type="Chemical" data-bw-id="gluten">
      gluten structure
    </span> 
    becomes 
    <span class="bw-node" data-bw-type="State" data-bw-id="aerated">
      highly aerated
    </span>.
  </p>
</article>
```

### Example: Supply Chain Transparency

```html
<div class="bw-context" data-bw-vocab="https://schema.org/">
  The 
  <span class="bw-node" data-bw-type="Product" data-bw-id="lithium">Lithium</span> 
  is 
  <span class="bw-edge" data-bw-rel="sourcedFrom">extracted by</span> 
  <span class="bw-node" data-bw-type="Organization" data-bw-id="mining-corp">
    Global Mining Corp
  </span> 
  in 
  <span class="bw-node" data-bw-type="Place" data-bw-id="bolivia">Bolivia</span>.
</div>
```

See [`examples/`](examples/) for more demonstrations.

---

## 📜 Manifesto

1. **Prose is Data**: If it's worth writing, it's worth connecting.
2. **Decorate, Don't Encapsulate**: Don't break the web; enhance it with `data-*` attributes.
3. **Cognitive Lift**: A UI should help the user think, not just browse.
4. **Ontology is the New CSS**: Instead of managing "Blue-500," we manage "Entity-Relationship-Confidence."
5. **Logic is Invisible**: Your HTML should look like a document but act like a database.

---

## 🔧 Common Entity Types

Brainwind is ontology-agnostic, but here are common types used with Schema.org:

| Type | Description | Example |
|------|-------------|---------|
| `Person` | Individual human | Chef, Author, CEO |
| `Organization` | Company, Institution | Restaurant, Fund, NGO |
| `Place` | Geographic location | City, Country, Region |
| `Product` | Physical or digital good | Ingredient, Device |
| `Technique` | Method or process | Cooking method, Algorithm |
| `Concept` | Abstract idea | Democracy, Umami |
| `Event` | Occurrence in time | Conference, Launch |
| `Chemical` | Molecular compound | Gluten, CO₂ |

---

## 🚦 Getting Started

**No installation required.** Brainwind is a markup pattern, not a library.

1. **Add a context wrapper** to define your vocabulary:
   ```html
   <div class="bw-context" data-bw-vocab="https://schema.org/">
   ```

2. **Mark your entities** with `.bw-node`:
   ```html
   <span class="bw-node" data-bw-type="Person" data-bw-id="unique-id">
     Entity Name
   </span>
   ```

3. **Connect them** with `.bw-edge`:
   ```html
   <span class="bw-edge" data-bw-rel="relationshipType">
     connects to
   </span>
   ```

That's it! Your HTML is now a queryable knowledge graph.

**Want visual feedback?** Add your own styling:
```css
.bw-node { border-bottom: 1px dashed blue; cursor: help; }
.bw-edge { font-style: italic; color: gray; }
```

---

## 🤝 Contributing

Brainwind is an open framework. We welcome:

- **Vocabulary mappings** for specific domains (medical, legal, scientific)
- **Parser implementations** (JavaScript, Python, etc.)
- **Integration examples** with popular frameworks
- **Documentation improvements**

---

## 📚 Resources

- **RDF Primer**: [W3C RDF 1.1 Primer](https://www.w3.org/TR/rdf11-primer/)
- **Schema.org**: [schema.org](https://schema.org/)
- **JSON-LD**: [json-ld.org](https://json-ld.org/)
- **HTMX**: [htmx.org](https://htmx.org/)

---

## 📄 License

MIT License - See [LICENSE](LICENSE) for details.

---

## 🌟 Philosophy

> "The web was always meant to be a knowledge graph. Brainwind just makes it visible."

Brainwind transforms the document from a static artifact into a **living synapse**—a connection point in the vast neural network of human knowledge.

---

**Ready to style some synapses?** Check out the [examples](examples/) directory to see Brainwind in action.
