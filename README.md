This pipeline only requires 2 packages to be installed (and all it's dependencies)

PRESTO - https://github.com/scottransom/presto

FETCH - https://github.com/devanshkv/fetch

There are bugs with the latest version of FETCH and this pipeline so I suggest using an older version, specifically this version here https://github.com/devanshkv/fetch/tree/f9f385a15ac773282f75294870156223c0f1287a

Commit #f9f385a on Nov 2, 2019 

Todo: Update for compatibility with latest version of FETCH

# Preparing the data
As of March 2022 we found that there are sometimes dropped packets in filterbank data of CHIME/Pulsar Filterbank files
Therefore I have developed a script to correct the dropped packets. _This is reccommended for all observations untill it is fixed up stream_

`fdp_submit_jobs.sh *.fil` will submit a job for each filterbank file. The script expects you to give it all the filterbank files you're interesting in. For example I will do the following to correct observations of J0012+54


`fdp_submit_jobs.sh J0012+54*.fil` 

# Setting up your folder structure
Symlink all the filterbank files in some folder

`ln -s $FULL_PATH_TO_FILTERBANK $DESTINATION`

# CHIME-Pulsar_automated_filterbank
The best way to run is to run the following command. You will need to run this command twice, once for the presto part of the pipeline and once for the FETCH part. It was designed this way for ease of use on super computers

`check_single_pulse.sh -b -d $DM`


To run the FETCH part of the pipeline, please run

`check_single_pulses.sh -f` 

will run FETCH on any unprocessed `.fil` files in your current directory.

This script will only run the pipeline incrementally on `.fil` files, meaning that it will not rerun the same `.fil` file twice. If you want to do that either use the method below or copy your `.fil` file to an empty directory (symbolic link works).

`get_bright_bursts.sh -i .`

will grab all the astrophysical bursts and put them into `positive_bursts/` and create a `positive_burst.csv` file

