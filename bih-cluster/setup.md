# Setup

## Before start

Suppose you already have access to BIH cluster, read the [BIH HPC Docs](https://docs.hpc.bihealth.org/) and tried to log into the cluster successfully.

To be able to run applications with graphic user interface on the cluster, check in your terminal if `echo $DISPLAY` returns empty. If so, add this line `export DISPLAY=:0` to the end of your shell rc file (`.bashrc` or `.zshrc` depending on which one you use).

For macOS, run `brew install xquartz` in your terminal to enable X11 forwarding.

## Log into the cluster

`ssh -Y YOUR_CHARITE_USERNAME_c@hpc-login-1.cubi.bihealth.org`

## Log into a compute node

`srun -I60 --pty --cpus-per-task=8 --mem=32G --part=medium --time=1-0 bash`&#x20;

**Everything below should be done in a compute node.**

## Create folders and soft links

```
ln -sfn /fast/work/groups/ag_horn group

mkdir -p $HOME/work/home/.cache
mkdir -p $HOME/work/home/.ccache
mkdir -p $HOME/work/home/.conda
mkdir -p $HOME/work/home/.config
mkdir -p $HOME/work/home/.local
mkdir -p $HOME/work/home/.singularity

ln -sfn $(realpath $HOME/work/home/.cache) $HOME/.cache
ln -sfn $(realpath $HOME/work/home/.ccache) $HOME/.ccache
ln -sfn $(realpath $HOME/work/home/.conda) $HOME/.conda
ln -sfn $(realpath $HOME/work/home/.config) $HOME/.config
ln -sfn $(realpath $HOME/work/home/.local) $HOME/.local
ln -sfn $(realpath $HOME/work/home/.singularity) $HOME/.singularity
```

## Copy preset files

<pre><code><strong>cp -rT $HOME/group/setup/config $HOME</strong></code></pre>

Things included:

* `.bash_profile`, `.bashrc`, `.zshrc`
* `.tmux.conf`
* `.condarc`
* `ys-cluster.zsh-theme`
* `startup.m` (MATLAB startup script)

## Setup Mambaforge

```
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh"
sh Mambaforge-Linux-x86_64.sh -b -p $HOME/work/mambaforge
rm Mambaforge-Linux-x86_64.sh
```

## Install and configure zsh and .oh-my-zsh

```
mamba install zsh -y
ZSH="$HOME/work/home/.oh-my-zsh" sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
mv $HOME/.zshrc.pre-oh-my-zsh $HOME/.zshrc
mv $HOME/ys-cluster.zsh-theme $HOME/work/home/.oh-my-zsh/custom/themes/
```

## Initialize conda for bash and zsh

```
conda init bash zsh
```

## Now open another terminal and try to log into the cluster

`ssh -Y YOUR_CHARITE_USERNAME_c@hpc-login-1.cubi.bihealth.org`

If you see error during login, fix it in the terminal in which you already logged into the cluster.

If everything works, you should see that you are using `zsh` now. From now on, you can log into a compute node and start a interactive session using:

* `srun -I60 --pty --cpus-per-task=8 --mem=32G --part=medium --time=1-0 --nodelist=hpc-cpu-50 zsh`&#x20;

where `--cpus-per-task`, `--mem` and `--nodelist` are optional parameters. Check out [BIH HPC Docs](https://docs.hpc.bihealth.org/slurm/quickstart/) for details.

You can also check out the [BIH HPC Docs](https://docs.hpc.bihealth.org/how-to/connect/gpu-nodes/) on how to use GPU nodes (for example, run CUDA version of `eddy` from `FSL`). `eddy` available in `$FSLDIR/bin` uses CUDA 11 by default. OpenMPI version is also available via `eddy_openmp`.

## Copy MATLAB Singularity image

```
mkdir -p $HOME/work/container
cp $HOME/group/setup/container/matlab-ossdbs.sif $HOME/work/container
```

## Set up Lead-DBS

```
getspm -P $HOME/work/MATLAB/toolbox
unzip $HOME/work/MATLAB/toolbox/spm12.zip
unzip -d $HOME/work/MATLAB/toolbox $HOME/work/MATLAB/toolbox/spm12.zip
rm $HOME/work/MATLAB/toolbox/spm12.zip
git clone https://github.com/netstim/leaddbs.git $HOME/work/MATLAB/toolbox/leaddbs
git -C $HOME/work/MATLAB/toolbox/leaddbs checkout classic
cp -r $HOME/group/setup/lead_data/* $HOME/work/MATLAB/toolbox/leaddbs
```

## Use MATLAB

Log into a compute node with X11 forwarding enabled

`actmatlab` # This activate MATLAB on the compute node

`runmatlab` # This starts MATLAB without GUI

`runmatlabx` # This starts MATLAB with GUI

After you start LeadDBS, edit the preference file from the menu and set the two keys below:

`prefs.lc.datadir = [ea_gethome, 'group', filesep, 'connectomes', filesep];`

`prefs.env.dev = 1;`
