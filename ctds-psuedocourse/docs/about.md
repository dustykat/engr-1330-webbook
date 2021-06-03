## About ENGR 1330 Webbook
The purpose of the webook/repository is to maintain a convienent back-up of course content for rapid migration across servers.  

## Special Notes
1. The structure is written to work on a web host, with hostname == `atomickitty.ddns.net`, if you clone to another server you will have the lovely task of changing the links.  The string editor `sed` will become your friend!

2. Materials herein come from many sources, in particular the Data8 repository from UC Berkeley.  Sources in notebooks are at least cited by a URL.  As the content is matured, proper citations are to be inserted.

3. The `3-Readings` directory contains copyrighted materials and should be exposed with care on a web server; generally no-one reads anymore, so its probably safe enought to protect using `.htaccess` simple uid:pwd approach. I use the materials during lectures to point out where I obtain various computational ideas.

## How to Use
1. Clone the entire repository to /var/www/html/engr-1330-webbook.  Have your main index point to this directory i.e. `http://your-fqdn-server.org/engr-1330-webroot/`
You can see working example at https://3.137.111.182/engr-1330-webbook/ (You will have to set a browser exception to accept the self-signed certificate)

## Syncronization Notes:
1. Sync with 3.137.111.182/engr-1330-webbook/ (AWS server -- primary and live website copy)
2. Sync with 75.3.84.227:192.168.1.75/ (Raspberry Pi -- developer and backup website copy)
3. Sync with 75.3.84.227:192.168.1.79/ (Macintosh -- developer copy)

# About this document

Put something here about the document, authors, copyright (GPL or MIT Open License)

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

