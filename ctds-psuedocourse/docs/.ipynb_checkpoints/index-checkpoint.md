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

A working backup of this webbook is maintained at [https://github.com/dustykat/engr-1330-webbook](https://github.com/dustykat/engr-1330-webbook).


## About ENGR 1330 Webroot/Webbook
The purpose of the webroot repository is to maintain a convienent back-up of course content for rapid migration across servers.  The webroot is [https://github.com/dustykat/engr-1330-webroot](https://github.com/dustykat/engr-1330-webroot); this webroot is specific to the lead author's server.  This webbook is contained WITHIN the webroot in directory `engr-1330-webbook` and the .gitignore for the webroot repository contains this directory listing.  However the book itself is stand alone, and can be copied directly into another webroot (and linked appropriately)

## Special Notes
1. The structure is written to work on a web host, with hostname == `atomickitty.ddns.net`, if you clone to another server you will have the lovely task of changing the links.  The string editor `sed` will become your friend!

2. Materials herein come from many sources, in particular the Data8 repository from UC Berkeley.  Sources in notebooks are at least cited by a URL.  As the content is matured, proper citations are to be inserted.

## How to Use
1. Clone the entire repository to /var/www/html/symlink_to_engr-1330-webbook.  Have your main index point to this directory i.e. `http://your-fqdn-server.org/symlink_to_engr-1330-webroot/`
You can see working example at [https://atomickitty.ddns.net/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/site/](https://atomickitty.ddns.net/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/site/) (You will have to set a browser exception to accept the self-signed certificate)

## Syncronization Notes:
1. Sync with atomickitty.ddns.net:3.137.111.182 (AWS server -- primary and live website copy)
2. Sync with 75.3.84.227:192.168.1.75/ (ATT server Raspberry Pi -- development website copy)
3. Sync with 75.3.84.227:192.168.1.79/ (Macintosh -- developer copy)

## On-Line Book Author's Notes

- Inserting Code Fragments

To insert a code fragment such as `print('Hello World')` simply indent in the source file used to generate the document

    print('hello world')
    
These fragments can be cut-and-paste into a JupyterLab notebook.

- Inserting Images

If the image is taken from a URL, use the following:

    ![image-name (a local tag)](url_to_image_source)

Such as:

    ![image-name](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQqn40YbupkMAzY63jYtA6auEmjRfCOvCd0FA&usqp=CAU)

Which will render a black swan:

![image-name](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQqn40YbupkMAzY63jYtA6auEmjRfCOvCd0FA&usqp=CAU)

If the image is local to the host replace the url with the path to the image.

- Inserting URL links

This is a variation of images, but without the `!`, such as

    [link-name-that-will-display](url_to_link_destimation)
    
For example the code below will link to the black swan search results:

    [link-to-images-of-black-swans](https://www.google.com/search?q=images+of+black+swan&client=safari&rls=en&sxsrf=ALeKk03oIoQ387TWjJoKzX-D_b7o1to43Q:1613002985584&tbm=isch&source=iu&ictx=1&fir=L2P5MiS1ICLTxM%252CC6BDdJoXT9KcEM%252C_&vet=1&usg=AI4_-kTXrBMpj__xL5IkGCshrXTp04fX3w&sa=X&ved=2ahUKEwiCneivyODuAhVJBs0KHY88CaAQ9QF6BAgUEAE&biw=1447&bih=975#imgrc=i_lxoojURNE3XM)

[link-to-images-of-black-swans](https://www.google.com/search?q=images+of+black+swan&client=safari&rls=en&sxsrf=ALeKk03oIoQ387TWjJoKzX-D_b7o1to43Q:1613002985584&tbm=isch&source=iu&ictx=1&fir=L2P5MiS1ICLTxM%252CC6BDdJoXT9KcEM%252C_&vet=1&usg=AI4_-kTXrBMpj__xL5IkGCshrXTp04fX3w&sa=X&ved=2ahUKEwiCneivyODuAhVJBs0KHY88CaAQ9QF6BAgUEAE&biw=1447&bih=975#imgrc=i_lxoojURNE3XM)



