# NDS.Live Filling Specification — exchange format schema

The normative JSON Schema (draft 2020-12) for **NDS.Live filling
specification** documents. A filling spec is the contract between a
map-data producer and a customer, expressed in NDS.Live schema
vocabulary — a producer's *catalog* of everything it can deliver, or a
*product* derived from it for one customer; this repository publishes the
machine-readable contract that every exported document's `$schema`
points to, so any JSON Schema validator can check a filling spec
without further tooling.

## Published versions

| Format version | Schema | Notes |
|---|---|---|
| **0.3** (current) | [`filling-spec-0.3.schema.json`](https://ndsev.github.io/ndslive-fspec-schema/filling-spec-0.3.schema.json) | One specification per document (`productSpecification` at the top level) plus an optional `derivedFrom` link from a product to its catalog. |
| 0.2 | [`filling-spec-0.2.schema.json`](https://ndsev.github.io/ndslive-fspec-schema/filling-spec-0.2.schema.json) | Two-part document (`specs.capability` / `specs.requirement`). Superseded; the fspec tooling migrates 0.2 files, splitting a two-part file into a catalog and a product. |

Served via GitHub Pages under
`https://ndsev.github.io/ndslive-fspec-schema/`.

## Stability

- **Published versions are immutable.** Once a
  `filling-spec-<version>.schema.json` is published here, its content
  never changes; a new format version gets a new file, and older files
  stay retrievable indefinitely.
- Exported documents reference the schema by absolute URL in `$schema`.
  Those references live as long as the documents do, which is why this
  repository exists separately from any tool: the URLs must outlive
  releases.
- Within a format version the schema evolves additively before first
  publication only; see the format's requirements documentation in the
  fspec tooling for the versioning policy.

## Validating a document

Any draft 2020-12 validator works, e.g.:

```bash
npx ajv-cli validate --spec=draft2020 \
  -s filling-spec-0.3.schema.json -d my-filling-spec.json
```

Note that the schema covers document *structure*. The fspec tooling
additionally validates NDS.Live semantics (layer types, attribute
names, condition codes against the NDS.Live model) and cross-reference
consistency, which no standalone JSON Schema can express.

## License

[BSD 3-Clause](LICENSE), © Navigation Data Standard e.V.
