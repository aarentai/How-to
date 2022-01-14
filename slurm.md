### Log in
```
ssh medusa.sci.utah.edu
```
then go to the folder you plan to run the code

### slurm script example
```
#!/bin/bash

# Example of running python script in a batch mode

#SBATCH -J metcnn
#SBATCH -p dgx
#SBATCH -t 72:00:00
#SBATCH -o output_dgx.out
#SBATCH --gres=gpu:2

# Load software

# Run python script
which conda
#/home/sci/hdai/anaconda2/bin/conda init bash
#source ~/.bashrc
eval "$(/home/sci/hdai/anaconda2/bin/conda shell.bash hook)"
conda activate pytorch17
which python
python /home/sci/hdai/Projects/MetCnn3D/MetCnnBrainPatchedSlice.py
```
Remark:
1.`#SBATCH -J metcnn` sets job name
2.`#SBATCH -t 72:00:00` sets running time limit
3.`#SBATCH -o output_dgx.out` designates the output log
4.`#SBATCH --gres=gpu:2` is for designating how many gpus you intend to use

### sbatch
Submit a job by
```sbatch run.slurm```
where `run.slurm` is the script above.

### scancel
Kill a job by
```scancel $JOBID```

### squeue
List jobs by
`squeue -u hdai`