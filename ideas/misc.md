# Execution examples

A few ways in which **Plato** might be run, so as to guide towards an implementation.

## No args

Running **Plato** with no args should do the right thing.

    $ plato

    Usage: plato <command>

    ...where command is one of:
    sync      parse all content locations
    <path>    adds <path> to content locations

    Options:
    -f --force   Forces an operation (non-interative mode)

## New content location

Add new location to be parsed by **Plato**

    $ plato /path/to/somewhere

    /path/to/somewhere isn't yet managed by plato - add? [Y/n]

## Sync

Show if **Plato** is out of sync with the known content locations

    $ plato sync
    Plato detected the following content locations which haven't yet been Platonised:
    /new/path/to/photos
    /new/path/to/videos

    The following content locations are being Platonised:
    /path/to/texts
    /path/to/voicememos

    The following content items are missing:
    /path/to/texts/2015/01/12/xmas.txt

Given the above information, the following command will:
- platonise everything in ```/new/path/to/photos``` and ```/new/path/to/videos```
- platonise item at ```/path/to/texts/2015/01/12/xmas.txt```

    $ plato sync -f
