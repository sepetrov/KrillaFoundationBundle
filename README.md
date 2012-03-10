Welcome to KrillaFoundationBundle
=================================

KrillaFoundationBundle helps you to integrate [Foundation](http://foundation.zurb.com "Foundation - Rapid Prototyping and Building Framework from ZURB") framework into your [Symfony2](http://symfony.com "Symfony2 - High Performance PHP Framework for Web Development") project.

The bundle can use either the [original](https://github.com/zurb/foundation) version of Foundation developed by [ZURB](http://foundation.zurb.com/), or the modified [LESS](https://github.com/matalin/FoundationLess) version developed Matalin Hatchard.

<a name="installation"/>
Installation
------------

- [Step 1: Download KrillaFoundationBundle](#installation-1)
- [Step 2: Configure the Autoloader](#installation-2)
- [Step 3: Enable the bundle](#installation-3)
- [Step 4: Install Foundation (optional)](#installation-4)
- [Step 5: Install YUI Compressor (optional)](#installation-5)
- [Step 6: Install assets (optional)](#installation-6)

<a name="installation-1"/>
### Step 1: Download KrillaFoundationBundle

Download the bundle using the standard Symfony2 method with the vendors script.
Add the following lines in your `deps` file:

```
[KrillaFoundationBundle]
    git=git://github.com/sepetrov/KrillaFoundationBundle.git
    target=bundles/Krilla/FoundationBundle
```
Now, run the vendors script to download the bundle:

``` bash
$ php bin/vendors update
```
<a name="installation-2"/>
### Step 2: Configure the Autoloader

Add the `Krilla` namespace to your autoloader:

``` php
<?php
// app/autoload.php

$loader->registerNamespaces(array(
    // ...
    'Krilla' => __DIR__.'/../vendor/bundles',
));
```

<a name="installation-3"/>
### Step 3: Enable the bundle

Finally, enable the bundle in the kernel:

``` php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new Krilla\FoundationBundle\KrillaFoundationBundle(),
    );
}
```
<a name="installation-4"/>
### Step 4: Install Foundation (optional)

To install Foundation using the Symfony2 vendors script, add the following lines to your `deps` file:

```
[foundation]
    git=git://github.com/zurb/foundation.git
    target=bundles/Krilla/FoundationBundle/Resources/public/foundation
```

Now, run the vendors script to download Foundation:

``` bash
$ php bin/vendors update
```
<a name="installation-5"/>
### Step 5: Install YUI Compressor (optional)

**Note:**

> This step installs the YUI Compressor from GitHub matching the download version that can be found at <http://yuilibrary.com/download/yuicompressor/>. At the time of writing it is [Version 2.4.7](http://yui.zenfs.com/releases/yuicompressor/yuicompressor-2.4.7.zip).

To install YUI Compressor using the Symfony2 vendors script, add the following lines to your `deps` file:

```
[yuicompressor]
    git=git://github.com/yui/yuicompressor.git
    version=9d65596f57
    target=yuicompressor
```

Now, run the vendors script to download YUI Compressor:

``` bash
$ php bin/vendors update
```

Now enable the Assetic filter by updating your `app/config/config.yml` file. The configuration options of interest here are `yui_css` and `yui_js`. The `assetic` section of the file should like this:

```yaml
# app/config/config.yml

# ...

# Assetic Configuration
assetic:
    debug:          %kernel.debug%
    use_controller: false
    # java: /usr/bin/java
    filters:
        cssrewrite: ~
        # closure:
        #     jar: %kernel.root_dir%/java/compiler.jar
        yui_css:
            jar: %kernel.root_dir%/../vendor/yuicompressor/build/yuicompressor-2.4.7.jar
        yui_js:
            jar: %kernel.root_dir%/../vendor/yuicompressor/build/yuicompressor-2.4.7.jar

# ...
```

<a name="installation-6"/>
### Step 6: Install assets (optional)

The template `Krilla/FoundationBundle/Resources/base_foundation.html.twig` combines the Foundation JavaScript and CSS files. Foundation suggests two files for your custom code: `vendor/bundles/Krilla/FoundationBundle/Resources/public/foundation/stylesheets/app.css` and `vendor/bundles/Krilla/FoundationBundle/Resources/public/foundation/javascripts/app.js`. The template loads `css/main.css` and `js/main.js` instead.
Here you have the option to either create those files:

```bash
$ mkdir -p web/css && touch web/css/main.css
$ mkdir -p web/js && touch web/js/main.js
```

or copy the files Foundation suggests:

```bash
$ mkdir -p web/css && [ -f web/css/main.css ] && cp web/css/main.css web/css/main.css.`date +%Y%m%d%H%M%S`.bak
$ cp vendor/bundles/Krilla/FoundationBundle/Resources/public/foundation/stylesheets/app.css web/css/main.css
$ mkdir -p web/js && [ -f web/js/main.js ] && cp web/js/main.js web/js/main.js.`date +%Y%m%d%H%M%S`.bak
$ cp vendor/bundles/Krilla/FoundationBundle/Resources/public/foundation/javascripts/app.js web/js/main.js
```
