# Von Bits und Beats

## Setup
Bevor wir richtig anfangen, lasst uns prüfen, ob unser Raspberry Pi funktioniert, und eine Umgebung für unser späteres Projekt aufsetzen. Um dies zu tun, befolge einefach folgende Schritte:
  1. Schalte den Raspberry Pi ein, indem du ihn mit Strom versorgst
  2. erstelle einen Ordner "Theremin" auf dem Desktop
  3. Erstelle eine Datei `theremin.py`, indem du in dem Ordner einen Rechtsklick machst und "Neue Datei" auswählst

## Let's make some noise!
`Achtung! Bitte ändert niemals etwas an der Verkabelung, wenn der Raspberry Pi läuft. Es besteht die Gefahr, dass die Elektronik dabei durchbrennt!!!!`

Nachdem wir uns diesen dezenten Aufruf zu Herzen genommen haben, wenden wir uns zuerst einer Möglichkeit zu mit dem Mikrocontroller einen Ton zu erzeugen. Hierfür werden wir einen handelsüblichen Piezobuzzer mit einem Piezoelement verwenden, so wie er auch in beinahe allen PCs verbaut ist.
Wikipedia sagt folgendes:
> Ein Piezoelement ist ein Bauteil, das den Piezoeffekt ausnutzt, um entweder durch Anlegen einer elektrischen Spannung eine mechanische Bewegung auszuführen (Piezoaktor, verwendet den sogenannten inversen Piezoeffekt), oder bei Einwirkung einer mechanischen Kraft eine elektrische Spannung zu produzieren. 

![Piezo Animation](https://upload.wikimedia.org/wikipedia/commons/c/c4/SchemaPiezo.gif)

Das bedeutet also, dass ein Piezoelement je nach angelegter Spannung seine Form ändert. Dies mag jetzt noch nicht besonders klingen (oder vielleicht schon, falls ihr das noch nicht kennt), aber wirklich praktisch wird dieses Bauteil erst wenn wir überlegen, was Schall eigentlich ist.
Schall ist letztendlich nichts anderes als eine Welle, die sich in der Luft als verdichtete und ausgedehnte Teile manifestiert. Das bedeutet also, dass wir Schall (und somit einen Ton) erzeugen können, wenn wir diese Welle erzeugen.

![Schallwellen](https://upload.wikimedia.org/wikipedia/commons/8/82/Spherical_pressure_waves.gif)

Im einfachsten Falle erzeugt ein Körper durch Verdrängung genau dies. _Wenn wir doch nur ein Bauelement kennen würden, welches sich elektronisch steuern lässt und seine Form ändern kann ..._


## Herr Fischer, Herr Fischer, wie tief ist das Wasser?


Dillinger is a cloud-enabled, mobile-ready, offline-storage, AngularJS powered HTML5 Markdown editor.

  - Type some Markdown on the left
  - See HTML in the right
  - Magic

# New Features!

  - Import a HTML file and watch it magically convert to Markdown
  - Drag and drop images (requires your Dropbox account be linked)


You can also:
  - Import and save files from GitHub, Dropbox, Google Drive and One Drive
  - Drag and drop markdown and HTML files into Dillinger
  - Export documents as Markdown, HTML and PDF

Markdown is a lightweight markup language based on the formatting conventions that people naturally use in email.  As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually* written in Markdown! To get a feel for Markdown's syntax, type some text into the left window and watch the results in the right.

### Tech

Dillinger uses a number of open source projects to work properly:

* [AngularJS] - HTML enhanced for web apps!
* [Ace Editor] - awesome web-based text editor
* [markdown-it] - Markdown parser done right. Fast and easy to extend.
* [Twitter Bootstrap] - great UI boilerplate for modern web apps
* [node.js] - evented I/O for the backend
* [Express] - fast node.js network app framework [@tjholowaychuk]
* [Gulp] - the streaming build system
* [Breakdance](http://breakdance.io) - HTML to Markdown converter
* [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

### Installation

Dillinger requires [Node.js](https://nodejs.org/) v4+ to run.

Install the dependencies and devDependencies and start the server.

```sh
$ cd dillinger
$ npm install -d
$ node app
```

For production environments...

```sh
$ npm install --production
$ NODE_ENV=production node app
```

### Plugins

Dillinger is currently extended with the following plugins. Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| Github | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |


### Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantanously see your updates!

Open your favorite Terminal and run these commands.

First Tab:
```sh
$ node app
```

Second Tab:
```sh
$ gulp watch
```

(optional) Third:
```sh
$ karma test
```
#### Building for source
For production release:
```sh
$ gulp build --prod
```
Generating pre-built zip archives for distribution:
```sh
$ gulp build dist --prod
```
### Docker
Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the Dockerfile if necessary. When ready, simply use the Dockerfile to build the image.

```sh
cd dillinger
docker build -t joemccann/dillinger:${package.json.version} .
```
This will create the dillinger image and pull in the necessary dependencies. Be sure to swap out `${package.json.version}` with the actual version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on your host. In this example, we simply map port 8000 of the host to port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart="always" <youruser>/dillinger:${package.json.version}
```

Verify the deployment by navigating to your server address in your preferred browser.

```sh
127.0.0.1:8000
```

#### Kubernetes + Google Cloud

See [KUBERNETES.md](https://github.com/joemccann/dillinger/blob/master/KUBERNETES.md)


### Todos

 - Write MORE Tests
 - Add Night Mode

License
----

MIT


**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>

