# PageRank & HITS Computation

C++ implementations of PageRank and HITS (Hubs & Authorities), the two foundational link-analysis algorithms behind web search ranking.

## Problem

Ranking pages or nodes by importance in a large graph — like the web, a citation network, or a social graph — isn't just about counting inbound links. A link from a highly authoritative source should count for more than one from an obscure page. This project implements the two classic algorithms that solve this: PageRank (Google's original ranking method) and HITS (which separates "hub" and "authority" scores), built as part of the Information Retrieval and Web Search course at Ca' Foscari University.

## Approach

- Implemented PageRank using the power iteration method on a sparse adjacency matrix, with an adjustable damping factor (default 0.85) and convergence threshold (1e-5)
- Implemented HITS with mutual reinforcement between hub and authority scores, including query-based subgraph extraction and L2 normalization per iteration to prevent score explosion
- Built both from scratch in C++ for performance, with OpenMP support for parallelized updates on larger graphs
- Tested against standard graph formats (plain text edge lists, GML) for citation and web-link datasets

## Results

Both algorithms converge correctly on test graphs and produce ranked output (node ID, PageRank score, hub score, authority score). Runtime scales with graph size as expected for power-iteration methods — smaller graphs (10k nodes) complete in a few seconds, while larger graphs take proportionally longer.

**Note:** the original draft of this README included specific benchmark numbers (runtime/memory at 10k/100k/1M nodes on AWS c5.2xlarge). I've left those out here since I'd recommend only including benchmark claims you can actually reproduce and explain if asked in an interview — if you did run these tests, feel free to add the real numbers back in.

## Tech Stack

C++17, OpenMP (parallelization), GNU Autotools (build system for HITS)

## How to Run

```bash
# PageRank
git clone https://github.com/PatilKhushbu/pagerank-hits.git
cd pagerank-hits/pagerank
g++ -std=c++17 -O3 -fopenmp -o pagerank pagerank.cpp graph.cpp
./pagerank -a 0.85 -c 1e-5 -t web_links.txt

# HITS
cd ../hits
aclocal && autoconf && automake --add-missing
./configure --enable-optimize
make -j$(nproc)
./hits -q "machine learning" -f gml citations.gml
```

---

**Contributors:** Khushbu Mahendra Patil
**Faculty Advisor:** Prof. S. Orlando — Information Retrieval and Web Search (CM0473), Ca' Foscari University of Venice
