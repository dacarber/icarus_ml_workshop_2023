# ICARUS ML Reconstruction Workshop

This repository is for a workshop organized by the ICARUS ML reconstruction group to train new comers to learn about our machine-learning-based data reconstruction chain. You can find the workshop agenda [here](https://indico.slac.stanford.edu/event/7979/).

## Software environment

For the workshop, we will use [this "Docker container"](https://hub.docker.com/layers/deeplearnphysics/larcv2/ub20.04-cuda11.6-pytorch1.13-larndsim/images/sha256-afe799e39e2000949f3f247ab73fe70039fb411cb301cb3c78678b68c22e37fb?context=explore).

Some notes below:

* The image is fairly large (multiple GBs). Please download in advance if you are using it locally. It is shared in both NVIDIA GPU and CPU running mode of our software.
* Supported GPUs include those with NVIDIA Volta (e.g. V100), Turing (e.g. RTX 2080Ti), and Ampare architectures (e.g. A100, RTX 3080). If you do want an older architectures to be supported, such as Pascal, please [contact Kazu](mailto:kterao@slac.stanford.edu).
* We assume basic knowledge about _software container_, in particular `Docker`. If you are learning for the first time, we recommend to use/learn about `Singularity` ([website](https://singularity.hpcng.org/)) instead of `Docker`.
    * You can pull a singularity image as follows
```shell
$ singularity pull docker://deeplearnphysics/larcv2:ub20.04-cuda11.6-pytorch1.13-larndsim
```

You can now launch a shell inside the singularity with
```shell
$ singularity exec --bind /path/to/workshop/folder/ larcv2_ub20.04-cuda11.6-pytorch1.13-larndsim.sif bash
```

### Docker alternative

You can also pull the docker image using docker (easier on Mac and Windows) directly with:
```shell
$ docker pull deeplearnphysics/larcv2:ub20.04-cuda11.6-pytorch1.13-larndsim
```
To see which images are present on your system, you can use docker images. It will look something like this:
```shell
$ docker images
REPOSITORY                TAG                                     IMAGE ID       CREATED        SIZE
deeplearnphysics/larcv2   ub20.04-cuda11.6-pytorch1.13-larndsim   cd28cb3cd04b   2 months ago   20.8GB
```
to run a shell in your image, simply do:
```shell
$ docker run -i -t cd28cb3cd04b bash
```

If you have apple silicon in your laptop, you're out of luck for now...

* [Ask Francois](mailto:drielsma@slac.stanford.edu) for questions or a request for a separate tutorial if interested.

## Resources

1. The *configuration files* are packages with this repository.

2. You can find *data files* for the examples used in this workshop under:
- SDF
```shell
/sdf/group/neutrino/icarus/workshop2023/larcv/ # Example MPV/MPR file prior to reconstruction
/sdf/group/neutrino/icarus/workshop2023/reco/  # Reconstructed HDF5 files
```
- S3DF
```shell
/sdf/data/neutrino/icarus/workshop2023/larcv/ # Example MPV/MPR file prior to reconstruction
/sdf/data/neutrino/icarus/workshop2023/reco/  # Reconstructed HDF5 files
```
- Public
  - [MPVMPR LArCV file](https://drive.google.com/file/d/1nP-fCq3e59rOePfDvECRsxoToUT03QLj/view?usp=sharing) (Day 1)
  - [MPVMPR HDF5 file](https://drive.google.com/file/d/1mlklhMtPVF39BJp51er6AP8uGypBO8MI/view?usp=sharing) (Day 2, 3)
  - [BNB numu + cosmics](https://drive.google.com/file/d/1dbOq9ViuOGmLyTvoMuEkUtNn3nA1TWGo/view?usp=sharing) (Day 4, 5)
  - [BNB intime cosmics](https://drive.google.com/file/d/1qBDUmCPjSsNi_SW6L6tWduPSFcBQaTMW/view?usp=sharing)
  - [High statistics CSV files](https://drive.google.com/drive/folders/1inRAzgCXSHEW-WAE1M25UTot_j7qioaO?usp=sharing)

3. The *network model parameters* for the inference tutorial can be found at:
- SDF/S3DF (same path)
```shell
/sdf/group/neutrino/drielsma/train/icarus/localized/full_chain/weights/full_chain/grappa_inter_nomlp/snapshot-2999.ckpt
```
- Public
  - [snapshot-2999.ckpt](https://drive.google.com/file/d/1jKcNHWSk-MgyRM7fqQF8Tsgb5VCadKbR/view?usp=sharing)

## Computing resource
Most of the notebooks can be ran strictly on CPU with the exception of:
- Training/validation notebook
- Inference and HDF5 file making notebook

For all other notebooks, you can run them locally, provided that you download:
- Singularity container
- Necessary data
- [lartpc_mlreco3d v2.8.6](https://github.com/DeepLearnPhysics/lartpc_mlreco3d/releases/tag/v2.8.5)

To gain access to GPUs:
- Everyone participating in this workshop should have access to both SDF and S3DF, if you do not, please reach out to [Francois](mailto:drielsma@slac.stanford.edu).
  - SDF Jupyter ondemand: https://sdf.slac.stanford.edu/public/doc/#/
  - S3DF Jupyter ondemand: https://s3df.slac.stanford.edu/public/doc/#/

* ICARUS collaborators also have an access to Wilson Cluster at FNAL, equipped with GPUs. Below is a few commands to log-in and load `Singularity` with which you can run a container image for the workshop (see the next section). For how-to utilize the Wilson Cluster, refer to [their website](https://computing.fnal.gov/wilsoncluster/slurm-job-scheduler/) as well as [this](https://cdcvs.fnal.gov/redmine/projects/nova_reconstruction/wiki/The_Wilson_Cluster) and [that](https://cdcvs.fnal.gov/redmine/projects/nova_reconstruction/wiki/Step-by-step_guide_to_running_on_the_WC) documentation from NOvA (replace "nova" with "icarus" and most commands should just work).

```shell
$ ssh $USER@wc.fnal.gov
$ module load singularity
$ singularity --version
singularity version 3.6.4
```
