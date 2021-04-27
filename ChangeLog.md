##v 1.1.2 - 2021-04-26
- Ported to python3
- updated test data output (previous version from 1.1.1 was with an older
  version of RNAfold, which gives slightly different results)
- added test.sh
##v 1.1.1 - 2018-09-06
- Resolving a bug in on-target detection from risearch results
- Structuring the messy stdout and stderr output
- README.md file has been updated with example test runs.
##v 1.1 - 2018-08-21
- --evaluate_all option added to evaluate gRNAs even if they have no on-targets
- --comment_out_NAs option added for easier pasrsing of the specificty report
- enabled using --guides and --guide options together to focus only on one gRNA from the file fed with --guides 
- --chromosome_names option added to be able to read multiple risearch files for each gRNA
- --ignored_chromosomes option added to limit your off-targets to certain chromosomes
- several other bug fixes and performance improvements
##v 1.0 - 2018-04-27
- First official release

