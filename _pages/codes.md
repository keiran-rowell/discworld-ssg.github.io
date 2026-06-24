---
permalink: /codes/
title: "The Codes of Discworld"
layout: single
classes: wide
author: keiran_rowell
---


> ℹ️ If you need some code for you science and don’t see it listed here, please discuss with the Discworld systems administration team ([sbf+discworld@unsw.edu.au](mailto:sbf@unsw.edu.au)) and we can see how to install it.  
>   
> If it’s a reasonably straightforward install, please have a go in your own `/home` folder
{: .notice--info}


### Programs at launch

- `CryoSPARC` (through [portal.discworld.analytical.unsw.edu.au](http://cryosparc.analytical.unsw.edu.au))
- Typical Cryo-EM/ET command line interface (CLI) programs
- `Doppio` (portal) / `Relion` (graphical/CLI)

### Software package managers

- SBGrid (all 200+ programs in the `Electron Microscopy` collection, major programs from `Vizualisation & Analysis`)

⚠️  Check `module avail sbgrid` to see if an available tool run, or the error is from the framework used on top of the tool. 
{: .notice--danger} 

-  `Scipion` framework

 📧 email [d.luque@unsw.edu.au](mailto:d.luque@unsw.edu.au) for expertise support, and contact with developers for difficult debugging
 {: .notice--warning}

- `Spack` -- scientific program installer

⚙️ `Spack` provides the potential to install 8559+ total programs, and counting..
{: .notice--info}

### Installing your own software

> Feel free to give new programs a try, you can't break other people's `/home` --- or ask us to install!
{: .notice--success}

If there’s a program you want, walk down the list in order of preference in how to go about it

1.  **Load a system module**: `module avail` to see all available modules, then `module load program` will give you access to the programs important enough to have been installed on the base system.
    
    `module overview` shows you just the `programs` without every version. Much shorter.
    {: .notice--info}

    This includes programming tools like `CUDA`, programming languages `python`, `R`, _etc._ 
 
2.  **Check** `sbgrid`:  
    
     **Check** `sbgrid`
    {: .notice--warning}
 
    `module load sbgrid/program/version`  
    `sbgrid` is an amazing collaborative Structural Biology Grid consortium. We install all 200+ programs in the `Electron Microscopy` collection. These installs usually live under   
       `/apps/sbgrid/<program>/<version_number>/bin/<program>` `bin` because computers use `bin`ary. SBGrid has good guides on [how to switch software versions](https://sbgrid.org/wiki/versions) and even provides [examples on running some programs](https://sbgrid.org/wiki/examples) *via* SBGrid.  
3. **Check** `scipion`: if you connect with `ssh -Y` you can launch the Scipion visual interface to click install a set of CryoEM programs, worth checking as what’s packaged may be different.
4. **Have a go installing it yourself**: This is what your `/home` is for.
   1. In open science code, most is **stored on GitHub**. GitHub has many commands for software developers. Don’t worry about these, you just need a local clone of the raw code inside `/home`. To get it locally run: `git clone` [`online-code-location`](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).   
      For example: `git clone https://github.com/ml-struct-bio/cryodrgn.git` ❄️ 🐉   
      However, the `Installation` section actually recommends using a package manger

      ```java
      # Create and activate conda environment
      (base) $ conda create --name cryodrgn python=3.12
      (cryodrgn) $ conda activate cryodrgn

      # install cryodrgn
      (cryodrgn) $ pip install cryodrgn
      ```
   2. We are going to let **you use the module system**. `spack install program`. Spack is a [cool way to share code install recipes](https://spack.readthedocs.io/en/latest/features.html) at every supercomputer around the world.
5. **Follow the README** this list the invocations to install the program if you’re luckily enough for it to ‘just work’. Central UNSW Research Technology Services [already have a guide on installation](https://docs.restech.unsw.edu.au/software/installing_software/).
6. **Reach out**: For tricky installs, if you’re unsure of the code, or the going gets rough, drop us a line.

{: .notice--warning}
> Please contact **Dr Daniel Luque** for expertise in the use of Scipion
