****************************************************************************************
Bipad Version 2.0 (Windows & Linux)
****************************************************************************************
Introduction:
Bipad is a software program for discovering TF binding motifs from ChIP-seq peak datasets based on recursive entropy minimization. It can build both homogeneous information models and bipartite ones with variable-length spacers.
****************************************************************************************
Compilation information
1. The Windows version was compiled in Microsoft Visual C++ 2015 Community Version on Windows 8.
2. The Linux version was compiled using GCC 5.3.0 on CentOS 6.7.
****************************************************************************************
Usage instructions:
1. Built-in help
	-h (switch): Showing usage instructions
2. Building homogeneous information models
	1. Required arguments
		-n: length of the information model
		-y: number of Monte Carlo cycles
		-f: name of the DNA sequence file corresponding to a ChIP-seq peak dataset
	2. Optional arguments:
		-2 (switch): indicating that both strands will be examined rather than only the positive strand
	3. Example commands:
		./Bipad_v2 -n 10 -y 1000 -f seq.txt -2
		./Bipad_v2 -n 10 -y 1000 -f seq.txt
3. Building bipartite information models:
	1. Required arguments
		-l: length of the left half site
		-r: length of the right half site
		-a: minimum gap size (should be smaller than -b)
		-b: maximum gap size (should be greater than -a)
		-y: number of Monte Carlo cycles
		-f: name of the DNA sequence file corresponding to a ChIP-seq peak dataset
	2. Optional arguments:
		-d (switch): indicating that a bipartite model of DR/RDR type will be built, either this argument or -i must be used
		-i (switch): indicating that a bipartite model of IR/ER type will be built, either this argument or -d must be used
	3. Example commands:
		./Bipad_v2 -l 6 -r 6 -a 1 -b 2 -y 1000 -f seq.txt -i
****************************************************************************************
Output files:
1. progress.txt: This file includes real-time progress information on the current run, which describes how many Monte Carlo cycles have finished and how much time each cycle took. 
2. output.txt: This file includes the final results of the current run, which contains the information model (i.e. information matrix), the frequency matrix, the optimal multiple alignment and its entropy, and the Rsequence value of the model. The alignment includes the position, strand and Ri value of the predicted binding site in each peak.
****************************************************************************************
Two examples are given below to further demonstrate how to use Bipad.
Example 1: Bipad will be applied to derive a homogeneous model of CTCF from the top 1000 peaks ranked by signal intensity in the ENCODE dataset of the optimal IDR thresholded type from the MCF-7 cell line. The Linux command for running Bipad is as follows.
./Bipad_v2 -n 15 -y 500 -2 -f CTCF_MCF7_top1000_seq.txt
The information matrix and frequency matrix are as follows.
0.150775	-1.75336	1.01395		-0.816559		278	74	506		142	
-2.10283	1.75163		-2.2593		-2.43484		58	844	52		46	
-4.0276		1.96413		-5.84083	-6.21522		15	978	4		3	
1.58711		-3.36278	-1.13248	-1.19697		753	24	114		109	
-2.70802	1.29286		0.415212	-4.12462		38	614	334		14	
-1.08289	0.993869	-2.15313	0.38469			118	499	56		327	
1.88845		-5.84083	-2.74611	-2.99857		928	4	37		31	
-9.38515	-9.38515	1.99621		-9.38515		0	0	1000	0	
0.782688	-5.54385	1.16528		-6.72218		431	5	562		2	
-3.09359	-4.0276		1.26919		0.490857		29	15	604		352	
-4.0276		-6.72218	1.96855		-6.72218		15	2	981		2	
-1.87471	-3.42322	1.77199		-2.23202		68	23	856		53	
-0.796434	1.55026		-3.36278	-1.34989		144	734	24		98	
0.634906	-2.9533		1.09967		-2.56497		389	32	537		42	
-1.6236		1.17295		0.201692	-1.91754		81	565	288		66	

Example 2: Bipad will be applied to derive a bipartite model of JUNB/AP1 from the top 500 peaks in the dataset of the optimal IDR thresholded type from the K562 cell line. The Linux command for running Bipad is as follows. As the bipartie motif of AP1 is of the IR/ER type, the -i argument should be used.
./Bipad_v2 -l 3 -r 3 -a 1 -b 2 -y 500 -i -f JUNB_K562_top500_seq.txt
The resultant information matrix and frequency matrix are as follows.
-8.38947	-8.38947	-6.515		1.98955			0	0	1	499	
-5.72651	-8.38947	1.92455		-2.55658		2	0	477	21	
1.97794		-4.84515	-6.515		-8.38947			495	4	1	0	

-8.38947	-8.38947	-8.38947	1.99243			0	0	0	500	
-4.54817	1.97794		-8.38947	-8.38947		5	495	0	0	
1.99243		-8.38947	-8.38947	-8.38947		500	0	0	0	
****************************************************************************************
References:
1. Bi,C. and Rogan,P.K. (2004) Bipartite pattern discovery by entropy minimization-based multiple local alignment. Nucleic Acids Res., 32, 4979–4991.
2. Landt,S.G., Marinov,G.K., Kundaje,A., Kheradpour,P., Pauli,F., Batzoglou,S., Bernstein,B.E., Bickel,P., Brown,J.B., Cayting,P., et al. (2012) ChIP-seq guidelines and practices of the ENCODE and modENCODE consortia. Genome Res., 22, 1813–1831.
3. Crooks,G.E., Hon,G., Chandonia,J.-M. and Brenner,S.E. (2004) WebLogo: a sequence logo generator. Genome Res., 14, 1188–1190.
4. Ruipeng Lu, Eliseos J Mucaki, Peter K Rogan. (2016) Discovery of Primary, Cofactor, and Novel Transcription Factor Binding Site Motifs by Recursive, Thresholded Entropy Minimization. BioRxiv, http://dx.doi.org/10.1101/042853