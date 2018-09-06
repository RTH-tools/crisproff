# crisproff
Off-targeting assessment of CRISPR-Cas9 gRNAs/on-targets

## CRISPRspec and CRISPRoff scores computation pipeline v1.1.1
================================================================================

### Prerequisites
* Python 2.7
* Biopython
* Vienna RNA Package (preferably 2.2.5): the script will call the RNAfold program when used
* Python libraries (optional): azimuth, numpy

Optional libraries are not necessary when you run the pipeline with "--no_azimuth" option.

### Usage
This pipeline DO NOT perform off-target predictions itself. It only computes
the CRISPRoff scores for given off-target sequences and the CRISPRspec score of
the gRNA/on-target based on given off-target data.

Please run the following command `python CRISPRspec_CRISPRoff_pipeline.py -h`
to read about which parameters to pass to the pipeline. Try our test runs below
to familiarize yourself with the pipeline parameters.

### Test suite
In the `crisproff/test_data/` folder, we have included several files that you
can use for the test runs presented below. Please run all the programs within
the `crisproff/` folder.

In its simplest form, you can run the pipeline for a single gRNA/on-target and
its off-target sequences (plain format: target per line, including the
on-target) with the following command. This would only report the CRISPRspec
score of the given gRNA/on-target (computed with given off-targets) to stdout.

	python CRISPRspec_CRISPRoff_pipeline.py --guide GGTGGACAAGCGGCAGATAGCGG --offtargets test_data/GGTGGACAAGCGGCAGATAGCGG_example_offtargets.txt --no_azimuth

Instead of reporting your results to stdout, you can use the
`--specificity_report` parameter to save your results in a file. Following
command will save the CRISPRspec result table in the
`crisproff/test_data/test_CRISPRspec.tsv` file.

	python CRISPRspec_CRISPRoff_pipeline.py --guide GGTGGACAAGCGGCAGATAGCGG --offtargets test_data/GGTGGACAAGCGGCAGATAGCGG_example_offtargets.txt --no_azimuth --specificity_report test_data/test_CRISPRspec.tsv


If you would like to generate the CRISPRoff scores as well, you have to provide
a directory using the `--CRISPRoff_scores_folder` parameter to save the scores
in the given directory. Following command will save the CRISPRoff results in
the `crisproff/test_data/` directory next to the CRISPRspec result table
`crisproff/test_data/test_CRISPRspec.tsv`.

	python CRISPRspec_CRISPRoff_pipeline.py --guide GGTGGACAAGCGGCAGATAGCGG --offtargets test_data/GGTGGACAAGCGGCAGATAGCGG_example_offtargets.txt --no_azimuth --specificity_report test_data/test_CRISPRspec.tsv --CRISPRoff_scores_folder test_data/

In the `crisproff/test_data/` folder, we also included two example RIsearch2
(v2.1) outputs generated for two gRNAs/on-targets given in
`crisproff/test_data/grnas_with_pam.fa`. To run the pipeline for both of these
gRNAs, you can call the pipeline like the following.

	python CRISPRspec_CRISPRoff_pipeline.py --guides test_data/grnas_with_pam.fa --risearch_results_folder test_data/ --no_azimuth --specificity_report test_data/test_CRISPRspec.tsv --CRISPRoff_scores_folder test_data/

This final run should generate three files in the `crisproff/test_data/`
folder: `test_CRISPRspec.tsv`, `GGGTGGGGGGAGTTTGCTCCTGG.CRISPRoff.tsv` and
`GGTGGACAAGCGGCAGATAGCGG.CRISPRoff.tsv`.

### How to use RIsearch2 (v2.1) to generate your off-target predictions?
You can perform your own off-target predictions using the [RIsearch2 (v2.1)](https://rth.dk/resources/risearch/) program. The program requires two input fasta files, one that includes the gRNA sequences and another one for the target genome. Example workflow about how to use the RIsearch2 program can be seen below. It is highly critical to run the RIsearch2 (v2.1) program with given options below to be able to generate the full list of off-target predictions (up to 6 mismatches) within the corresponding genome.

	risearch2.x -c genome.fa -o genome.suf
	risearch2.x -q grnas.fa -i genome.suf -s 1:20 -m 6:0 -e 10000 -l 0 --noGUseed -p3

Alternatively, you can also use the [Cas-OFFinder
webserver](http://www.rgenome.net/cas-offinder/) to generate the off-target
predictions for your gRNA and pass this result file to the pipeline with
`--offtargets` option.

### Citation
 If you find this software useful for your research,
 please cite the following work:

 [Citation comes here]

### Copyright
Copyright 2018 by the contributors (see AUTHORS file)

This is a free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This software is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this software, see LICENSE.
If not, see <http://www.gnu.org/licenses/>.


### Contact
ferro@rth.dk
gorodkin@rth.dk
