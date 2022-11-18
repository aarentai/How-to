### Overview
A cluster is a group of inter-connected computers or hosts that work together to support applications and middleware (e.g. databases).  In a cluster, each computer is referred to as a “node”. Unlike grid computers, where each node performs a different task, computer clusters assign the same task to each node. 

### Logging into the clusters
```
ssh medusa.sci.utah.edu
ssh u1265496@notchpeak.chpc.utah.edu
```

### slurm script example
```
#!/bin/bash

#SBATCH --job-name=haocheng
#SBATCH --account=delacy-gpu-np
#SBATCH --partition=delacy-gpu-np
#SBATCH --gres=gpu:1
#SBATCH --time=2:00:00
#SBATCH --output=/scratch/general/lustre/u1265496/Projects/Metric-Cnn-3D/Models/IpmiSubjects/output.txt
#SBATCH --nodes=1 
#SBATCH --ntasks=64
#SBATCH --mem=100G

which conda
#/home/sci/hdai/anaconda2/bin/conda init bash
#source ~/.bashrc
eval "$(/home/sci/hdai/anaconda2/bin/conda shell.bash hook)"
conda activate pytorch17
which python
python /home/sci/hdai/Projects/MetCnn3D/MetCnnBrainPatchedSlice.py
```

### Remarks
| Options     | Descriptions                                                                                                                |
|-------------|-----------------------------------------------------------------------------------------------------------------------------|
| --job-name  | Specify a name for the job allocation.                                                                                      |
| --acount    | Charge resources used by this job to specified account.                                                                     |
| --partition | Request a specific partition for the resource allocation.                                                                   |
| --gres      | Specifies a comma-delimited list of generic consumable resources.                                                           |
| --time      | Set a limit on the total run time of the job allocation.                                                                    |
| --output    | Instruct Slurm to connect the batch script's standard output directly to the file name specified in the "filename pattern". |
| --nodes     | Request that a minimum of minnodes nodes be allocated to this job.                                                          |
| --ntasks    | sbatch does not launch tasks, it requests an allocation of resources and submits a batch script.                            |
| --mem       | Specify the real memory required per node.                                                                                  |
1. --time: If the requested time limit exceeds the partition's time limit, the job will be left in a PENDING state (possibly indefinitely).
2. --output: Remember to create the path before run the slurm script, or the job can nerver be launched due to slurm cannot create path.

### sbatch
Submit a job by
```sbatch run.slurm```
where `run.slurm` is the script above.

### squeue
List jobs by
```squeue -u hdai```

### scancel
Kill a job by
```scancel $JOB_ID```

### scontrol
Read detail of a job by
```scontrol show job $JOB_ID```

### nvidia-smi
1. After launching the job, use `squeue -u hdai` to check the running status. 
```
JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
6235797 delacy-gp haocheng u1265496  R    2:55:49      1 notch330
```
2. Run `ssh $NODELIST` though the node, here the $NODELIST=notch330
3. Run `nvidia-smi`