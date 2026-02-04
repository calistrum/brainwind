# Brainwind RDF Mapping Guide

This document explains how Brainwind HTML/Markdown maps to standard RDF (Resource Description Framework) formats.

## Core Mapping

### HTML to RDF Triples

Every Brainwind semantic statement maps to an RDF triple (Subject-Predicate-Object):

```html
<span class="bw-node" data-bw-id="chef-rossi" data-bw-type="Person">Chef Rossi</span>
<span class="bw-edge" data-bw-rel="uses">uses</span>
<span class="bw-node" data-bw-id="technique-01" data-bw-type="Technique">fermentation</span>
```

**Becomes:**

```turtle
@prefix bw: <https://brainwind.io/> .
@prefix schema: <https://schema.org/> .

bw:chef-rossi a schema:Person ;
    bw:uses bw:technique-01 .

bw:technique-01 a schema:Technique .
```

## Vocabulary Mapping

### Context/Vocabulary

```html
<div class="bw-context" data-bw-vocab="https://schema.org/">
```

**Maps to JSON-LD:**

```json
{
  "@context": "https://schema.org/",
  "@graph": [...]
}
```

**Maps to Turtle:**

```turtle
@prefix schema: <https://schema.org/> .
```

### Entity Types

| Brainwind | RDF/Schema.org |
|-----------|----------------|
| `data-bw-type="Person"` | `a schema:Person` |
| `data-bw-type="Organization"` | `a schema:Organization` |
| `data-bw-type="Place"` | `a schema:Place` |
| `data-bw-type="Product"` | `a schema:Product` |
| `data-bw-type="Event"` | `a schema:Event` |

### Relationships

| Brainwind | Schema.org Property |
|-----------|---------------------|
| `data-bw-rel="uses"` | `schema:uses` or custom |
| `data-bw-rel="locatedIn"` | `schema:location` |
| `data-bw-rel="producedBy"` | `schema:manufacturer` |
| `data-bw-rel="author"` | `schema:author` |

## Complete Example

### Brainwind HTML

```html
<article class="bw-context" data-bw-vocab="https://schema.org/">
  <p>
    <span class="bw-node" data-bw-type="Product" data-bw-id="pizza">Pizza</span>
    <span class="bw-edge" data-bw-rel="originatesFrom">originated in</span>
    <span class="bw-node" data-bw-type="Place" data-bw-id="naples">Naples</span>.
  </p>
</article>
```

### JSON-LD Output

```json
{
  "@context": "https://schema.org/",
  "@graph": [
    {
      "@id": "pizza",
      "@type": "Product",
      "name": "Pizza",
      "originatesFrom": {
        "@id": "naples"
      }
    },
    {
      "@id": "naples",
      "@type": "Place",
      "name": "Naples"
    }
  ]
}
```

### Turtle Output

```turtle
@prefix schema: <https://schema.org/> .
@prefix bw: <https://brainwind.io/> .

bw:pizza a schema:Product ;
    schema:name "Pizza" ;
    bw:originatesFrom bw:naples .

bw:naples a schema:Place ;
    schema:name "Naples" .
```

### N-Triples Output

```
<https://brainwind.io/pizza> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <https://schema.org/Product> .
<https://brainwind.io/pizza> <https://schema.org/name> "Pizza" .
<https://brainwind.io/pizza> <https://brainwind.io/originatesFrom> <https://brainwind.io/naples> .
<https://brainwind.io/naples> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <https://schema.org/Place> .
<https://brainwind.io/naples> <https://schema.org/name> "Naples" .
```

## Advanced Features

### Multiple Relationships

```html
<span class="bw-node" data-bw-id="chef">Chef</span>
<span class="bw-edge" data-bw-rel="worksAt">works at</span>
<span class="bw-node" data-bw-id="restaurant">Restaurant</span>
and
<span class="bw-edge" data-bw-rel="teaches">teaches at</span>
<span class="bw-node" data-bw-id="school">Culinary School</span>
```

**Produces two triples:**

```turtle
bw:chef bw:worksAt bw:restaurant .
bw:chef bw:teaches bw:school .
```

### Nested Contexts

```html
<div class="bw-context" data-bw-vocab="https://schema.org/">
  <div class="bw-context" data-bw-vocab="https://example.com/custom/">
    <!-- Custom vocabulary for nested content -->
  </div>
</div>
```

### Literal Values

Text without `data-bw-id` is treated as a literal:

```html
<span class="bw-node" data-bw-id="product">Product</span>
costs
<span class="bw-node" data-bw-type="PriceSpecification">$10</span>
```

```turtle
bw:product schema:price "10"^^schema:Number .
```

## Using with SPARQL

Once converted to RDF, you can query Brainwind data:

```sparql
PREFIX bw: <https://brainwind.io/>
PREFIX schema: <https://schema.org/>

SELECT ?person ?technique
WHERE {
  ?person a schema:Person .
  ?person bw:uses ?technique .
  ?technique a schema:Technique .
}
```

## Compatibility

Brainwind is compatible with:

- **RDFa**: Similar attribute-based approach
- **Microdata**: Schema.org integration
- **JSON-LD**: Direct conversion possible
- **Turtle/N-Triples**: Standard RDF serializations
- **OWL**: Can be extended with ontology definitions

## Tools for Conversion

### JavaScript Example

```javascript
function extractBrainwindTriples(element) {
  const triples = [];
  const nodes = element.querySelectorAll('.bw-node');
  const vocab = element.getAttribute('data-bw-vocab') || 'https://brainwind.io/';
  
  nodes.forEach(node => {
    const subject = node.getAttribute('data-bw-id');
    const type = node.getAttribute('data-bw-type');
    
    if (subject && type) {
      triples.push({
        subject: `${vocab}${subject}`,
        predicate: 'http://www.w3.org/1999/02/22-rdf-syntax-ns#type',
        object: `${vocab}${type}`
      });
    }
  });
  
  return triples;
}
```

### Python Example

```python
from rdflib import Graph, Namespace, Literal, URIRef
from rdflib.namespace import RDF, RDFS

def brainwind_to_rdf(html_content):
    g = Graph()
    bw = Namespace("https://brainwind.io/")
    schema = Namespace("https://schema.org/")
    
    # Parse HTML and extract nodes
    # ... (use BeautifulSoup or similar)
    
    # Add triples
    g.add((bw.chef_rossi, RDF.type, schema.Person))
    g.add((bw.chef_rossi, bw.uses, bw.technique_01))
    
    return g.serialize(format='turtle')
```

## Best Practices

1. **Use URIs**: Make `data-bw-id` globally unique (e.g., use UUIDs or URLs)
2. **Reuse Vocabularies**: Stick to Schema.org when possible
3. **Document Custom Relations**: If using custom `data-bw-rel`, document them
4. **Validate**: Use RDF validators to check output
5. **Link External**: Reference Wikidata, DBpedia when applicable

## Further Reading

- [RDF 1.1 Primer](https://www.w3.org/TR/rdf11-primer/)
- [Schema.org Documentation](https://schema.org/docs/documents.html)
- [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/)
- [SPARQL 1.1 Query Language](https://www.w3.org/TR/sparql11-query/)
