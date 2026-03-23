# ETP²E — Euler Topological Planar Partition Explorer
<img width="1908" height="992" alt="image" src="https://github.com/user-attachments/assets/bd148000-e5f3-4f52-be3d-a5dfb5d11b49" />
<img width="1032" height="966" alt="image" src="https://github.com/user-attachments/assets/a75b0f66-af36-4f7a-88da-6bb483153b3b" />


**Parse Eulerian-style topological planar stroke patterns • Enumerate combinatorial partitions by drawing mode • Visualize clipped & paginated results**
ETP²E is an interactive web-based explorer that takes simple **stroke-based SVG patterns** and systematically enumerates topologically meaningful ways of partitioning / combining them under three different generation philosophies:

- **Stroke-only** (S!) — treats each `<path>` as one atomic stroke  
- **Slice-only** (C!) — considers all possible cutting / crossing points between strokes  
- **Stroke-then-Slice** (StC) — first takes stroke paths, then applies slicing to each resulting piece  

Results are clipped to a square canvas, deduplicated (up to topological equivalence in many cases), and presented in an elegant card-based paginated gallery.

### Motivation
This tool was originally created to assist in the generative design of **logographs** for constructed languages (conlangs), where a small number of strokes should produce a rich, visually-distinct set of glyphs while obeying strong topological / combinatorial constraints.



The early motivation for this is because of my attempt to prove this preposition:Let a graph have 𝐿 edges. Under the assumptions that every subset of edges forms a valid stroke and strokes are identified up to reversal, the number of distinct strokes is what???
<details>
  <summary>Proof Attempt (unfinished):</summary>
  
$$ \text{Proposition. Let } L \text{ be the total number of lines. Then the total number of distinct single-stroke combinations (modulo reversal) is} $$
$$ T_L = \binom{L}{1} + \sum_{k=2}^{L-1} \left( \binom{L}{k} - 1 \right) + \binom{L}{L}. $$
$$ \text{Proof.} $$
$$ \text{For each } k = 1,2,\dots,L, \text{ there are } \binom{L}{k} \text{ ways to choose } k \text{ lines.} $$
$$ \text{Each such choice represents a candidate single-stroke combination.} $$
$$ \text{For } k = 1, \text{ reversal does not produce a new combination.} $$
$$ \text{For } k = L, \text{ the full set of lines forms a single combination.} $$
$$ \text{For each } k = 2,\dots,L-1, \text{ each combination has a reverse, which is considered equivalent.} $$
$$ \text{Thus, one duplicate must be removed for each such } k. $$
$$ \text{There are } (L - 2) \text{ such values of  k, so we subtract 1 from each corresponding term.} $$
$$ \text{Therefore,} $$
$$ T_L = \binom{L}{1} + \sum_{k=2}^{L-1} \left( \binom{L}{k} - 1 \right) + \binom{L}{L}. $$
$$ \square $$
</details>

It is also useful for mathematicians and topologists interested in:
- stroke-based curve enumeration  
- planar graph / arrangement partitioning  
- connected vs. visually-disconnected stroke components  
- controlled combinatorial explosion in low-stroke regimes (especially 2–5 strokes)

## Features
- Upload or paste **SVG stroke patterns** (single-layer, path-based)
- Three enumeration modes: **S!** • **C!** • **StC**
- Option to filter to **only 2D-connected strokes** (eliminates topologically-connected but visually-disjoint pieces)
- Real-time statistics:
  - base strokes
  - theoretical maximum combinations
  - actually generated & valid candidates (capped at 50 000)
  - scanned candidates (uncapped count)
  - generation time
- Clean, paginated card gallery (20 results / page)
- Direct jump to any page
- Results clipped to consistent square bounds

## How to Use

### 1. Prepare your stroke pattern (SVG)

Use any vector editor:

- **Recommended**: Adobe Illustrator, Inkscape, Affinity Designer, Boxy SVG
- **Quick option**: Figma

Steps in Figma (example):

1. Create a square frame  
2. Draw strokes using:
   - **Line tool** (L)  
   - **Rectangle** (R) → convert to path if needed  
   - **Ellipse** (O)  
3. Select the frame → right-click → **Copy as SVG**  
4. Paste the copied SVG code into the textarea on the ETP²E page

**Important**: Only `<path>` elements are currently parsed. No fills, groups, transforms, or raster images.

### 2. Generate partitions

| Field                        | Meaning                                                                                 | Typical values     |
|------------------------------|-----------------------------------------------------------------------------------------|--------------------|
| `possible_strokes`           | Maximum number of strokes used in each generated glyph                                  | 1 – 6              |
| `mode`                       | S! • C! • StC                                                                           | StC often richest  |
| `is_connected_stroke_only`   | Discard strokes that are topologically connected but visually separated in 2D           | usually **on**     |
| `go_to_page`                 | Jump directly to result page                                                            | —                  |

Click **Generate** → wait a few seconds to minutes (depending on parameters).

### 3. Explore results

- Browse cards (20 per page)
- Look at generation # and SVG preview
- Interesting disconnected-but-connected examples often appear around pages 20–40 when `is_connected_stroke_only` is off

## Real-world Application Example

**Conlang logograph generation**

Many constructed language designers want small stroke sets (3–5 strokes) that still produce hundreds or thousands of visually-distinct glyphs.

Try these settings for nice results:

- `possible_strokes`: **3**  
- `mode`: **StC** (Stroke-then-Slice)  
- `is_connected_stroke_only`: **on**

You will usually get a rich, calligraphic-feeling set of candidate logographs.

## Planned Improvements

- Export selected SVGs (single or batch)  
- Better duplicate / near-duplicate filtering using more invariant features  
- Interactive stroke coloring / labeling  
- Elementary mathematical proof & formulas for the combinatorial bounds  
- Support compound paths and basic transforms in input SVG  
- WebAssembly acceleration for larger stroke counts

## Contributing

Pull requests welcome — especially:

- performance optimizations  
- better topological filtering  
- mathematical documentation of the enumeration bounds

## License
MIT
