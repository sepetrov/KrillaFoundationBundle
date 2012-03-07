<a name="top"/>
Welcome to KrillaFoundationBundle
=================================

KrillaFoundationBundle helps you to integrate [Foundation](http://foundation.zurb.com "Foundation - Rapid Prototyping and Building Framework from ZURB") framework into your [Symfony2](http://symfony.com "Symfony2 - High Performance PHP Framework for Web Development") project.

The bundle can use either the [original](https://github.com/zurb/foundation) version of Foundation developed by [ZURB](http://foundation.zurb.com/), or the modified [LESS](https://github.com/matalin/FoundationLess) version developed Matalin Hatchard.

<a name="installation"/>
Installation
------------

-  [Step 1: Download KrillaFoundationBundle](#installation-1)
-  [Step 2: Configure the Autoloader](#installation-2)
-  [Step 3: Enable the bundle](#installation-3)
-  [Step 4: Install Foundation (recommended)](#installation-4)
    - [Step 4.1: Install the original version](#installation-4-1)
    - [Step 4.2: Install the LESS version](#installation-4-2)
- [Step 5: Install YUI Compressor (recommended)](#installation-5)
- [Step 6: Install LESS compiler (optional)](#installation-6)

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

So far the only thing we can use is the `Krilla/FoundationBundle/Resources/base.html.twig` layout template.
Not very useful really! To speed up the integration of Foundation in your project and to make maximum use of the bundle it is highly recommended to follow the rest of the installation instructions.

<a name="installation-4"/>
### Step 4: Install Foundation (recommended)

Suggested are two methods of installation:

<a name="installation-4-1"/>
#### Step 4.1: Install the original version

To install the original version of Foundation using the Symfony2 vendors script, add the following lines to your `deps` file:

```
[foundation]
    git=git://github.com/zurb/foundation.git
    target=bundles/Krilla/FoundationBundle/Resources/public/foundation
```

Now, run the vendors script to download Foundation:

``` bash
$ php bin/vendors update
```

Now you can use is the `Krilla/FoundationBundle/Resources/base_foundation.html.twig` layout template. The template includes the Foundation JavaScript and CSS files. It is using [Assetic](http://symfony.com/doc/current/cookbook/assetic/yuicompressor.html "How to Minify JavaScripts and Stylesheets with YUI Compressor") filters to combine and minify them with [YUI Compressor](http://developer.yahoo.com/yui/compressor/).

**Note:**

> You can find instructions how to install YUI Compressor and configure the Assetic filters on [Step 5: Install YUI Compressor](#installation-5).


<a name="installation-4-2"/>
#### Step 4.2: Install the LESS version

To install the LESS version of Foundation using the Symfony2 vendors script, add the following lines to your `deps` file:

```
[FoundationLess]
    git=git://github.com/matalin/FoundationLess.git
    target=bundles/Krilla/FoundationBundle/Resources/public/FoundationLess
```

Now, run the vendors script to download Foundation:

``` bash
$ php bin/vendors update
```

Now you can use is the `Krilla/FoundationBundle/Resources/base_foundation_less.html.twig` or `Krilla/FoundationBundle/Resources/base_foundation_lessphp.html.twig` layout template. The templates include the Foundation JavaScript and CSS files. They are using the [Assetic](http://symfony.com/doc/current/cookbook/assetic/yuicompressor.html "How to Minify JavaScripts and Stylesheets with YUI Compressor") filter to combine and minify them with [YUI Compressor](http://developer.yahoo.com/yui/compressor/).

**Note:**

> This installation method requires a LESS compiler. The `Krilla/FoundationBundle/Resources/base_foundation_less.html.twig` template is using the `less` Assetic filter which requires a [LESS compiler](http://lesscss.org/#-server-side-usage) to be installed on [Node.js server](http://nodejs.org/). The `Krilla/FoundationBundle/Resources/base_foundation_lessphp.html.twig` template is using the `lessphp` Assetic filter, which needs the PHP LESS compiler `lessphp`. You can find instructions how to install `lessphp` in [Step 6: Install LESS compiler](#installation-6).

<a name="installation-5"/>
### Step 5: Install YUI Compressor (recommended)

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
### Step 6: Install LESS compiler (optional)

**Note:**

> LESS compiler is only needed if you choose to use the LESS version of Foundation, i.e. you have installed the Foundation framework following the instruction on [Step 4.2: Install the LESS version](#installation-4-2).
> If you have installed the original version of Foundation, following the instructions on [Step 4.1: Install the original version](#installation-4-1) and you do not plan to use LESS in your project, than you can skip this step.

The easiest way to use [LESS](http://lesscss.org) is by installing [lessphp](https://github.com/leafo/lessphp), a PHP LESS compiler. There are alternative ways to add LESS support, but that is beyond the scope of this instruction and this seems to be the fastest way to achieve the goal. After all, the main goal is to get you up and running as fast as possible.

To install `lessphp` using the Symfony2 vendors script, add the following lines to your `deps` file:

```
[lessphp]
    git=git://github.com/leafo/lessphp.git
    target=lessphp
```

Now, run the vendors script to download lessphp:

``` bash
$ php bin/vendors update
```

Now update your `app/autoload.php` file by adding with the following lines to the bottom, to make sure `lessc` class can be autoloaded:

```php
<?php
// app/autoload.php

// ...

spl_autoload_register(function($class) {
    $paths = array(
        'lessc' => __DIR__.'/../vendor/lessphp/lessc.inc.php',
    );
    isset($paths[$class]) && require $paths[$class];
});
```

Now enable the Assetic filter by updating your `app/config/config.yml` file. The configuration option of interest here is `lessphp`. The `assetic` section of the file should like this:

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
        # yui_css:
        #     jar: %kernel.root_dir%/java/yuicompressor-2.4.2.jar
        lessphp: ~

# ...
```
