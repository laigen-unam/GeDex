# GeDex
A consensus Gene-disease Event Extraction System based on frequency patterns and supervised learning

Welcome to the repository for the GeDex gene-disease extraction system. This tool was created to retrieve consensus gene-disease associations from a collection of biomedical research abstracts. For a more detailed description, please see <b>upcoming paper</b>.

## Using GeDex  

Currently, there are a couple of options that allow a user to use GeDex. 
1) A Bitbucket repository at https://bitbucket.org/laigen/gedex/src/master/
2) A Docker Hub at https://hub.docker.com/r/laigen/gedex
With Docker you will not need to install any of the dependencies or specific program versions that are used in this project; everything is neatly packaged for immediate use.
  
  
## Docker (fast and easy!)  

With Docker you will not need to install any of the dependencies or specific program versions that are used in this project; everything is neatly packaged for immediate use.
  
  
### Installation  

First, make sure that Docker is installed and running. You can read more information on how to do this by visiting https://www.docker.com/products/container-runtime.   
Once you have Docker installed, you will need to pull the corresponding image from dockerhub (https://hub.docker.com/r/laigen/gedex). You can do this by typing the following command into your terminal.

```bash
docker pull laigen/gedex
```

This will get the latest image for gedex at the time of execution. Some dependencies are a little large, so you can definitley take a bathroom break at this point.

### Getting predictions  
So now for the fun part. You can create a directory with any name you like. 

```bash
mkdir testgedex
cd testgedex
```
  

Inside of this directory, there must be a file called **pmids.txt**. This file must contain a list of the PubMed IDs from the articles you wish to analyze. Each line must contain one PubMed ID. You can use [input-corpora/pmids.txt](https://bitbucket.org/laigen/gedex/src/master/input-corpora/pmids.txt) as an example. This will be the input for the entire pipeline.  
  
To actually get predictions we must first decide on the number of CPUs that will be used for the tasks at hand. Keep in mind that larger collections will requiere a lot of computing power in order to finish quickly. In our example we will use 4 CPUs.  
  
```bash
NUM_JOBS=4
```

Now we are ready! We can run the entire GeDex pipeline with the following command

```bash
docker run -v "${PWD}:/input-corpora" --rm -it laigen/gedex:latest bash -c "cd scripts && sh run-gedex.sh ${NUM_JOBS}"
```
And that is it. The pipeline will run automatically, displaying helpful messages along the way. Final predictions will be found in the **predictions/** directory.

Have fun!
