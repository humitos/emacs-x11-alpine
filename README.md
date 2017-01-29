## Try Emacs with Docker!

This is the **easiest way to try** all the set of humitos' configurations (https://github.com/humitos/emacs-configuration) without touching your computer configuration and break anything:

```
docker run --rm -it \
    -e DISPLAY \
    -v $(pwd):/src \
    -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
    -v $XAUTHORITY:/root/.Xauthority \
    --net=host \
    humitos/emacs-x11-alpine
```

### What that command does?

In a few words, it downloads a minimal pre-built linux image with emacs and this configuration already setup with all its
dependencies. So, once you run that command and after downloading the image (~350 Mb) you will see emacs running in your computer.


### What those strange arguments mean?

This is the explanation per argument:

-i, –interactive  
runs the command in an interactive way by keeping STDIN open

-t, –tty  
allocates a pseudo-TTY

-e, –env  
shares the DISPLAY environment variable so emacs it’s opened there

-v, –volumen  
mounts the files needed to write by the container in that DISPLAY

–net  
allows this writing communication

–rm  
automatically removes the container when it exits

### How I can edit files from my computer with this image?

As the image is ran in an isolated container, it doesn't have access to your data from your computer. So, if you want to use this image for real, you have to mount the directory where the files you want to modify are. This is done by using the `-v` option. For example:

```
-v /home/humitos/source:/src:rw
```

After running the docker command including this new parameter you will be able to modify all the files from your `/home/humitos/source` directory. This folder will be mounted under `/src` on the container so `/home/humitos/source/test.py` file will be accessed by `/src/test.py`. By the default is the current directory.


Full documentation at: https://github.com/humitos/emacs-configuration
