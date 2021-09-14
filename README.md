# PHSY3340: Introduction to Python and Related Lessons

We live in a world driven by computers, algorithms, and data. These 
lectures seek to equip students with the basic knowledge and skills to
use python to mainpulate data, produce basic models and make
decisions about the world around them. Students will also be introduced 
to high-performance computing using ManeFrame
II.

# Getting Started

## Initial Setup of Your Repository and Python Environment

1. Go to the [GitHub repository for our class Jupyter notebooks](https://github.com/SouthernMethodistUniversity/PHYS3340_Guest_Lectures).
2. Select "Fork". This will create a personal copy of the repository.
3. Select "Code" and copy the HTTPS URL for the forked repository.
4. Go to the [HPC Portal](https://hpc.smu.edu) and log in.
5. Select "Interactive Apps" and then "JupyterLab".
6. Set the fields to:
  * "Additional environment modules to load": `python/3`
  * "Custom module paths": Clear the contents if any
  * "Custom environment settings": Clear the contents if any
  * "Partition": `htc`
  * "Number of hours" `1`
  * "Number of nodes": `1`
  * "Cores per node": `1`
  * "GPUs per node": `0`
  * "Memory": `6`
7. Select "Launch" and wait for the job and JupyterLab session to begin (this can take a few minutes).
8. Select "Connect to JupyterLab", which will appear when the JupyterLab session has started.
9. Select "File", "New", "Terminal" to start a new terminal session within JupyterLab.
10. In the terminal session, type each command and press Enter:

```
git clone <paste the URL for the forked repository without brackets>
cd PHYS3340_Guest_Lectures
git remote add upstream https://github.com/SouthernMethodistUniversity/PHYS3340_Guest_Lectures.git
mkdir work
module load python/3
conda env create -f environment.yml --force
```

## Launching a JupyterLab Session and Accessing Your Notebooks

1. Go to the [HPC Portal](https://hpc.smu.edu) and log in.
2. Select "Interactive Apps" and then "JupyterLab".
3. Set the fields to:
  * "Additional environment modules to load": `python/3`
  * "Custom module paths": Clear the contents if any
  * "Custom environment settings": `source activate ~/.conda/envs/phys_3340`
  * "Partition": `htc`
  * "Number of hours" `24`
  * "Number of nodes": `1`
  * "Cores per node": `1`
  * "GPUs per node": `0`
  * "Memory": `6`
4. Select "Launch" and wait for the job and JupyterLab session to begin (this can take a few minutes).
5. Select "Connect to JupyterLab", which will appear when the JupyterLab session has started.
6. Select the "File Browser" icon at the top of the left sidebar and browse to your `PHYS3340_Guest_Lectures` directory.

## Working on Notebooks

1. Browser into "code" directory.
1. Right-click on a notebook and select "Copy".
2. Browse into your "work" directory.
3. Right-click with the directory and select "Paste".
4. Double click the notebook to open.

## Pulling New Notebooks

1. Save the notebook.
2. Open a terminal session via "File", "New", "Terminal".
3. In the terminal session, type each command and press Enter after each line:

```
cd PHYS3340_Guest_Lectures
git fetch upstream
git merge upstream/main -m "Merge from upstream."
```

```{note}
* If you have edited a file tracked upstream, *e.g.*  `assignment.ipynb`,
  you won't be able to merge. Checkout the file to clear the changes, *e.g.* `git
  checkout assignment.ipynb`, and then proceed with `git merge
  upstream/main -m "Merge from upstream."`.
* If the above doesn't work, first verify that all notebooks that you want to
  save are in your `work` directory, then run `git reset --hard`, and then
  proceed with the fetch and merge steps.
```

## Installing New Packages

New Python packages can be installed allowing you to build upon the work of
others. Both methods should be run from the Terminal from within the Jupyter
Lab session. Installing packages directly via `pip` is the suggested procedure
for the class when installing your personaly selected packges, while
installation via the `requirements.txt` should be reserved for packages pushed
from upstream.

1. Open a terminal session via "File", "New", "Terminal".
2. In the terminal session, type each command and press Enter after each line:

### New Packages via `pip`

```
cd PHYS3340_Guest_Lectures
pip install <package_name>
```

### New Packages via `requirements.txt`

Before executing the following commands do the "Pulling New Notebooks" commands
above first. This will make sure that you have the most recent version of the
`requirements.txt` file available to you. 

```                                                                           
cd PHYS3340_Guest_Lectures                                                          
pip install --ignore-installed -r requirements.txt
```                                                                           

## Submitting Completed Assignments via GitHub

1. Save the notebook.
2. Open a terminal session via "File", "New", "Terminal".
3. In the terminal session, type each command and press Enter after each line:

```
cd PHYS3340_Guest_Lectures
git add work/<the name of the completed notebook without brackets>.ipynb
git commit -m "<Brief note about work witout brackets>"
git push
git tag -a <assignment number without brackets> -m "<Completed assignment number without brackets>"
git push --tags
```
## Add Dr. Olness to Your Forked GitHub Repository

1. Log into GitHub
2. Go to your PHYS3340_Guest_Lectures repository
3. Select "Settings"
4. Select "Manage access" on the left-side panel
5. Select "Invite a collaborator"
6. Type "olness" in the field and then select "Fred Olness" when it appears
7. Select "Add egodat to this repository"
