<br><br>


# <p style="text-align:center"> Computational Thinking and Data Science </p>

## <p style="text-align:center">A WebBook to Accompany ENGR 1330 at TTU </p>

<p style="text-align:center">by <br><br>Theodore G. Cleveland and Farhang Forghanparast<br></p>

<p style="text-align:center">with contributions from :<br> Dinesh Sundaravadivelu Devarajan, Turgut Batuhan Baturalp (Batu), Tanja Karp, Long Nguyen, and  Mona Rizvi </p>

Copyright © 2021 Author, *The contents of this book are licensed for free consumption under the following license: [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)*

## Introduction
 
This on-line webbook is a collection of lessons, laboratory, and exercises contents for ENGR-1330 sections taught bt the first two authors; students in other sections are welcome to use this as a resource with proper attribution (check with your instructor regarding what they will consider acceptable) 

suggested citation: 

<font color=magenta>Theodore G. Cleveland, Farhang Forghanparast, Dinesh Sundaravadivelu Devarajan, Turgut Batuhan Baturalp (Batu), Tanja Karp, Long Nguyen, and Mona Rizvi. (2021) *Computational Thinking and Data Science: A WebBook to Accompany ENGR 1330 at TTU*, Whitacre College of Engineering, DOI (pending) [https://3.137.111.182/engr-1330-webbook/](https://3.137.111.182/engr-1330-webbook/)</font>

<!--The entire course content is served here and can be accessed from **blackboard.ttu.edu** or directly using the public URL.  
Homeworks and exams must be uploaded to **blackboard.ttu.edu** to be graded.   Solutions are posted after due dates have passed, these links are updated weekly-ish.-->

## Document History
This document is a living document and is updated frequently, Python is an ever evolving tool and stuff that works today will be constructively broken by the development team (python.org) in their quest for continuous improvement.  Generally these changes occur in the packages (libraries, external modules) and primative python is quite stable.

## Administrator Notes
The lead author built this webbook on a Raspberry Pi 4B (4GB) running Ubuntu 20.XX, an Apache Web Server, a JupyterHub (fully encrypted) with iPython extensions, R core, Latex, and MkDocs with extensions.  The deployment hardware is an Amazon Web Services Virtual Private Server (Lightsail Instance) in the West Virginia Server Farm (typically the container is run on x86-64 Xeon hardware)

Direct editing on the AWS server is possible, but the typesetting may not render correctly; additionally running some of the notebooks will use up the daily allocation of compute time on the server and the whole thing will hang up; remember to do all development and testing on the Raspberry PI or your laptop.  The development server is hardware cloned weekly (it takes 12 hours, during which it is inaccessible) 

A working backup is maintained at [https://github.com/dustykat/engr-1330-webbook](https://github.com/dustykat/engr-1330-webbook).

