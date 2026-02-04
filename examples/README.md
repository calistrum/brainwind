# Brainwind Examples

This directory contains examples demonstrating Brainwind's capabilities across different domains and formats.

## 📁 Files

### [pizza.html](pizza.html)
A complete HTML example showing semantic markup for a culinary article about Neapolitan pizza. Demonstrates:
- Entity markup (Person, Place, Product, Technique, Chemical, Concept)
- Relationship edges
- HTMX integration points
- Visual styling with brainwind.css
- JavaScript for extracting triples

**Open in browser** to see the interactive demo.

### [pizza.md](pizza.md)
The same content in Brainwind Markdown format. Shows:
- Extended Markdown syntax with attributes
- Link-as-node alternative syntax
- RDF triple extraction examples
- Conversion to HTML

**Use with LLMs** or Markdown parsers that support attributes.

### [system-prompt.md](system-prompt.md)
A comprehensive system prompt for instructing LLMs (ChatGPT, Claude, Gemini) to output Brainwind-formatted content. Includes:
- Complete syntax rules
- Entity types and relationships
- Example outputs
- Domain-specific ontologies
- Validation checklist

**Copy-paste** into your LLM conversations.

## 🚀 Quick Start

### View the HTML Example

1. Open `pizza.html` in your browser
2. Hover over highlighted terms to see the "synapse" effect
3. Click interactive elements to see entity information
4. Open browser console to see extracted triples

### Use the Markdown Example

1. Copy content from `pizza.md`
2. Use with a Markdown parser that supports attributes
3. Or parse it programmatically to extract semantic data

### Try with an LLM

1. Copy the system prompt from `system-prompt.md`
2. Paste into ChatGPT/Claude as a system instruction
3. Ask it to write about any topic
4. Get back semantically-annotated content

## 📚 More Examples Coming Soon

We're working on examples for:
- Supply chain documentation
- Scientific research papers
- Legal contracts
- Medical records
- News articles
- Educational content

## 🤝 Contributing Examples

Have a great use case? Submit a PR with:
1. Your example file(s)
2. A brief description
3. Any domain-specific vocabulary used
4. RDF triple examples

See [CONTRIBUTING.md](../CONTRIBUTING.md) for details.
