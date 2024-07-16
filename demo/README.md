## Example data
`case.bam`, `case.bam.bai`,  `control.bam`,  `control.bam.bai`

## Expected results
`line.vcf` - expected results

## Running
- copy the example data (BAM and BAI files) to some directory
- pull Docker image from Dockerhub: `docker pull crankycrank/totalrecall:demo-hg19`
- start a container: `docker run -it -v /path/to/workdir:/mnt crankycrank/totalrecall:demo-hg19`
where `/path/to/workdir` should be replaced with the full path to the directory example data were copied to
- (within the container) `cd /mnt`
- run from the directory input files were copied to:
```
LC_ALL=C snakemake -j 1 -s /opt/totalrecall/Snakefile -p results.tgz
```

### Using Singularity/Apptainer
Alternatively, Docker image can be converted to a Singularity image:
```
singularity build totalrecall-demo-hg19.sif docker://crankycrank/totalrecall:demo-hg19
```
Then the code can be run from the working directory as follows:
```
singularity exec --no-home -B /path/to/workdir/ totalrecall-demo-hg19.sif snakemake -j1 -s /opt/totalrecall/Snakefile -p results.tgz``
```