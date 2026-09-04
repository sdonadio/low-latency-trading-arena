# Low-Latency Trading Arena

An interactive companion for a graduate course on low-latency trading systems
in C++. Sixteen pages — a course map plus one page per topic — each built
around live, clickable widgets rather than static slides: a tick-to-trade
waterfall whose stages you can price in nanoseconds, an order book you can post
into and get stuck at the back of the queue in, a micro-benchmark you can ruin
four different ways, a struct whose fields you reorder until the padding
disappears, and a latency histogram whose p99.9 you can blow out with a single
`new`.

The thesis of the course is that high-frequency trading is not forecasting, it
is a **race**. Two bots running the same idea finish in the order their
messages reach the matching engine, so the only thing speed buys you is a place
in a FIFO queue — and the number that decides whether you got there is not the
mean but the **tail**: p50, p99, and above all **p99.9** of tick-to-trade.

## Two tracks, identical content

The material is taught in two formats. The 15-week track gives each topic its
own session. The condensed 9-session track pairs adjacent topics into one
longer meeting; nothing is dropped and nothing is reordered. Every topic page
shows both positions in its hero, and the course map on `index.html` regroups
the fifteen cards into the nine sessions at the flick of a switch.

| Week | Topic | Session (9-session track) |
|------|-------|---------------------------|
| 1 | HFT Landscape & Market Microstructure | 1 |
| 2 | C++ Performance Foundations | 2 |
| 3 | Memory Management & Smart Pointers | 2 |
| 4 | Custom Allocators & Memory Pools | 3 |
| 5 | Templates & Generic Programming | 3 |
| 6 | Compile-Time & Policy-Based Design | 4 |
| 7 | Data Structures for HFT — The Order Book | 4 |
| 8 | Algorithmic Complexity & Time-Series | 5 |
| 9 | Concurrency I — Atomics & Memory Models | 5 |
| 10 | Concurrency II — Lock-Free Pipelines | 6 |
| 11 | Network Protocols & Market Data | 7 |
| 12 | Async I/O & Serialization | 7 |
| 13 | Low-Latency Design — SIMD & Kernel Bypass | 8 |
| 14 | Profiling, the Tail & Production | 8 |
| 15 | Latency Arbitrage, Multi-Venue & the Tournament | 9 |

Nothing is thrown away: the order book of week 1 is the data structure of week
7; the cost model of week 2 justifies the pool of week 4; the ownership rules
of week 3 are what make that pool safe; the cache line of week 2 becomes the
false sharing of week 9 and the padded indices of week 10's ring; and weeks
13–14 spend the last microseconds that week 15's cross-venue race is won with.

## The code

Each topic's lab and homework build one piece of a C++ trading bot that
connects to a live matching engine and is graded on tick-to-trade latency. Two
public starter repositories carry the header stubs, the autograder and the
arena client:

- [hft-cpp-starter-columbia](https://github.com/sdonadio/hft-cpp-starter-columbia)
  — 15-week track starter
- [hft-cpp-starter-uchicago](https://github.com/sdonadio/hft-cpp-starter-uchicago)
  — 9-session track starter

Every C++ snippet shown on this site is real, standalone C++20 and compiles
with `clang++ -std=c++20` (or `g++`), except where a fragment is explicitly
quoted from the starter's own headers.

## Self-contained static HTML

Every page is a single `.html` file with exactly one inline `<style>` block and
one inline `<script>` block. There are no images, no build step, no package
manifest, no CDN and no external requests of any kind — the only outbound links
are to this repository, to the two starter repositories, and (from the course
map) to the two sibling sites. All diagrams are inline SVG drawn by the page's
own script. Each page shares one byte-identical CSS custom-property palette, so
re-theming the site means editing the `:root` block.

Pages are keyboard-accessible, carry `aria-label`s on every control and every
generated diagram, honour `prefers-reduced-motion`, and collapse to a single
column below 720px with no horizontal overflow.

## Sibling sites

Same shape, same contract, different subject:

- [Computer Architecture Arena](https://sdonadio.github.io/computer-architecture-arena/)
  — the prequel: the machine your C++ actually runs on, from the Turing machine
  to tick-to-trade.
- [Financial Markets Arena](https://sdonadio.github.io/financial-markets-arena/)
  — the finance introduction: what a market is, who trades in it, and what a
  spread pays for.

## Run it locally

```sh
git clone https://github.com/sdonadio/low-latency-trading-arena
cd low-latency-trading-arena
python3 -m http.server
```

Then open <http://localhost:8000/>.

Opening `index.html` directly from the filesystem also works, since nothing is
fetched over the network.

## Deploying

The site is plain static files, so GitHub Pages serves it as-is from the
repository root. `.nojekyll` is present so Pages skips Jekyll processing.

## Browser support

Any current browser. The pages use CSS custom properties, CSS grid, inline SVG
and ES5-compatible scripts.

## Licence

Content © the author, all rights reserved.
