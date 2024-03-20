# SUBMIT
Script to submit quantum chemistry jobs to slurm. Working only on vera.C3SE

## Usage: 
	SUBMIT [inputfile] [program (optional)] [additional options (optional)]    (order is irrelevant)

## Supported programs:
- g16 - Gaussian16 (.com)
- orca - ORCA 5.0.1 (.inp)
- cp2k - CP2K 7.1 (.inp)
- python - Regular Python script (.py)
- ade - Python script for AutoDE (.py)
- crest - xyz file (.xyz)
- bash - bash script (.sh)
- vasp - VASP 6.4.4 (ask Martin access!) (no input file requested, but vasp keyword must be specified)

## Additional options:
	-m [filenames] - launch multiple jobs in succession (not implemented yet)
	-t [time] - time limit (formats: Dd, HHh, MMm, HH:MM:SS or D-HH:MM:SS. Default = 12h, Max is 7d) Examples: -t 30m; -t 02h; -t 1d
	-n [1-32] - number of cores (default = 32, Max on Vera = 32)    
	-N [1-2]  - number of nodes (default = 1)    
	-M [1-1024]  - total allocated memory in GB (default = 64) 
	-p [partition] - vera or lux (default = vera) 
	-J [job name] - sbatch job name (default = input file name, without extension. For vasp: vasp_[current folder])
	[any other key(s)] - additional argument (only for bash, python and crest). Can be put in quotes. Example: SUBMIT this.sh "arg1 arg2 arg3" 
	--arg [argument] - same as above, when [argument] is conflicting with SUBMIT script (e.g. -n or -t). Again, "[argument(s)]" can be put in quotes.
	--chk - (only for gaussian) put \hk=[filename].chk on top of the input file
	--debug - prints the submitter.sh file and does NOT launch the calculation

### Time limit pre-sets:  
	test	- 10m     
	short	- 01h
	long	- 5d

### Other:
	mailme	- send email to the user when the job is finished. It takes you CID automatically and send it to CID@chalmers.se

## Examples:
	SUBMIT test.com test
	SUBMIT longassjob.inp cp2k -t 7d -M 196 -N 2 mailme
	SUBMIT input.inp
	SUBMIT vasp -t 06h 
	SUBMIT CCSDT_SinglePoint.com -M 800 -t 1d
	SUBMIT pythonscript.py -n 1 -t 10m
	SUBMIT bashscript.sh 
	SUBMIT bashscript.sh "10 100 1000"

