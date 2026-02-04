# Brainwind Markdown Example

This document demonstrates how to use **Brainwind** syntax in Markdown for LLM-generated content.

---

## The Perfect Neapolitan Pizza

### Foundation & Ingredients

The authentic [Neapolitan Pizza]{.bw-node data-bw-type="Product" data-bw-id="pizza-margherita"} {.bw-edge data-bw-rel="originatesFrom"} [Naples, Italy]{.bw-node data-bw-type="Place" data-bw-id="naples"}.

The key ingredient is [San Marzano Tomatoes]{.bw-node data-bw-type="Product" data-bw-id="san-marzano"}, which are {.bw-edge data-bw-rel="grownIn"} the volcanic soil of [Mount Vesuvius]{.bw-node data-bw-type="Place" data-bw-id="mount-vesuvius"}.

### The Master's Technique

[Chef Antonio Rossi]{.bw-node data-bw-type="Person" data-bw-id="chef-rossi"} {.bw-edge data-bw-rel="uses"} a [72-hour cold fermentation]{.bw-node data-bw-type="Technique" data-bw-id="fermentation-72h"} technique. This process transforms the [gluten structure]{.bw-node data-bw-type="Chemical" data-bw-id="gluten"} into an [aerated, elastic matrix]{.bw-node data-bw-type="Concept" data-bw-id="texture-airy"}.

### Supply Chain

The base flour, [Tipo 00]{.bw-node data-bw-type="Product" data-bw-id="flour-tipo-00"}, is {.bw-edge data-bw-rel="producedBy"} [Molino Caputo]{.bw-node data-bw-type="Organization" data-bw-id="molino-caputo"} in [Capua]{.bw-node data-bw-type="Place" data-bw-id="capua"}.

The cheese, [Mozzarella di Bufala]{.bw-node data-bw-type="Product" data-bw-id="mozzarella-bufala"}, comes from water buffaloes raised in the [Campania region]{.bw-node data-bw-type="Place" data-bw-id="campania"}.

### Certification Standards

The [Associazione Verace Pizza Napoletana]{.bw-node data-bw-type="Organization" data-bw-id="avpn"} {.bw-edge data-bw-rel="certifies"} authentic pizzas. They require cooking in a [wood-fired oven]{.bw-node data-bw-type="Product" data-bw-id="wood-oven"} at [485°C (905°F)]{.bw-node data-bw-type="Concept" data-bw-id="temp-485c"} for [60-90 seconds]{.bw-node data-bw-type="Concept" data-bw-id="time-90sec"}.

### The Science of Flavor

Research by the [University of Naples Federico II]{.bw-node data-bw-type="Organization" data-bw-id="univ-naples"} shows that the [umami flavor]{.bw-node data-bw-type="Concept" data-bw-id="umami"} {.bw-edge data-bw-rel="resultsFrom"} [free glutamate]{.bw-node data-bw-type="Chemical" data-bw-id="glutamate"} in tomatoes synergizing with [5'-ribonucleotides]{.bw-node data-bw-type="Chemical" data-bw-id="ribonucleotides"} in [Parmigiano-Reggiano]{.bw-node data-bw-type="Product" data-bw-id="parmesan"}.

---

## Alternative Syntax: Link-as-Node (Standard Markdown)

For simpler LLM outputs or systems that don't support extended Markdown attributes:

The [Chef Rossi](node:chef-01 "Person") prepares the [San Marzano Tomatoes](node:tomato-99 "Product") using traditional [fermentation techniques](node:technique-01 "Technique").

The [Associazione Verace Pizza Napoletana](node:avpn "Organization") was founded in [1984](node:event-1984 "Event") in [Naples](node:naples "Place").

---

## Conversion to HTML

When this Markdown is processed by a Brainwind parser, it converts to:

```html
<p class="bw-context" data-bw-vocab="https://schema.org/">
  The authentic 
  <span class="bw-node" data-bw-type="Product" data-bw-id="pizza-margherita">
    Neapolitan Pizza
  </span>
  <span class="bw-edge" data-bw-rel="originatesFrom">originates from</span>
  <span class="bw-node" data-bw-type="Place" data-bw-id="naples">
    Naples, Italy
  </span>.
</p>
```

---

## RDF Triples Extracted

From this document, we can extract triples like:

```turtle
@prefix schema: <https://schema.org/> .
@prefix bw: <https://brainwind.io/> .

bw:pizza-margherita a schema:Product ;
    schema:name "Neapolitan Pizza" ;
    bw:originatesFrom bw:naples .

bw:naples a schema:Place ;
    schema:name "Naples, Italy" .

bw:san-marzano a schema:Product ;
    schema:name "San Marzano Tomatoes" ;
    bw:grownIn bw:mount-vesuvius .

bw:chef-rossi a schema:Person ;
    schema:name "Chef Antonio Rossi" ;
    bw:uses bw:fermentation-72h .

bw:fermentation-72h a bw:Technique ;
    schema:name "72-hour cold fermentation" .
```

---

## Usage Tips

### For Content Creators

1. Write naturally in Markdown
2. Wrap important entities in `[Entity]{.bw-node data-bw-id="id" data-bw-type="Type"}`
3. Use `{.bw-edge data-bw-rel="relationship"}` for relationship words
4. The text remains readable even without Brainwind processing

### For LLMs

When instructed to use Brainwind syntax, output:
- Clear, readable prose
- Entities wrapped in the extended Markdown syntax
- Unique IDs for each entity
- Appropriate types from Schema.org or custom ontologies

### For Developers

Parse Brainwind Markdown to:
- Generate knowledge graphs
- Create interactive documentation
- Enable semantic search
- Build linked data applications
- Train AI models on structured content

---

## Notes

- This syntax is compatible with many Markdown parsers that support attributes
- For parsers that don't support attributes, the link-as-node syntax provides a fallback
- The semantic meaning is preserved even if the Brainwind styling is not applied
- All relationships can be extracted programmatically for database storage or graph visualization
