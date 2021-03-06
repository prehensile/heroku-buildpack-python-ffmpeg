Heroku buildpack: Python-ffmpeg
===============================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/). The only difference from the clean Python buildpack is that this one includes ffmpeg. A static build is simply cloned from [this repo](https://github.com/integricho/ffmpeg1.2-static-with-codecs), which includes a couple of useful codecs, but still trying to be light on disk space.

This version of **heroku-buildpack-python-ffmpeg** is a simple update of [integricho's buildpack](https://github.com/integricho/heroku-buildpack-python-ffmpeg), based on a newer revision of the base [heroku-buildpack-python](https://github.com/heroku/heroku-buildpack-python).

Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --buildpack git://github.com/prehensile/heroku-buildpack-python-ffmpeg.git

    $ git push heroku master
    ...
    -----> Python app detected
    -----> Installing runtime (python-2.7.8)
    -----> Installing dependencies using pip
           Downloading/unpacking requests (from -r requirements.txt (line 1))
           Installing collected packages: requests
           Successfully installed requests
           Cleaning up...
    -----> Discovering process types
           Procfile declares types -> (none)

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/prehensile/heroku-buildpack-python-ffmpeg.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root.

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug.

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.4.2

Runtime options include:

- python-2.7.8
- python-3.4.2
- pypy-2.4.0 (unsupported, experimental)
- pypy3-2.4.0 (unsupported, experimental)

Other [unsupported runtimes](https://github.com/heroku/heroku-buildpack-python/tree/master/builds/runtimes) are available as well.
