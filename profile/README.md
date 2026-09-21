# AnimaLogica

### Data, reasoning, and reliable execution for the BEAM.

Elixir and Erlang are exceptional at concurrency, distribution, fault tolerance, and long-running systems. But modern applications increasingly depend on capabilities that have traditionally lived outside the BEAM: columnar data, scientific arrays, graph computation, probabilistic algorithms, logic programming, structured AI, and high-performance native code.

**AnimaLogica is building those missing pieces.**

The goal is not to turn Elixir into Python, Rust, or C++. It is to help make the BEAM a first-class participant in modern data and intelligent systems while preserving the qualities that make it distinctive.

Where computation belongs on the BEAM, we implement it there. Where native performance matters, we use Rust, Zig, SuiteSparse, or other established systems behind idiomatic Elixir APIs. Where data is too large to materialize, we stream it. And where systems need to survive failure, we build around OTP rather than around it.

The projects are independent libraries, but they increasingly form a stack.

## Data infrastructure

Modern systems need to move large amounts of structured data without turning everything into lists of Elixir terms.

### [ExArrow](https://github.com/AnimaLogica/ex_arrow)

Native Apache Arrow for the BEAM.

ExArrow brings Arrow IPC, Parquet, Arrow Flight, Flight SQL, ADBC, datasets, scanners, and Arrow-native streaming pipelines to Elixir. Columnar data remains in native buffers while the BEAM works with lightweight handles.

It is intended to make Elixir a serious participant in the wider Arrow ecosystem rather than requiring Python or JVM processes at the boundary.

### [ExZarr](https://github.com/AnimaLogica/ExZarr)

Chunked N-dimensional arrays for Elixir.

ExZarr implements Zarr v2 and v3 for scientific, analytical, and larger-than-memory workloads, with parallel chunk processing, streaming APIs, pluggable storage, compression, and interoperability with the Python Zarr ecosystem.

Where Arrow is the columnar interchange layer, Zarr provides the chunked N-dimensional storage layer.

### [ExCodecs](https://github.com/AnimaLogica/codecs)

A codec framework for the BEAM.

ExCodecs provides a common architecture for high-performance codecs, including compression and spatial formats, with native acceleration hidden behind an Elixir API.

It exists because compression, serialization, spatial data, and other binary transformations are infrastructure, not application-specific details.

## Computation

Moving data efficiently is only useful if we can compute over it efficiently.

### [ExDataSketch](https://github.com/AnimaLogica/ex_data_sketch)

Streaming probabilistic algorithms for Elixir.

ExDataSketch implements HyperLogLog, Count-Min Sketch, KLL, Theta, DDSketch, Bloom and Cuckoo filters, IBLTs, UltraLogLog, heavy-hitter algorithms, and other sketches for answering useful questions without retaining all of the underlying data.

It combines pure Elixir reference implementations with optional native acceleration and integrates with Streams, Flow, GenStage, Broadway, telemetry, and multiple persistence backends.

### [ExGraphBLAS](https://github.com/AnimaLogica/ex_graphblas)

Sparse linear algebra and graph computation on the BEAM.

ExGraphBLAS exposes GraphBLAS-style matrices, vectors, semirings, graph algorithms, and knowledge-graph operations through idiomatic Elixir, with a pure Elixir backend and native SuiteSparse:GraphBLAS acceleration.

Graphs become algebra. Traversal, reachability, shortest paths, PageRank, connected components, and relationship queries become operations over sparse matrices.

### [ExSystolic](https://github.com/AnimaLogica/ex_systolic)

A systolic-array computation model for Elixir.

ExSystolic explores computation as networks of small processing elements communicating locally in deterministic ticks. It provides a foundation for experimenting with dataflow, parallel matrix algorithms, semirings, hardware-style computation, and alternative execution backends.

It asks a broader question: what computational models become practical when we combine the BEAM's concurrency model with ideas normally associated with specialized hardware?

## Knowledge and reasoning

Data becomes more valuable when relationships, rules, provenance, and constraints can be expressed directly.

### [ExDatalog](https://github.com/AnimaLogica/ex_datalog)

A production-oriented Datalog engine for Elixir.

ExDatalog provides recursive rules, stratified negation, aggregates, constraints, provenance, query planning, semi-naive evaluation, magic sets, and pluggable storage.

Datalog gives applications a compact declarative language for graph traversal, authorization, dependency analysis, derived knowledge, temporal reasoning, and explainable rule systems.

It is also a natural bridge between deterministic reasoning and probabilistic AI.

### [TerminusDB Client for Elixir](https://github.com/AnimaLogica/terminusdb-client-elixir)

An idiomatic Elixir client for the versioned document graph database TerminusDB.

The client supports document operations, schemas, branches, commits, diffs, merges, GraphQL, WOQL, streaming, telemetry, and immutable connection contexts.

Together with ExDatalog and ExGraphBLAS, it forms part of a broader exploration of graphs not simply as storage, but as executable knowledge.

### [ExOutlines](https://github.com/AnimaLogica/ex_outlines)

Structured LLM output for Elixir.

ExOutlines turns probabilistic model responses into validated application data through schemas, constraints, validation, and automatic repair.

LLMs are powerful precisely because their output is flexible. Production software needs the opposite property at its boundaries. ExOutlines provides that boundary.

## Reliable execution

Intelligent and data-intensive systems still need to get work done reliably.

### [Kathikon](https://github.com/AnimaLogica/kathikon)

A BEAM-native durable job queue and execution platform.

Kathikon treats a job as a durable obligation: it must eventually complete, retry, be cancelled, or be explicitly discarded, but it should never simply disappear.

Built on OTP and Mnesia, it provides durable execution without requiring PostgreSQL, Redis, RabbitMQ, or another external broker simply to run background work.

## A developing stack

Taken together, the projects cover increasingly large parts of a modern data system:

```text
                  Applications
                       |
        +--------------+--------------+
        |                             |
   Structured AI                 Rule systems
    ExOutlines                    ExDatalog
        |                             |
        +-------------+---------------+
                      |
             Knowledge / Graphs
       TerminusDB       ExGraphBLAS
                      |
               Computation
      ExDataSketch     ExSystolic
                      |
                  Data plane
        ExArrow       ExZarr
                      |
                   Codecs
                  ExCodecs
                      |
              Durable execution
                  Kathikon
                      |
                     OTP
```

This is not intended to become a monolithic framework.

Each project should remain useful independently. The value of the organization is that the pieces share a philosophy and can increasingly interoperate: streaming instead of unnecessary materialization, explicit data structures, deterministic cores, observable execution, native acceleration where justified, and BEAM-native APIs throughout.

## What we are exploring

AnimaLogica is particularly interested in the intersection of:

- Elixir, Erlang, and OTP
- streaming and larger-than-memory computation
- Apache Arrow and columnar systems
- scientific and multidimensional data
- sparse linear algebra and graph algorithms
- probabilistic data structures
- logic programming and Datalog
- knowledge graphs and provenance
- structured and explainable AI
- native Rust and Zig acceleration
- durable distributed execution

The underlying thesis is simple:

> **The BEAM should not have to sit beside the data and AI stack. It can be part of the data and AI stack.**

## Projects

| Project | Purpose |
| --- | --- |
| [ExArrow](https://github.com/AnimaLogica/ex_arrow) | Apache Arrow, Parquet, Flight, Flight SQL, ADBC, and native data pipelines |
| [ExZarr](https://github.com/AnimaLogica/ExZarr) | Zarr v2/v3 N-dimensional chunked arrays |
| [ExCodecs](https://github.com/AnimaLogica/codecs) | Extensible native codec framework |
| [ExDataSketch](https://github.com/AnimaLogica/ex_data_sketch) | Streaming probabilistic data structures |
| [ExGraphBLAS](https://github.com/AnimaLogica/ex_graphblas) | Sparse linear algebra and graph computation |
| [ExSystolic](https://github.com/AnimaLogica/ex_systolic) | Systolic and dataflow computation |
| [ExDatalog](https://github.com/AnimaLogica/ex_datalog) | Datalog rules, recursion, provenance, and reasoning |
| [TerminusDB Client](https://github.com/AnimaLogica/terminusdb-client-elixir) | Elixir client for the versioned document graph database |
| [ExOutlines](https://github.com/AnimaLogica/ex_outlines) | Validated structured output from LLMs |
| [Kathikon](https://github.com/AnimaLogica/kathikon) | Durable BEAM-native background jobs and task execution |

---

**AnimaLogica builds infrastructure for Elixir systems that need to move data, compute over it, reason about it, and act on it reliably.**
