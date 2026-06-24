---
title: "Discworld Field Guide"
layout: single
classes: wide
author: keiran_rowell
toc: false
sidebar:
  - title: "Discworld Field Guide"
    nav: "field-guide-nav"
---

### The Gates 🚪
{: data-toc="🚪 Login"}
There are two ways to pass through the gates of your laptop on Discworld:

1. **Through a webportal** 
2. **Via the command line**

> 🔓You **must** be on campus or behind the [UNSW VPN](https://www.unsw.edu.au/myit/services/wifi-network/vpn) 🦁🔒 to access any of these services
{: .notice--warning}

These ways of accessing the GPUs serve different purposes: 
 
1. Provides convenience and a visual multi-program interface during an interactive session. But, by its very nature is less flexible (some programs aren’t supported, many don’t even have an interface).

2. Involves some learning and involves installing a suitable terminal on your laptop, but is *far* more flexible and opens up the possibility of more powerful calculations, ‘set-and-forget’ longer running jobs, and more efficient jobs queuing.

To access the webportal, go to [portal.discworld.analytical.unsw.edu.au](http://portal.discworld.analytical.unsw.edu.au)

**To login to Discworld** through the terminal:

🍏 MacOS: Start the `Terminal` app

🪟 Windows: Install the “Windows Subsystem of Linux” (`WSL2`). If new, try [Ubuntu](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=en-GB&gl=AU) 🟠

> UNSW Research Technology Services has a guide [here](https://docs.restech.unsw.edu.au/using_katana/accessing_katana/#connecting-to-katana-via-terminal).
{: .notice--info}

🐧 Linux: this will have an inbuilt terminal. Use your favourite.

**Login into a command-line** shell securely (`ssh`):

- **Passwords:** Access _via_ zID and zPass. _You do not set a new password_ 
    
🗝️ In a Discworld new user onboarding session, we will set you up with a securely encrypted key access per device; the same public-private key access that protects the internet servers every day. The world is moving away through passwords, like [passkeys](https://safety.google/authentication/passkey/) are now replacing password fields in web logins.
<br> We would highly prefer you use secure device-to-device key.  
{: .notice--info}
 
- `ssh <zID>@discworld.analytical.unsw.edu.au` and you’ve opened the door to Discworld, we gave you the key during on-boarding 🗝️

---

### `Command` masher ⌨️
{: data-toc="⌨️  `command` reference"}

One thing that makes Linux systems *seem* hard to work with is your possible commands are invisible. You’re given a black mirror without the buttons to show the things you normally want to do.

Luckily, Linux people old and new recognise this & have compiled lists of common things to do.

For example: <https://www.geeksforgeeks.org/linux-unix/basic-linux-commands/>

> **Please think before you type**. If you’re new, familiarise yourself with the common commands below before branching out to more advanced use.  
>   
> These allow us to keep the cluster nimble and flexible while also providing ‘easier’ commands for common software use.
{: .notice--danger}

The first hurdle is learning to work with your files *without clicking on them.* Feels weird at first, but you’ll generate thousands of files in CryoEM so it will absolutely save you time.  
  
Basic navigation and file movement commands are: `ls`, `pwd`, `mkdir`, `cd`, `cp`, `mv`, `rm`, `grep`

> `rm` is DANGEROUS. It is a COMPLETE DELETION. We have confirmation on for your safety, but don’t get used to it, other systems will *immediately* execute `rm` and the file will be gone.
{: .notice--danger}
> We provide a `saferm` that will ask for confirmation, if you're a beginner 
{: .notice--success}

If those seem to be missing letters, that’s because they *are*. You’ll end up typing so often you don’t want to spell out `list ./my_data` or `print-working-directory` over & over again. 

---
#### Discworld shortcuts
📂 Folders are called `directories` in Linux land  
🧭 `paths` are as `/full/path/to/file` the slashes `/` go down folders, like in your file browser. <br>There are some shorthands: `.`=‘here’, `./`=‘here folder’, `../`=‘folder above’, `~`='home folder'<br>
🏠 `cd /home` = `cd ~`; takes you home quickly<br>
↩️ `cd -` will take you back to the last folder you were in<br>
⬆️ Up arrow (`↑`) goes back through your shell commands<br>
📍 `whereami` prints the working directory (the one your command line prompt is in) <br>
❔ `which` tells you where a `program` is located. You can then tell the other programs

`which` is useful after loading a program. _e.g._ `module load sbgrid/relion`   `which relion`
{: .notice--info}

⏪ `Cntrl + r` starts a ‘reverse search’; lets you search for old commands by a particular word<br>
🚫 `Cntrl + c` cancels whatever action you were doing<br>
👋 `exit` (or `quit`) will get your out of most programs, including logout from Discworld<br>

📃 `list -al` will give you *all* files, including the ones hidden by the magic `.` in front<br> 
It *also* shows `permissions`: who can `read`, `write` (hence overwrite/<span style="color: #FF0E0E;">delete</span>), run/`execute` files

<code><span style="color: #A3BE8C;">r</span><span style="color: #D08770;">w</span><span style="color: #EBCB8B;">x</span><span style="color: #8FBCBB;">r</span><span style="color: #BF616A;">w</span><span style="color: #B48EAD;">x</span><span style="color: #5E81AC;">r</span><span style="color: #81A1C1;">w</span><span style="color: #88C0D0;">x</span> size username date filename</code>
<br>&nbsp;&nbsp;`u` `g` `o`

Be very careful who you share write access with
{: .notice--danger} 

In the above <span style="color: #A3BE8C;">read</span>/<span style="color: #D08770;">write</span>/<span style="color: #EBCB8B;">execute</span> letters are grouped first-to-last by `user`, `group` and `other`
- `group` will typically your lab group, but can be made from any collection of `users`
- `other` is _anyone_ else on Discworld!
- `chmod` – change (file) mode. Another `ch` command; to change file `permissions` 
- `chmod` works on the corresponding to the letters listed on the left `chmod g-r file` will remove the ability for anyone in the `group` to read the file.<br>

Use `chmod+` to add permisions, `chmod-` to remove, `chmod=` to set
{: .notice--info}

🕐 `list -snew` will sort your files by the newest ones accessed<br>
🃏 `*` is the ‘wildcard’ and will fill in the slots letters should be:<br> 

`cryo*` matches `cryosparc`, `cryoEM`, `cryo-EM`, `cryotomo`, `cryogenic_hibernation_capsule`, and so on. 
{: .notice--info}

`*` is handy, but be careful.
{: .notice--warning}

📦 `disk-use` shows you the ‘disk usage’ of a folder – that is, where all the file storage is going<br>
🔎 `search` will help you locate where a particular file is, just give it the 📁 directory to search<br>
📑 `search-word` will look for a word (or a string of letters) inside the list of files given to it<br>

---

🐈(👁️) `cat` (also linked as `show`) is used to show a file on the terminal: `cat file`. 

It’s because you can con**cat**enate two files together with it `cat file1 file2 > file3`
{: .notice--success}

🐧 Linux land is full of brief historical puns.
{: .notice--info}
🔚 `tail --follow` live view of the bottom of a file.<br> Very useful for `slurm-<jobID>.out` log progress<br>
✘✓ `find-replace` is done by `sd` (newer `sed`), in modifies the file ‘live’<br> `sd old_word new_word file.txt`<br>

Be sure to save a copy before running a ‘find-replace’, *e.g.* with `cp file file.bak`
{: .notice--warning}

↩️  `extract` unpacks all sorts of compressed files<br> 
↪️  `compress` creates a the standard Linux compressed file format (`.tar.gz`)<br>
↔️ `difference` finds the different *lines* between two files (*i.e.* what changed?)<br>
🔺 `delta` compare two files on a *character* level. This was done with an `--option` to your `~/.zshrc`<br>
✂️ `cut` & `paste` are useful to work segments of files. **Be sure to back up**<br>
 𝄜 If handling complex tablulated data, try using `DataFrames` in your language of choice<br>

🎨 we’ve used colours to make common file types easier to see

 run `unset EXA_COLORS` to remove the colours
{: .notice--warning}

---

Even more helpfully, you can read what the commands do while in the command line.

> **Too long; didn’t read** 📃
{: .notice--success}

We have installed ‘too long didn’t read' manuals. `tldr command` will provide one line on what the command does and use examples. If you want a complete manual of a command it’s `man command`.

> 🥱 **_Please_ don't ‘tl;dr’ this guide, or the manual pages** 
> The manual pages examples will often tell you what you need for simple uses without having to wait for an admin to become free.
{: .notice--danger}

> Most command line tools you can also add `--help` after them to see what they do.
{: .notice--info}

---

#### Basic command line (`zsh`) shell improvements.

We’ve moved to a modern user-friendly shell by default. This gives you colours, autocomplete et*c.* For command shell scripts from elsewhere you probably need to run `bash script.sh`  
We’ve but `hello_discworld.sh` in your `/home`, you’ll see it specifies at the top that it uses `bash` to run the script. Have a try with `bash hello_discworld.sh` since it’s tiny. Please queue big `program`s.  
If you really don’t like `zsh` you can ask us to change your default shell with `chsh` ('change shell')

> 🦀 We’ve swapped some classic `commands` for new ones. For example `du` ('disk usage') secretly runs the `dust` ('disk usage [programmed in rust]') implementation through `aliases`.  
> We think these are nicer and faster, but if you want to change any of these substitutions, feel free to edit your personal aliases <https://www.howtogeek.com/439736/how-to-create-aliases-and-shell-functions-on-linux/>
{: .notice--success}

> 📝 Writing to files is common task. Use the `edit <file>` command. `edit` is secretly [micro](https://github.com/zyedidia/micro)
{: .notice--info}

`cp file file.bak` is a quick way to create a second copy of a small non-critical file. Anything more important should go through a proper back-up process.  
  
What’s nice is you can easily share scripts from others and you own, check out:   
`python fasta_fixed-width_to_single-line.py --help`  
It uses the powerful international [BioPython](https://biopython.org/) module that understands biological files in a clean way.

---

#### Discworld standard `s`cheduler and custom ‘helper’ commands

Since all our users are doing CryoEM work, our admin team have set up some automated scripts that can be called as if they were out-of-the box shell commands. Standard scheduler commands remain

- `sdesktop` --- start a visual desktop backed by cluster resources
- `sdraft [job_name]` --- custom Discworld script; directly edits a **batch job** template
   
Batch job files are just `shell` `commands` with info for resources at the top.<br> We can call them `[job_name].slurm` to keep track
{: .notice--info}

- `sbatch` --- send a job file to the cluster to run in the background
- `sinteractive [resources]` --- request an interactive shell with resources 
- `scancel` --- cancel a job based on its `JOBID` 

`JOBID` is a number not a name, so its easier for the schedule track
{: .notice--info}

- `sacct` --- print accounting for you jobs' resource usage
- `squeue` - see the state of your job in the queue. 

See [STATE CODES](https://slurm.schedmd.com/job_state_codes.html), `R` is running `PD` pending 👍
{: .notice--info}

- `sinfo` - get information about the status of the cluster
- `scontrol [action] [job_ID]`- advance control over what a submitted job should do

---

### Requesting resources 🫲
{: data-toc="⏱️ Job scheduling"}

> 🤖 Just ask for what you need, with a bit of overhead so your job won’t run out of time or RAM
{: .notice--warning}

Put the resources you need as `--flags` after `sinteractive`

|  **Resource**                                                                                                                                                                                                 |  **Meaning**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--job-name="descriptive-name"` | Purely for your records                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `-time=1:30:30`                 | Time duration you hold resources (`hr:min:sec`)                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `--mem=20GB`                    | Your RAM. That is, the memory needed to keep the program running. You just have to measure the consumption in a test job to avoid your program crashing.                                                                                                                                                                                                                                                                                                                                           |
| `--cpus-per-task=4`             | How many central processing units to assign per instance of the program you are running                                                                                                                                                                                                                                                                                                                                                                                                            |
| `--gres=gpu:<model>:1`          | Since GPUs are expensive, you need to ask for the number in your generic resource. `<model>` is optional; if you know if you need a big one or a small one you can specify here.  Otherwise `--gres=gpu:<num_gpus>` is fine.                                                                                                                                                                                                                                                                       |
| `--array=<indexes>`<br>  `--array=0-N`<br>  `--array=0,5,20-25`<br>  `--array=0-25:5`<br>  `--array=0-25%5` | 🪄 Advanced users may set up many *many* jobs differing by one parameter. Arrays excel here.<br> Run subjobs number `0➔`_N_<br> Run jobs number `0, 5, 20→25`<br> Run jobs with step size `:5`, _i.e_ `0, 5, 10, 15, 20, 25..`<br> Run jobs `0→25`, but only run maximum 5-at-at time, to avoid overwhelming the queue<br> Please read the [SLURM Array manual page](https://slurm.schedmd.com/job_array.html) |

---

### Data at the door 🗂️
{: data-toc="🗂️ Data management"}

> **Do not pull your CryoEM particle data down to your /home drive**. The cluster already knows how to access the data and handles transfers, you just occasionally need to tell it where it go looking.   
>   
> The EMU manages the raw data from the instruments and is classified (*see below*) and stored on the central university’s storage solution.
{: .notice--danger}

- **Raw data** - This is generated from the instruments at the Electron Microscopy Unit. They handle permissions and backup of the raw data
- **Processing data** - This lives on the university’s ‘Elastic Storage Solution’. It doesn’t live on Discworld (it’s in a different room) so it needs to be *mounted* (like a USB) by giving the programs this file path structure to your data:  
   `/data/ESS/<cryo instrument>/<lab head lastname>/<user_zID>/(raw|live|processing)`
- **Program data** - This is in a *pooled* `/home` drive, which through filesystem magic lives in a network of shared, expensive flash drives. As such it’s suitable for programs install and working environments (`conda` should resolve quickly). It is not suitable for CryoEM data
- **Finalised 3D maps** – these should be deposited in the appropriate scientific database (*e.g.* [EMPIAR](https://www.ebi.ac.uk/empiar/)) and/or deposited to [UNSW’s Research Data Archive](https://www.dataarchive.unsw.edu.au/) ‘glacial’ storage. The Data Archive is managed under your supervisor’s [Research Data Management Plan](https://www.dataarchive.unsw.edu.au/help/rdmp-and-data-archive).
- ⁉️ **Unsure?** - Doesn’t fit the above classes? <br>Contact an admin at [sbf+discworld@unsw.edu.au](mailto:sbf+discworld@unsw.edu.au)<br> For hard classification cases talk to [UNSW Research Data Management support team](mailto:RDM@unsw.edu.au)

> 🌐 **Globus [In Development]** - UNSW has a [Globus](https://app.globus.org/) site license. Globus excels at large data transfers, and makes data points discoverable (like EM data connected at another Facility). Please use the Globus portal and all the data sharing permissions it grants you. It has many nifty features.
{: .notice--success}


`rsync` --- when in doubt this is a safe, resumable way to remotely sync data between Linux systems.

---

### 🤕 **--- What to do when things go wrong**
{: data-toc="🤕 Emergencies"}

> 1. **Notice within 2 weeks**
> 2. **DON’T PANIC**
>
> 💾 We save a `snapshot` of your `/home` drive to another storage server every night. That means if you alert us within two weeks we can start the process of ‘rolling-back’ to an old save state. We only keep the last two weeks otherwise the user storage will balloon.
>
> 📜 Recall [The Laws of Discworld](The_Laws_of_Discworld.md) **/home is for your** ***tools*** **not your data**
{: .notice--warning}

---

### GPU Alley👨‍💻🛣️
{: data-toc="🛣️ Job lanes"}

> `SLURM` (Simple Linux Utility for Resource Management) provides a single master queue for a variety of computational work, ensuring a **fair quality of service for everyone**.   
{: .notice--success}

> The `fairshare` algorithm is used. To stop other people’s smaller interactive jobs being entirely delayed, the scheduler naturally brings forward jobs that have been waiting a long time, and schedules really large jobs to start when the resources are less busy (the middle of the night or the weekend).
{: .notice--info}


> **We’ll keep our queue as simple as possible**, as such we can’t write in exceptions to your personal deadlines. Your jobs will still run efficiently, but in the share the queue determines is fairest. Accordingly, plan your work with suitable wait time if you have a deadline in the future
{: .notice--info}

---

### Future improvements 🚧
{: data-toc="🚧 Under construction"}

> Please try to be patient and respectful with our administration and development team. We try to roll out new features to you as fast as we stably can, so require testing time.
{: .notice--warning}

<a href="#" class="btn btn--primary">NOT WORKING</a>

<a href="#" class="btn btn--inverse">PLANNED</a>

<a href="#" class="btn btn--warning">IN TESTING</a>

<a href="#" class="btn btn--info">STABLE</a>

<a href="#" class="btn btn--success">NEW AND WORKING</a>
