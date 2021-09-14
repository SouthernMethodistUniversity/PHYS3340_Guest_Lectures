# PHSY3340: Introduction to Python and Related Lessons

We live in a world driven by computers, algorithms, and data. These 
lectures seek to equip students with the basic knowledge and skills to
use python to mainpulate data, produce basic models and make
decisions about the world around them. Students will also be introduced 
to high-performance computing using ManeFrame
II.

# Using Anaconda

## Installing and Loading Anaconda

This step can be skipped when using ManeFrame II (M2) as Anaconda is already
installed and available via `module load python/3`.

Directions for installing Anaconda on your own machine can be found
[here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html).
Either the full Anaconda or the miniconda distributions will work. The
differences between the two are noted on the installation page. More
information on getting started can be found
[here](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html#starting-conda).

## Installing the `phys_3340` Environment

1. `conda env create -f environment.yml --force`

## Using the `phys_3340` Environment

1. `conda activate phys_3340` to start (`source activate ~/.conda/envs/phys_3340` on M2)
2. `conda deactivate` when finished

## Remove Environment

1. `conda remove --name phys_3340 --all`

# Using Python Environments

## Loading a Python Environment

There are many Python 3 installations on M2. An example of one is given:

```
module purge
module load spack gcc-9.2
source <(spack module tcl loads --dependencies python@3.7%gcc@9.2)
```

## Installing the `phys_3340` Environment

```
python3 -m venv ~/.venv/phys_3340
source ~/.venv/phys_3340/bin/activate
pip install --upgrade pip wheel
pip install -r requirements.txt
```

## Using the `phys_3340` Environment

1. `source ~/.venv/phys_3340/bin/activate` to start
2. `deactivate` when finished

## Remove Environment

1. `rm -rf ~/.venv/phys_3340`

