![DEDO  - Dynamic Environments with Deformable Objects](misc/imgs/header.jpg)
### DEDO  - Dynamic Environments with Deformable Objects
DEDO is a lightweight and customizable suite of environments with
deformable objects. It is aimed for researchers in the machine learning, 
reinforcement learning, robotics and computer vision communities.
The suite provides a set of every day tasks that involve deformables, 
such as hanging cloth, dressing a person, and buttoning buttons. 
We have provided examples for integrating two popular 
reinforcement learning libraries: [StableBaselines3](https://github.com/DLR-RM/stable-baselines3) and [RLlib](https://docs.ray.io/en/latest/rllib.html).
We also provided reference implementaionts for training a various 
Variational Autoencoder variants with our environment. 
Dedo is easy to set up and has few dependencies, it is
highly parallelizable and supports a wide range of customizations: 
loading custom objects, adjusting texture and material properties. 

**Table of Contents:**<br />
[Installation](#install)<br />
[GettingStarted](#examples)<br />
[Tasks](#tasks)<br />
[Use with RL](#rl)<br />
[Use with VAE](#svae)<br />
[Customization](#custom)<br />

Please refer to **[Wiki for the full documentation ](../../wiki)**

<a name="install"></a>
## Installation

_Optional initial step_:  create a new conda environment with
`conda create --name dedo python=3.7` and activate it with
`conda activate dedo`. 
Conda is not strictly needed, alternatives like virtualenv can be used;
a direct install without using virtual environments is ok as well.



```
git clone https://github.com/contactrika/dedo
cd dedo
pip install numpy  # important: Nessasary for compiling numpy-enabled PyBullet
pip install -e .
```
Python3.7 is recommended as we have encountered that on some OS + CPU combo, PyBullet could not be compiled with Numpy enabled in Pip Python 3.8.
To enable recording/logging videos install ffmpeg:
```
sudo apt-get install ffmpeg
```
See more in **[Installation Guide in wiki](../../wiki/Installation)**
<a name="examples"></a>
## Getting started
To get started, one can run one of the following commands to visualize the tasks through a hard-coded policy. 

```
python -m dedo.demo --env=HangBag-v1 --viz --debug
```

* `dedo.demo` is the demo module
* `--env=HangGarment-v1` specifies the environment
* `--viz` enables the GUI
* `---debug` outputs additional information in the console
* `--cam_resolution 400` specifies the size of the output window


See more in **[Usage-guide](../../wiki/Usage-guide)**


![misc/imgs/hang_task_ui.jpg](misc/gifs/HangBag-v1_0.gif)


## Tasks
See more in **[Task Overview](../../wiki/Tasks-Overview)**

We provide a set of 10 tasks involving deformable objects, most tasks contains 5 handmade deformable objects. 
There are also two procedurally generated tasks, `ButtonProc` and `HangProcCloth`, in which the deformable objects are procedurally generated. 
Furthermore, to improve generalzation, the `v0` of each task will randomizes textures and meshes.

All tasks have `-v1` and `-v2` with a particular choice of meshes and textures
that is not randomized. Most tasks have versions up to `-v5` with additional
mesh and texture variations.

Tasks with procedurally generated cloth (`ButtonProc` and `HangProcCloth`)
generate random cloth objects for all versions (but randomize textures only
in `v0`).

### HangBag
![misc/gifs/HangGarment-v1.gif](misc/gifs/HangBag-v1_0.gif)
```
python -m dedo.demo_preset --env=HangBag-v1 --viz
```
`HangBag-v0`: selects one of 108 bag meshes; randomized textures

`HangBag-v[1-3]`: three bag versions with textures shown below:

![misc/imgs/hang_bags_annotated.jpg](misc/imgs/hang_bags_annotated.jpg)


### HangGarment
![misc/gifs/HangGarment-v1.gif](misc/gifs/HangGarment-v1_0.gif)
```
python -m dedo.demo_preset --env=HangGarment-v1 --viz
```
`HangGarment-v0`: hang garment with randomized textures 
(a few examples below):

![misc/gifs/HangGarment-v1.gif](misc/gifs/HangGarment-v1_0.gif)

`HangGarment-v[1-5]`: 5 apron meshes and texture combos shown below:

![misc/imgs/hang_garments_5.jpg](misc/imgs/hang_garments_5.jpg)


`HangGarment-v[6-10]`: 5 shirt meshes and texture combos shown below:

![misc/imgs/hang_shirts_5.jpg](misc/imgs/hang_shirts_5.jpg)


### HangProcCloth
![misc/gifs/HangGarment-v1.gif](misc/gifs/HangProcCloth-v1_0.gif)
```
python -m dedo.demo_preset --env=HangProcCloth-v1 --viz
```
`HangProcCloth-v0`: random textures, 
procedurally generated cloth with 1 and 2 holes.

`HangProcCloth-v[1-2]`: same, but with either 1 or 2 holes

![misc/imgs/hang_proc_cloth.jpg](misc/imgs/hang_proc_cloth.jpg)

### Buttoning
![misc/gifs/HangGarment-v1.gif](misc/gifs/Button-v1_0.gif)
```
python -m dedo.demo_preset --env=Button-v1 --viz
```
`ButtonProc-v0`: randomized textures and procedurally generated cloth with 
2 holes, randomized hole/button positions.

`ButtonProc-v[1-2]`: procedurally generated cloth, 1 or two holes.

![misc/imgs/button_proc.jpg](misc/imgs/button_proc.jpg)

`Button-v0`: randomized textures, but fixed cloth and button positions.

`Button-v1`:  fixed cloth and button positions with one texture 
(see image below):

![misc/imgs/button.jpg](misc/imgs/button.jpg)


### Hoop
![misc/gifs/HangGarment-v1.gif](misc/gifs/Hoop-v1_0.gif)
```
python -m dedo.demo_preset --env=Hoop-v1 --viz
```
`Hoop-v0`: randomized textures
`Hoop-v1`: pre-selected textures
![misc/imgs/hoop_and_lasso.jpg](misc/imgs/hoop_and_lasso.jpg)
### Lasso
![misc/gifs/HangGarment-v1.gif](misc/gifs/Lasso-v1_0.gif)
```
python -m dedo.demo_preset --env=Lasso-v1 --viz
```
`Lasso-v0`: randomized textures
`Lasso-v1`: pre-selected textures




### DressBag
![misc/gifs/HangGarment-v1.gif](misc/gifs/DressBag-v1_0.gif)
```
python -m dedo.demo_preset --env=DressBag-v1 --viz
```
`DressBag-v0`, `DressBag-v[1-5]`: demo for `-v1` shown below

![misc/imgs/dress_bag.jpg](misc/imgs/dress_bag.jpg)

Visualizations of the 5 backpack mesh and texture variants for `DressBag-v[1-5]`:

![misc/imgs/backpack_meshes.jpg](misc/imgs/backpack_meshes.jpg)
### DressGarment
![misc/gifs/HangGarment-v1.gif](misc/gifs/DressGarment-v1_0.gif)
```
python -m dedo.demo_preset --env=DressGarment-v1 --viz
```
`DressGarment-v0`, `DressGarment-v[1-5]`: demo for `-v1` shown below

![misc/imgs/dress_garment.jpg](misc/imgs/dress_garment.jpg)

### Mask
![misc/gifs/HangGarment-v1.gif](misc/gifs/Mask-v1_0.gif)
```
python -m dedo.demo_preset --env=Mask-v1 --viz
```

`Mask-v0`, `Mask-v[1-5]`: a few texture variants shown below:

![misc/imgs/mask_0.jpg](misc/imgs/mask_0.jpg)

<a name="rl"></a>
## RL Examples

`dedo/run_rl_sb3.py` gives an example of how to train an RL
algorithm from Stable Baselines 3:

```
python -m dedo.run_rl_sb3 --env=HangGarment-v0 \
    --logdir=/tmp/dedo --num_play_runs=3 --viz --debug
```

`dedo/run_rllib.py` gives an example of how to train an RL
algorithm using RLLib:

```
python -m dedo.run_rllib --env=HangGarment-v0 \
    --logdir=/tmp/dedo --num_play_runs=3 --viz --debug
```

For documentation, please refer to [Arguments Reference](../../wiki/Arguments-Reference) page in wiki

To launch the Tensorboard:
```
tensorboard --logdir=/tmp/dedo --bind_all --port 6006 \
  --samples_per_plugin images=1000
```
<a name="svae"></a>
## SVAE Examples

`dedo/run_svae.py` gives an example of how to train various flavors of VAE:

```
python -m dedo.run_rl_sb3 --env=HangGarment-v0 \
    --logdir=/tmp/dedo --num_play_runs=3 --viz --debug
```

`dedo/run_rllib.py` gives an example of how to train an RL
algorithm from Stable Baselines 3:

```
python -m dedo.run_rl_sb3 --env=HangGarment-v0 \
    --logdir=/tmp/dedo --num_play_runs=3 --viz --debug
```

To launch the Tensorboard:
```
tensorboard --logdir=/tmp/dedo --bind_all --port 6006 \
  --samples_per_plugin images=1000
```




<a name="custom"></a>
## Customization

To load custom object you would first have to fill an entry in `DEFORM_INFO` in 
`task_info.py`. The key should the the `.obj` file path relative to `data/`:

```
DEFORM_INFO = {
...
    # An example of info for a custom item.
    'bags/custom.obj': {
        'deform_init_pos': [0, 0.47, 0.47],
        'deform_init_ori': [np.pi/2, 0, 0],
        'deform_scale': 0.1,
        'deform_elastic_stiffness': 1.0,
        'deform_bending_stiffness': 1.0,
        'deform_true_loop_vertices': [
            [0, 1, 2, 3]  # placeholder, since we don't know the true loops
        ]
    },
```

Then you can use `--override_deform_obj` flag:

```
python -m dedo.demo --env=HangBag-v0 --cam_resolution 200 --viz --debug \
    --override_deform_obj bags/custom.obj
```


For items not in `DEFORM_DICT` you will need to specify sensible defaults,
for example:

```
python -m dedo.demo --env=HangGarment-v0 --viz --debug \
  --override_deform_obj=generated_cloth/generated_cloth.obj \
  --deform_init_pos 0.02 0.41 0.63 --deform_init_ori 0 0 1.5708
```

Example of scaling up the custom mesh objects:
```
python -m dedo.demo --env=HangGarment-v0 --viz --debug \
   --override_deform_obj=generated_cloth/generated_cloth.obj \
   --deform_init_pos 0.02 0.41 0.55 --deform_init_ori 0 0 1.5708 \
   --deform_scale 2.0 --anchor_init_pos -0.10 0.40 0.70 \
   --other_anchor_init_pos 0.10 0.40 0.70
```
See more in **[Customization Wiki](../../wiki/Customization)**

## Addtional Asset
`BGarment` dataset comes from [Berkeley Garment Library](http://graphics.berkeley.edu/resources/GarmentLibrary/)
