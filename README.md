# panSieve

panSieve is a tool for extracting unique sequences from pangenome graphs. It processes GFA (Graphical Fragment Assembly) files and extracts non-redundant sequences, including references and unique variants.

## Features

- Processes both uncompressed and gzipped GFA files
- Converts graph files to vg format for processing
- Extracts reference sequences and generates variant calls
- Creates non-redundant sequence sets
- Supports both FASTA and FASTQ output formats
- Configurable through external configuration files

## Prerequisites

The following tools must be installed and available in your PATH:

- [vg](https://github.com/vgteam/vg) (Variation Graph Tool) v1.61.0
- [seqkit](https://github.com/shenwei356/seqkit) v2.10.0

You can set up a conda environment using the `environment.yml` file

```bash
conda env create -n pansieve --file environment.yml
conda activate pansieve
```

## Installation

```bash
git clone https://github.com/promicrobial/panSieve.git && cd panSieve
chmod +x src/sieve
```

## Usage

```bash
./src/sieve <input.gfa[.gz]> <config_file>
```

## Arguments

```txt
<input.gfa[.gz]>: Input GFA file (can be gzipped)
<config_file>: Configuration file containing paths and settings
```

## Configuration File

The configuration file should contain the following variables:

`OUTPUT_DIR` /path/to/output/directory `OUTPUT_FILENAME` output.fasta OR output.fastq

## Example

```bash
# Create a configuration file
echo "OUTPUT_DIR=./output" > config.conf
echo "OUTPUT_FILENAME=sequences.fa" >> config.conf

# Run panSieve
./src/sieve input.gfa config.conf
```

## Output

The tool generates a non-redundant set of sequences in either FASTA or FASTQ format.

Intermediate files are automatically cleaned up after processing

## Documentation

Full documentation is available in the [docs](docs/) directory.

## License

MIT

## Citation

If you use panSieve in your research, please cite: [Citation Information]
