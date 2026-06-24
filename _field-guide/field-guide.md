---
permalink: /field-guide/
title: "Discworld Field Guide"
layout: single
sidebar: nav
classes: wide
---

> [!IMPORTANT]
> **What to expect from the pilot:** Testing phase will a stable clustered `CryoSPARC` and `Relion`

> [!NOTE]
> For support inquiries email [sbf@unsw.edu.au](mailto:support.discworld@sbf.unsw.edu.au), please read the guide first

> [!NOTE]
> Containers are speculative, and unavailable as we validate deployment issues (security, *etc*)

> [!NOTE]
> We can trial these features because we have a new system, a small number of users entirely focused on CryoEM *processing* in long-term engagements. It does not operate in a way that allow mores general purpose use, or direct `command` or `script` portability to other systems. They serve a different purpose so have different functions and problems to solve.

**Hello from Discworld!** ❄️🔬 → 💻 → 🐢 🌌

> My days here have been as rewarding as they are troublesome, and often confusing. I have been assembling my notes on CryoEM computing for some time now.   
>   
> My intent is to create a guide for anyone whose research path may lead them into high performance computing.   
>   
> There are days I fear my work will only serve to create more confusion about what I've learnt, but I felt it nеcessary to provide in hopеs that these insights may be illuminating for new users.  
>   
> Contained within are `commands`, scripts, data tips, warnings, diagrams and more, all organized in an effort to promote safe travel and computational awareness.  
>   
> While this arrangement highlights the basic chronology of user on-boarding, users could skip to whatever section most directly applies to their impending research deadline, as no two Discworld experiences are the exactly same.  
>   
> Accordingly, certain passages may detail specific programs that you will not encounter. It is still recommended you cover these sections as to increase your general understanding of high performance computing.  
>   
> There will be times when your programs will be tested in ways this guide can neither prepare you for, nor help you from. Discworld travel is not recommended for those without an advisor and allocated time to train. Swift and incomprehensible error messages will follow any decision to breach your container environment (though we keep your `/home` environment safe).  
>   
> With that in mind, I believe the unabridged *Discworld Field Guide* compiled here to be an essential companion for all modern CryoEM data processing research, as well as those potentially seeking more permanent computing knowledge.

Kindest regards, 
*Keiran Rowell*

---

### The Gates 🚪

There are two ways to pass through the gates of your laptop on Discworld:

1. **Through a webportal** 
2. **Via the command line**

> [!NOTE]
> You must be on campus or behind the [UNSW VPN](https://www.unsw.edu.au/myit/services/wifi-network/vpn) to access any of these services

These ways of accessing the GPUs serve different purposes.  
**1.** provides convenience and a visual multi-program interface during an interactive session. But, by its very nature is less flexible (some programs aren’t supported, many don’t even have an interface).

**2.** involves some learning and involves installing a suitable terminal on your laptop, but is *far* more flexible and opens up the possibility of more powerful calculations, ‘set-and-forget’ longer running jobs, and more efficient jobs queuing.

To access the webportal, go to [portal.discworld.analytical.unsw.edu.au](http://portal.discworld.analytical.unsw.edu.au)

**To login to Discworld** through the terminal:

🍏 MacOS: Start the `Terminal` app

🪟 Windows: Install the “Windows Subsystem of Linux” (`WSL2`). If new, try [Ubuntu](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=en-GB&gl=AU) 🟠

> UNSW Research Technology Services has a guide [here](https://docs.restech.unsw.edu.au/using_katana/accessing_katana/#connecting-to-katana-via-terminal).

🐧 Linux: this will have an inbuilt terminal. Use your favourite.

**Login into a command-line** shell securely (`ssh`):

- **Passwords:** You do no set your own passwords. Access via zID will use your university zPass.  
  We would highly prefer you use secure device-to-device key.   
    
  In a Discworld new user session; we will set you up with a securely encrypted key access per device, the same public-private key access that protects the internet servers every day. The world is moving away through passwords, like [passkeys](https://safety.google/authentication/passkey/) are now replacing password fields in web logins.
- `ssh <zID>@discworld.analytical.unsw.edu.au` and you’ve opened the door to Discworld, we gave you the key during on-boarding 🗝️

> [!WARNING]
> **[Future speculative feature, will need a fair amount of development time]** Unlike most clusters (which have to be super efficient and handle anonymous users), we are exploring your login placing you directly in a personal `container`. This means you’re not touching the base cluster system, but in a personal virtual Linux system for each user.
>
> We will trial an unprecedented step of giving you *personal* `sudo` ('super-user do' *i.e. ‘*run-as-admin’). See the `command` guide below. It has great power 🪄 , slow down when using it.  
>   
> 🏗️ Don’t worry, you can try installing Linux packages without breaking the base cluster.
>
> 🏗️ Do worry, you can break your container beyond repair. In that case we’ll have to do administration work to restore your personal container to working order within last fortnight.

Congrats, you now have a high performance “super” computer at your fingertips 💻

---

### `Command` masher ⌨️

One thing that makes Linux systems *seem* hard to work with is your possible commands are invisible. You’re given a black mirror without the buttons to show the things you normally want to do.

Luckily Linux people old and new recognise this and have compiled lists of common things to do.

For example: <https://www.geeksforgeeks.org/linux-unix/basic-linux-commands/>

> [!WARNING]
> **Please think before you type**. If you’re new, familiarise yourself with the common commands below before branching out to more advanced use.  
>   
> These allow us to keep the cluster nimble and flexible while also providing ‘easier’ commands for common software use.

The first hurdle is learning to work with your files *without clicking on them.* Feels weird at first, but you’ll generate thousands of files in CryoEM so it will absolutely save you time.  
  
Basic navigation and file movement commands are: `ls`, `pwd`, `mkdir`, `cd`, `cp`, `mv`, `rm`, `grep`

> [!NOTE]
> `rm` is DANGEROUS. It is a COMPLETE DELETION. We have confirmation on for your safety, but don’t get used to it, other systems will *immediately* execute `rm` and the file will be gone.

If those seem to be missing letters, that’s because they *are*. You’ll end up typing so often you don’t want to spell out `list ./my_data` or `print-working-directory` over & over again. Other shortcuts:

---

📂 Folders are called `directories` in Linux land  
🧭 `paths` are as `/full/path/to/file` or, in shorthand: `.` ‘here’ `./` ‘here folder’, `../` ‘folder above’

![](/wiki/s/-505230918/6452/267b0663176c4f8787189805bf0a33b7c6d3998e/_/images/icons/emoticons/star_blue.png) `/home` = `~` takes you home quickly

⬆️ Up arrow (`↑`) goes back through your shell commands

⏪ `Cntrl + r` starts a ‘reverse search’ that lets you search for old commands by a particular word

🚫 `Cntrl + c` cancels whatever action you were doing

🔎 `ls -al` will give you *all* files, including the ones hidden by the magic `.` in front  
It *also* shows `permissions` of who can `read`, `write` (hence overwrite/delete), run/`execute` files

- rwxrwxr-- size username date filename ![](/wiki/s/-505230918/6452/267b0663176c4f8787189805bf0a33b7c6d3998e/_/images/icons/emoticons/warning.png) Be very careful who you share write access with `u` `g` `o`
- In the above read/write/execute letters are group to first by `user`, `group` and `other`
- `group` will typically literally be your lab group, but can be made from any collection of `users`
- To change file permission we have another `ch` command, `chmod` – change (file) mode
- `chmod` works on the corresponding to the letters listed on the left `chmod g-r file` will remove the ability for anyone in the `group` to read the file. Use `chmod+` to add permisions, `chmod=` to set

🕐 `ls -snew` will sort your files by the newest ones accessed

👋 `exit` (or sometimes `quit`) will get your out of most programs, including logout from Discworld

↩️ `cd -` will take you back to the last folder you were in

🃏 `*` is the ‘wildcard’ and will fill in the slots letters should be: `cryo*` matches `cryosparc`, `cryoEM`, `cryo-EM`, `cryotomography`, `cryogenic_hibernation_capsule` and so on. ![](/wiki/s/-505230918/6452/267b0663176c4f8787189805bf0a33b7c6d3998e/_/images/icons/emoticons/warning.png) handy, but be careful.

---

🐈 `cat` is used to show a file on the terminal: `cat file`. It’s because you can con**cat**enate two files together with it. Linux land is full of brief historical puns. See your `~/.zshrc` if you want more. `\cat` if you don’t want line numbering  
🔚 `tail --follow` live view of the bottom of a file. Very useful for `slurm-<jobID>.out` log progress

✘✓ `find-replace` is done by `sd` (newer `sed`), in modifies the file ‘live’ `sd old_word new_word file`

- ℹ️ be sure to save a copy before running a ‘find-replace’, *e.g.* with `cp file file.bak`

❔ `which` tells you where a `program` is located

![](/wiki/s/-505230918/6452/267b0663176c4f8787189805bf0a33b7c6d3998e/_/images/icons/emoticons/help_16.png) ↔️ `diff` (secretly [difftastic](https://difftastic.wilfred.me.uk/)) finds the different *lines* between two files (*i.e.* what changed?)

🔺 `delta` compare two files on a *character* level. This was done with an `--option` to your `~/.zshrc`

✂️ `cut` & `paste` are useful to work segments of files. **Be sure to back up**  
 𝄜 If handling complex tablulated data, you could try using `DataFrames` in your language of choice

🎨 we’ve used colours to make common files easier to see. run `unset EXA_COLORS` to remove some

---

Even more helpful, you can read what the commands do while in the command line.

> [!NOTE]
> **Too long; didn’t read** 📃

We have installed ‘too long didn’t read' manuals. `tldr command` will provide one line on what the command does and use examples. If you want a complete manual of a command it’s `man command`.

> [!CAUTION]
> [Please don't ‘tl;dr’ this guide, or the manual pages]  
> The manual pages examples will often tell you what you need for simple uses without having to wait for an admin to become free.

> [!IMPORTANT]
> Most tools you can also add `--help` after them to see what they do.

---

> [!NOTE]
> Basic command line (`zsh`) shell improvements.

We’ve moved to a modern user-friendly shell by default. This gives you colours, autocomplete et*c.* For command shell scripts from elsewhere you probably need to run `bash script.sh`  
We’ve but `hello_discworld.sh` in your `/home`, you’ll see it specifies at the top that it uses `bash` to run the script. Have a try with `bash hello_discworld.sh` since it’s tiny. Please queue big `program`s.  
If you really don’t like `zsh` you can ask us to change your default shell with `chsh` ('change shell')

> [!NOTE]
> We’ve swapped some classic `commands` for new ones. For example `du` ('disk usage') secretly runs the `dust` ('disk usage [programmed in rust]') implementation through `aliases`.  
> We think these are nicer and faster, but if you want to change any of these substitutions, feel free to edit your personal aliases <https://www.howtogeek.com/439736/how-to-create-aliases-and-shell-functions-on-linux/>

> [!NOTE]
> Writing to files is common task. Use the `edit <file>` command. `edit` is secretly [micro](https://github.com/zyedidia/micro)

`cp file file.bak` is a quick way to create a second copy of a small non-critical file. Anything more important should go through a proper back-up process.  
  
What’s nice is you can easily share scripts from others and you own, check out:   
`python fasta_fixed-width_to_single-line.py --help`  
It uses the powerful international [BioPython](https://biopython.org/) module that understands biological files in a clean way.

---

> [!NOTE]
> Discworld standard `s`cheduler and custom ‘helper’ commands

Since all our users are doing CryoEM work, our admin team have set up some automated scripts that can be called as if they were out-of-the box shell commands. Standard scheduler commands remain

- `sdesktop` [👷‍♂️ **undeveloped future feature**] - start a visual desktop backed by cluster resources
- `sdraft [job_name]` a custom script for Discworld has you directly editing a batch job template   
  ℹ️ batch job files are just `shell` `commands` with info for resources. We add `.slurm` to see them.
- `sbatch`- send a job file to the cluster to run in the background
- `sinteractive [resources]` - request an interactive terminal session, specify resource request
- `scancel` - cancel a job based on its `JOBID` ℹ️ `JOBID` is a number not a name, to easily track
- `sacct` - give accounting for you jobs
- `squeue` - see the state of your job in the queue. See [STATE CODES](https://slurm.schedmd.com/job_state_codes.html), `R` is running `PD` pending ![](/wiki/s/-505230918/6452/267b0663176c4f8787189805bf0a33b7c6d3998e/_/images/icons/emoticons/thumbs_up.png)
- `sinfo` - get information about the status of the cluster
- `scontrol [action] [job_ID]`- advance control over what a submitted job should do

---

### Requesting resources 🫲

> [!NOTE]
> Just ask for what you need, with a bit of overhead so your job won’t run out of time or RAM

Put the resources you need as `--flags` after `sinteractive`

|  **Resource**                                                                                                                                                                                                 |  **Meaning**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--job-name="descriptive-name"`                                                                                                                                                             | Purely for your records                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `-time=1:30:30`                                                                                                                                                                      | Time duration you hold resources (`hr:min:sec`)                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `--mem=20GB`                                                                                                                                                                          | Your RAM. That is, the memory needed to keep the program running. You just have to measure the consumption in a test job to avoid your program crashing.                                                                                                                                                                                                                                                                                                                                           |
| `--cpus-per-task=4`                                                                                                                                                                   | How many central processing units to assign per instance of the program you are running                                                                                                                                                                                                                                                                                                                                                                                                            |
| `--gres=gpu:<model>:1`                                                                                                                                                               | Since GPUs are expensive, you need to ask for the number in your generic resource. `<model>` is optional; if you know if you need a big one or a small one you can specify here.  Otherwise `--gres=gpu:<num_gpus>` is fine.                                                                                                                                                                                                                                                                       |
|                                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `--array=<indexes>`  `--array=0-N`  `--array=0,5,20-25`  `--array=0-25:5`  `--array=0-25%5` | 🪄 Advanced users may set up many *many* jobs differing by one parameter. Arrays excel here. <br/><ul><li><p>Run subjobs number 0-&gt;<em>N</em></p></li><li><p>Run jobs number 0, 5, 20-&gt;25</p></li><li><p>Run jobs with step size <code>:5</code>, <em>i.e. </em>0, 5, 10, 15, 20, 25..</p></li><li><p>Run jobs 0-&gt;25 but only run maximum 5-at-at time, to avoid overwhelming the queue</p></li></ul> Please read the [SLURM Array manual page](https://slurm.schedmd.com/job_array.html) |

---

### Data at the door 🗂️

> [!WARNING]
> **Do not pull your CryoEM particle data down to your /home drive**. The cluster already knows how to access the data and handles transfers, you just occasionally need to tell it where it go looking.   
>   
> The EMU manages the raw data from the instruments and is classified (*see below*) and stored on the central university’s storage solution.

- **Raw data** - This is generated from the instruments at the Electron Microscopy Unit. They handle permissions and backup of the raw data
- **Processing data** - This lives on the university’s ‘Elastic Storage Solution’. It doesn’t live on Discworld (it’s in a different room) so it needs to be *mounted* (like a USB) by giving the programs this file path structure to your data:  
   `/data/ESS/<cryo instrument>/<lab head lastname>/<user_zID>/(raw|live|processing)`
- **Program data** - This is in a *pooled* `/home` drive, which through filesystem magic lives in a network of shared, expensive flash drives. As such it’s suitable for programs install and working environments (`conda` should resolve quickly). It is not suitable for CryoEM data
- **Finalised 3D maps** – these should be deposited in the appropriate scientific database (*e.g.* [EMPIAR](https://www.ebi.ac.uk/empiar/)) and/or deposited to [UNSW’s Research Data Archive](https://www.dataarchive.unsw.edu.au/) ‘glacial’ storage. The Data Archive is managed under your supervisor’s [Research Data Management Plan](https://www.dataarchive.unsw.edu.au/help/rdmp-and-data-archive).
- ⁉️ **Unsure?** - Doesn’t fit the above classes? Contact an admin at [sbf@unsw.edu.au](mailto:sbf@unsw.edu.au) or for complex classification cases talk to the [UNSW Research Data Management support team](mailto:RDM@unsw.edu.au)

> [!IMPORTANT]
> 🌐 **Globus [In Development]** - UNSW has a [Globus](https://app.globus.org/) site license. Globus excels at large data transfers, and makes data points discoverable (like EM data connected at another Facility). Please use the Globus portal and all the data sharing permissions it grants you. It has many nifty features.

`rsync` - when in doubt this is a safe, resumable way to remotely sync data between Linux systems.

---

🤕 **- What to do when things go wrong**

> [!WARNING]
> **PLEASE DON’T DO ANYTHING DANGEROUS RIGHT NOW.** We are in trial mode after all

> [!WARNING]
> 1. **Notice within 2 weeks**
> 2. **DON’T PANIC**
>
> 💾 We save a `snapshot` of your `/home` drive to another storage server every night. That means if you alert us within two weeks we can start the process of ‘rolling-back’ to an old save state. We only keep the last two weeks otherwise the user storage will balloon.
>
> 📜 Recall [The Laws of Discworld](The_Laws_of_Discworld.md) **/home is for your** ***tools*** **not your data**

<details>
<summary>How a containter works</summary>

It’s *kinda* like a virtual machine or an emulator (you can pick which Linux you want 🐧 )

The things that make this possible is **1.** very clever programmers **2.** sharing the Linux `kernel` without simulating a whole `operating system` and isolating it safely (fake container `sudo`)

> [!NOTE]
> The `kernel` is run by some arcane wizardry that aged many beards in the process.
>
> 🚫 Don’t learn such black magic unless it’s your job, or you are interested in dark arts ⬛

![Wikimedia - ](../attachments/21879165-5853-4428-a81f-de3aacefe642.png)

Suffice do say we stay lightweight by not having to run that magic and inscrutable penguin for every single user, we hope we can give you a sandbox `container` to play in on the top, if all works.

![3eHZJ-20250828-095035.png](../attachments/22dcdc85-5c67-4455-835d-dd6b036c431f.png)

Anyway, that’s enough peeking under the hood. Get back in your container and ship structures! 🔬

![MSC_Zoe_(ship,_2015)_003-20250828-095209.jpg](../attachments/1d4413df-a828-4b4a-8c7b-8165db75a459.jpg)

</details>

---

### GPU Alley👨‍💻🛣️

> [!IMPORTANT]
> `SLURM` (Simple Linux Utility for Resource Management) provides a single master queue for a variety of computational work, ensuring a fair quality of service for everyone.   
>   
> The `fairshare` algorithm is used. To stop other people’s smaller interactive jobs being entirely delayed, the scheduler naturally brings forward jobs that have been waiting a long time, and schedules really large jobs to start when the resources are less busy (the middle of the night or the weekend).

> [!WARNING]
> **We’ll keep our queue as simple as possible**, as such we can’t write in exceptions to your personal deadlines. Your jobs will still run efficiently, but in the share the queue determines is fairest. Accordingly, plan your work with suitable wait time if you have a deadline in the future

---

### Future improvements 🚧

> [!TIP]
> Please try to be patient and respectful with our administration and development team. We try to roll out new features to you as fast as we stably can, so require testing time.

NOT WORKING

**Most of this so far – we are currently building a minimal viable product**

PLANNED

IN TESTING

STABLE
