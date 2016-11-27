# JSON-LD in Python

There are two major Python libraries with different strengths and limitations.

## rdflib

[`rdflib`](http://rdflib.readthedocs.io/en/stable/apidocs/) is the go-to library for working with RDF in Python. It supports parsing and serializing RDF in many formats (including JSON-LD via the `rdflib-jsonld` extension), supports in memory generation and manipulation of RDF graphs, and has connectors for SPARQL etc.. However, even with the `rdflib-jsonld` extension, support for JSON-LD is limited, and the functions of a JSON-LD processor are no implemented.

## PyLD

[PyLD](https://github.com/digitalbazaar/pyld) is described as an _"implementation of the JSON-LD specification in Python"_. It uses native JSON-LD data stuctures and implements the functions of a JSON-LD processor (compaction, expansion, framing, etc.). However, it has no facilities for working with data as RDF triples, or taking data from RDF sources except by reparsing a JSON-LD serialization.

## Using `rdflib` and `PyLD` together?

Because `rdflib` and `PyLD` use different in-memory data structures it is not trivial to use the powerful RDF support of rdflib in conjuction with the JSON-LD processor implementation of PyLD. A small compatibility library [`rdflib_pyld_compat.py`](../rdflib_pyld_compat.py) provides a bridge from rdflib to PyLD formats without the need to serialize and then re-parse the data.

**Warning:** `rdflib_pyld_compat.py` was written while preparing this demonstration as has not been thoroughly exercised or tested.

A simple example program `<select_anno.py>` illustrates operations that one might want to do in both libraries: first building and manipulating an RDF graph with `rdflib`, then processing and tweaking the JSON with `PyLD`. The program take one command line argument which is the URI of the the annotation target used to select annotations. Running:

``` shell
jsonld-in-python> python select_anno.py http://example.org/hand2
```

produces:

``` json
{
  "@context": "http://example.org/context",
  "id": "http://example.org/anno1",
  "motivation": "http://example.org/Drawing",
  "on": "http://example.org/hand2",
  "resource": "http://example.org/hand1",
  "type": "oa:Annotation"
}
```

---

_| [Index](../README.md) | [Next: IIIF and Linked Data](../iiif_ld/README.md) |_