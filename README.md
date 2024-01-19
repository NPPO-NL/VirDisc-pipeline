# VirDisc-pipeline
A CLC pipeline for the discovery of _de novo_ assembled viral and viroid putative sequences as part of a High-Throughput Sequencing test.

VirDisc is bio-informatics pipeline for the discovery of _de novo_ assembled viral and viroid putative sequences to use in CLC Genomics. In short, the pipeline takes illumina sequencing data obtained from plant rRNA depleted total RNA. A quality trim of the reads is performed, followed by a _de novo_ assembly and consensus sequences extraction with a minimal read depth of 10.  The consensus sequences larger than 100 nt are selected. Firstly, these sequences are analysed using megablast  and, for sequences with no megablast hit by using DIAMOND with a local installation of the NCBI nt and nr databases, respectively. BLAST results are visualized in Krona to identify putative viral or viroid sequences. Secondly, a Pfam domain search is performed with the in 6 reading frames translated consensus sequences. The same pipeline is repeated with 1% of the trimmed reads, because _de novo_ assembly of high coverage contigs can be problematic by resulting in fragmented assemblies. 
The pipeline also contains a control section in which the trimmed reads are used to 1) assemble the chloroplast rbcL gene to identify plant species by megaBLAST and visualization of the outcome by Krona, 2) map to nuclear and chloroplast rRNAs to monitor the rRNA depletion efficiency and to identify the number of non-rRNA reads 3) map to selected ERCC sequences, to monitor the sequencing efficiency from a control sample and to monitor contamination and/or cross-talk from the control sample to the diagnostic samples.

_Installation guide_\
To be able to use the VirDisc pipeline several installations need to be in place. It is a CLC workflow containing CLC internal and external applications. Therefore, CLC genomics workbench and CLC Server are mandatory dependencies. Moreover, CEAs and dependencies have to be installed on all jobnodes and CEA configurations need to be imported. Finally, the workflow has to be imported or reconstructed.

Up to date installation guides regarding CLC Genomics Workbench and CLC Server can be found at:
https://resources.qiagenbioinformatics.com/manuals/clcgenomicsworkbench/current/User_Manual.pdf. 
https://resources.qiagenbioinformatics.com/manuals/clcserver/current/admin/User_Manual.pdf.

_CEAs, dependencies and importing CEA xml_\
Information about CEAs and their dependencies can be found at https://github.com/NPPO-NL/CLC-External-Applications. The VirDisc pipelines uses the following CEAs: 
- CEA001_blastn
- CEA002_DIAMOND
- CEA003_Chunk_file
- CEA004_Select_chunks_without_hits
- CEA005_Krona
- CEA007_BLASTn_taxonomy_sorter
- CEA008_Sequence_selector\
After installing CEAs and their dependencies, the CEAs need to be configured correctly. To configure different aspects of a CLC Server, including importing the CEA configuration file, a web portal is available for administrators. Download "VirDisc-CEA-configuration.xml" to a location accessible to your CLC web portal. Subsequently, access your CLC web portal, navigate to “Extensions” and “External applications”. The external application configuration file can be imported to a CLC Server by clicking on the “Import configuration...” button. Browse and select the xml file.
After importing the xml, make sure that the paths to the scripts are all accessible. Paths to scripts and or databases can be changed manually for each individual CEA, in the command line text box within the external application editing view (Figure 27). This step is mandatory if the scripts and or databases cannot be found in the specific locations of the CEA configuration file.

_Importing workflow_\
After configuring the CEAs, the CLC workflow needs to be imported. Please download “VirDisc_pipeline.clc” and import the file using the standard import function of CLC Genomics Workbench. If all CEAs are correctly configured this workflow is ready to use.
