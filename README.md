# panSieve

panSieve is a command-line tool for extracting unique sequences from pangenome graphs. It processes GFA (Graphical Fragment Assembly) files to identify and extract non-redundant sequences, including references and unique variants.

## Features

- Processes both uncompressed and gzipped GFA files
- Converts graph files to vg format for processing
- Extract reference paths and variant sequences
- Remove redundant sequences through deduplication
- Supports both FASTA and FASTQ output formats

## Prerequisites

The following tools must be installed and available in your PATH:

- bash (version 4+)
- Standard Unix tools (e.g. gunzip)
- [vg](https://github.com/vgteam/vg) (Variation Graph Tool) v1.61.0
- [seqkit](https://github.com/shenwei356/seqkit) v2.10.0

You can set up a conda environment using the `environment.yml` file. This process should only take a few minutes.

```bash
conda env create -n pansieve --file environment.yml
conda activate pansieve
```

## Installation

```bash
git clone https://github.com/promicrobial/panSieve.git && cd panSieve
chmod +x src/sieve

# Optionally, add to your PATH
export PATH=$PATH:$(pwd)/panSieve/src

```

## Usage

Basic usage:
```bash
sieve -i <input.gfa[.gz]> -o <output_dir>
```

Depending on available resources, a GFA file of ~3GB should be processed withint 15 minutes.

Full options:
```bash
Usage: sieve [options] -i <input.gfa[.gz]> -o <output_dir>

Description:
    Process a variant graph file (GFA or GFA.gz) and extract non-redundant sequences,
    including the reference and unique variants.

Required Arguments:
    -i, --input FILE    Input GFA file (can be gzipped)
    -o, --output DIR    Output directory (default: ./output)

Optional Arguments:
    -f, --outfile STR   Basename for output files (default: sieved-pangenome)
    -t, --threads INT   Number of threads to use (default: all available)
    -s, --stats        Generate detailed graph statistics
    -v, --verbose      Enable verbose output (shows commands being executed)
    -d, --debug        Enable debug output (shows detailed debugging information)
    -k, --keep-temp    Keep temporary files
    -l, --log FILE     Log output to specified file
    --dry-run         Show commands without executing them
```

## Output Files

The tool generates a non-redundant set of sequences in either FASTA or FASTQ format.

Intermediate files are automatically cleaned up after processing

```
<output_dir>/
├── graph.xg                         # GFA input graph in VG format
├── sieved-pangenome.fa              # Original sequences
├── sieved-pangenome-dedup.fa        # Deduplicated sequences (final output file)
├── sieved-pangenome.stats           # Sequence statistics
├── sieved-pangenome-sequence-lengths.txt     # Sequence lengths
└── sieved-pangenome-graph.stats     # Graph statistics (if --stats specified)
```

## Examples

Process a GFA file and generate statistics:
```bash
sieve -i input.gfa -o results -f sample1 -t 8 --stats
```

Process a compressed GFA file:
```bash
sieve -i input.gfa.gz -o results -v
```

Dry run to see what commands would be executed:
```bash
sieve -i input.gfa -o results --dry-run
```

## Testing

The repository includes a comprehensive test suite. To run the tests:

```bash
cd test
./test-sieve
```

## Documentation

Full documentation is available in the [docs](docs/) directory.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Citation

If you use panSieve in your research, please cite:

```bibtex
@software{cole_pansieve_2024,
  author       = {Cole, Nathaniel},
  title        = {panSieve: A tool for extracting unique sequences from pangenome graphs},
  year         = {2024},
  publisher    = {GitHub},
  url          = {https://github.com/cpnh/panSieve}
}
```
## Acknowledgments

Test data sourced from the [vg project](https://github.com/vgteam/vg).
