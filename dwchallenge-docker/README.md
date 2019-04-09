# Usage

**Warning** After the first execution this will take more then 5GB of your diskspace.

## Simple

Having docker installed and downloaded/cloned these files, change directory (cd) to where the files are and run:
```
docker-compose up
```

For the first time it's going to take few to few-teen minutes to build the image, but the consequential runs will be very fast.

Eventually it'll produce in your console something like this:
``` 
 or 127.0.0.1):8888/?token=3c0d22ecb67697d7f5df94c0059a8ad57c30bd06f0e5d163
```
Just enter in your browser:
```
https://localhost:8888/?token=3c0d22ecb67697d7f5df94c0059a8ad57c30bd06f0e5d163
```

## Some customization

To work on jupyter notebooks located on your computer edit the `docker-compose.yml` :
```
    volumes:
      - type: bind
        source: [location of your notebooks on the host filesystem]
        target: /data/notebooks
```

Wanna change the port? Edit:
```
    ports:
      - [your favorite port]:8888
```



# References

This image is somehow inspired on the Continuum Analytics original one (https://hub.docker.com/_/anaconda), plus it has the minimum stuff required for Data Workshop challenges.