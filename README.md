# Plato

**Plato** is an [IndieWeb](https://indiewebcamp.com/why)-inspired web-based asset browser. My assets. My family's assets. (If you host your own **Plato** instance, then _your_ assets.)

Assets? Anything you want: the written word (long or short form), photos, voice memos, reviews (of book, film), quotes, and just about anything you can keep on a hard drive.

# Why Plato?

Because of [Forms](https://en.wikipedia.org/wiki/Theory_of_Forms). Or "shapes", really.

All your assets come in a certain shape. Or, you'd like to view or present it in a certain shape.

A **review** comes in the shape "precis of content, followed by your opinion of said content, perhaps enhanced with some media (like a book cover), followed by a point rating (e.g. out of 5 stars, or 10 marks)".

A **photograph** comes in the shape "the image, optionally followed by some written description, geo-location, date and timestamp, and links to individuals (if any) with whom the moment was shared".

And so on.

(And because I feel a bit philosophical right now.)

# I mean, why Plato-the-thing?

We all create a lot of stuff. Memories, words, projects, photos, essays.

Some _thoughts_ start in Evernote.
Some _projects_ start on Github.
Some _hacks_ start on your hard drive.
Some _doodles_ start in one of your 5 empty Moleskines.
Some _great ideas_ start on your mobile phone's note-taking app.

**That's fine - everything starts somewhere.** However...

Some _photos_ stay trapped in your phone's ```/media``` folder.
Some _voice memos_ stay trapped in WhatsApp.
Some _blog posts_ are scattered over 2 Jekyll installations and 1 FTP site somewhere.

Everything must start or end, or be remembered on **Plato**.
(in the case of content re-posted to silos, the content must certainly start on **Plato**)

**Plato** - The aggregator for your digital life.

# Some quick technical thoughts

Assets will live on a file-system -- the simplest of databases. It is easy to browse with existing tools. It is easy to put together with existing tools, e.g. copy, drag-drop, rsync. It is easy to back up, e.g. right-click / create archive, or ```cp -R /plato /my/backups```.

Your assets might live remotely, so a web API with a window into your filesystem will suffice.

The **Plato** viewer will be web-based. As such, **Forms** will be served to humans using HTML. Each **Form** can be customised to look a certain way, e.g. photographs at a high resolution front-and-center, with description underneath, possibly with cinema mode.

Assets will be discoverable. This could be path-based, or using some other meta data system.

Meta data could give more meaning to the basic components of a **Form** in the form of tags, categories, dates, and links.

# Inspirations

* [jcs](https://jcs.org/)
* [Huginn](https://github.com/cantino/huginn)
* [IndieWeb projects](https://indiewebcamp.com/Projects)
* [A previous experiment](https://github.com/uysio/vierkante) - Basically an experiment in rendering different things from an ElasticSearch cache, and heavily inspired by [jcs](https://jcs.org/)

# Architecture

<pre>
                                    +---------------------+                                                             
                                    |                     |                                                             
    +----------->2FA <--------------+       web API       |                                                             
                                    |        (in)         |                                                             
                                    +---------+-----------+                                                             
YOU                                           |                                                                         
                                              |                                                                         
          +------------------+      +---------v-----------+     +-----------------+     +---------------+               
          |                  |      |                     |     |                 |     |               |               
    +----->    local access  +------>     /plato (DB)     +----->     render      +----->    serve      +------>   WORLD
          |                  |      |                     |     |                 |     |    (out)      |               
          +------------------+      +---------------------+     +-------+-^-------+     +---------------+               
                                                                        | |                                             
                                                                        | |                                             
                                                                    +---v-+---+                                         
                                                                    |         |                                         
                                                                    |  cache  |                                         
                                                                    |         |                                         
                                                                    +---------+                                         
</pre>

## cache

Could be a path-based asset cache like ElasticSearch as used in [vierkante](https://github.com/uysio/vierkante).

## render

Or "webify".

Turns assets into something that can be rendered on the web.

E.g. go from this:

    /plato/Forms/photos/2015/11/17/birthday.tiff

To this:

    ls -1 /plato-render/photos/2015/11/17
    image.png
    image.thumb.png
    image.hd.png
    index.html

## serve

Statically serves ```/plato-render/index.html``` and all children.

## web API

A secure, authenticated web-based API that will accept **Forms** and related assets from your good self, either via a web frontend, a mobile app, Twilio, or some other service which is authorised to use it (like IFTTT or Zapier).

## plato DB

The filesystem where RAW assets live. Could potentially effect **render** via [inotify](https://en.wikipedia.org/wiki/Inotify)

# Some things I believe in

* Alan Kay is almost definitely always right
* Simpler is better, but no simpler
* Show, don't tell
* Build upon what came before
* [s-exppressions](https://en.wikipedia.org/wiki/S-expression) is the only way to program
* Don't use [silos](https://en.wikipedia.org/wiki/Information_silo), unless it's your own silo
