---
Weitong Zhang, June 29th, 2018

---

# C# 
## 1 in List<>()
### 1.1 *SelectMany()* Method
See full *Microsoft* documentation [here](https://msdn.microsoft.com/en-us/library/bb534336(v=vs.110).aspx).
In *C#*:
```c
class PetOwner
{
    public string Name { get; set; }
    public List<String> Pets { get; set; }
}

public static void SelectManyEx1()
{
    PetOwner[] petOwners = 
        { new PetOwner { Name="Higa, Sidney", 
              Pets = new List<string>{ "Scruffy", "Sam" } },
          new PetOwner { Name="Ashkenazi, Ronen", 
              Pets = new List<string>{ "Walker", "Sugar" } },
          new PetOwner { Name="Price, Vernette", 
              Pets = new List<string>{ "Scratches", "Diesel" } } };

    // Query using SelectMany().
    IEnumerable<string> query1 = petOwners.SelectMany(petOwner => petOwner.Pets);

    Console.WriteLine("Using SelectMany():");

    // Only one foreach loop is required to iterate 
    // through the results since it is a
    // one-dimensional collection.
    foreach (string pet in query1)
    {
        Console.WriteLine(pet);
    }
```
And this will return:
> Using SelectMany():
> Scruffy
> Sam
> Walker
> Sugar
> Scratches
> Diesel

### 1.2 *ToDictionary()* Method
See full *Microsoft* documentation [here](https://msdn.microsoft.com/en-us/library/bb549277(v=vs.110).aspx).
Note this line in the following example:
> Dictionary<long, Package> dictionary = packages.ToDictionary(p => p.TrackingNumber);

It will use *TrackingNumber* as the key in the **Dictionary**, and the package itself contains the attribute of *TrackingNumber*.
```csharp
class Package
{
    public string Company { get; set; }
    public double Weight { get; set; }
    public long TrackingNumber { get; set; }
}

public static void ToDictionaryEx1()
{
    List<Package> packages =
        new List<Package>
            { new Package { Company = "Coho Vineyard", Weight = 25.2, TrackingNumber = 89453312L },
              new Package { Company = "Lucerne Publishing", Weight = 18.7, TrackingNumber = 89112755L },
              new Package { Company = "Wingtip Toys", Weight = 6.0, TrackingNumber = 299456122L },
              new Package { Company = "Adventure Works", Weight = 33.8, TrackingNumber = 4665518773L } };

    // Create a Dictionary of Package objects, 
    // using TrackingNumber as the key.
    Dictionary<long, Package> dictionary = packages.ToDictionary(p => p.TrackingNumber);

    foreach (KeyValuePair<long, Package> kvp in dictionary)
    {
        Console.WriteLine(
            "Key {0}: {1}, {2} pounds",
            kvp.Key,
            kvp.Value.Company,
            kvp.Value.Weight);
    }
}
```
> This code produces the following output:
> Key 89453312: Coho Vineyard, 25.2 pounds
 Key 89112755: Lucerne Publishing, 18.7 pounds
 Key 299456122: Wingtip Toys, 6 pounds
 Key 4665518773: Adventure Works, 33.8 pounds




---

# Java 
## 1 List Interface
See full general introduction [here](https://www.javatpoint.com/java-list).
> List Interface is the subinterface of **Collection**.

Being an interface means it cannot be *instantiated* (`new List()` is not possible).
To instanize a List:
```java
List<String> names1 = new ArrayList<String>();
List<String> names2 = new LinkedList<String>();
List<String> names3 = new Vector<String>();
```
You can also instantiate it with values, in an easier way, using the Arrays class, as follows:
```java
List<String> names = Arrays.asList("sup1", "sup2", "sup3");
```
However, note that it is not allowed to add more elements to that list, as it's *fixed-size*.




---
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
docker build -t joemccann/dillinger:${package.json.version}
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
