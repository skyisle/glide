Glide
=====

[![Build Status](https://travis-ci.org/bumptech/glide.svg?branch=master)](https://travis-ci.org/bumptech/glide)

Glide is a fast and efficient open source media management framework for Android that wraps media decoding, memory and
disk caching, and resource pooling into a simple and easy to use interface.

![](static/glide_logo.png)

Glide supports fetching, decoding, and displaying video stills, images, and animated GIFs. Glide includes a flexible api
that allows developers to plug in to almost any network stack. By default Glide uses a custom HttpUrlConnection based
stack, but also includes utility libraries plug in to Google's Volley project or Square's OkHttp library instead.

Glide's primary focus is on making scrolling any kind of a list of images as smooth and fast as possible, but Glide is
also effective for almost any case where you need to fetch, resize, and display a remote image.

Download
--------
You can download a jar from GitHub's [releases page][1].

Or use Gradle:

```groovy
repositories {
  mavenCentral()
}

dependencies {
    compile 'com.github.bumptech.glide:glide:3.4.+'
    compile 'com.android.support:support-v4:19.1.0'
}
```

Or Maven:

```xml
<dependency>
  <groupId>com.github.bumptech.glide</groupId>
  <artifactId>glide</artifactId>
  <version>3.4.0</version>
  <type>aar</type>
</dependency>
<dependency>
  <groupId>com.google.android</groupId>
  <artifactId>support-v4</artifactId>
  <version>r7</version>
</dependency>
```

How do I use Glide?
-------------------
Checkout the [GitHub wiki][2] for pages on a variety of topics, and see the [javadocs][3].

Simple use cases will look something like this:

```Java

// For a simple view:
@Override
public void onCreate(Bundle savedInstanceState) {
    ...

    ImageView imageView = (ImageView) findViewById(R.id.my_image_view);

    Glide.with(this).load("http://goo.gl/h8qOq7").into(imageView);
}

// For a list:
@Override
public View getView(int position, View recycled, ViewGroup container) {
    final ImageView myImageView;
    if (recycled == null) {
        myImageView = (ImageView) inflater.inflate(R.layout.my_image_view,
                container, false);
    } else {
        myImageView = (ImageView) recycled;
    }

    String url = myUrls.get(position);

    Glide.with(myFragment)
        .load(url)
        .centerCrop()
        .placeholder(R.drawable.loading_spinner)
        .crossFade()
        .into(myImageView);

    return myImageView;
}

```

Volley
-------
Volley is now an optional dependency that can be included via a utility library. To use Volley to fetch media over
http/https:

With Gradle:

```groovy
dependencies {
    compile 'com.github.bumptech.glide:volley-integration:1.1.+'
    compile 'com.mcxiaoke.volley:library:1.0.+'
}
```

Or with Maven:

```xml
<dependency>
    <groupId>com.github.bumptech.glide</groupId>
    <artifactId>volley-integration</artifactId>
    <version>1.1.0</version>
    <type>jar</type>
</dependency>
<dependency>
    <groupId>com.mcxiaoke.volley</groupId>
    <artifactId>library</artifactId>
    <version>1.0.5</version>
    <type>aar</type>
</dependency>
```

Then in your Activity or Application, register the Volley based model loader:
```java
public void onCreate() {
  Glide.get(this).register(GlideUrl.class, InputStream.class,
        new VolleyUrlLoader.Factory(yourRequestQueue));
  ...
}
```

After the call to register any requests using http or https will go through Volley.

OkHttp
------
In addition to Volley, Glide also includes support for fetching media using OkHttp. To use OkHttp to fetch media over
http/https:

With Gradle:

```groovy
dependencies {
    compile 'com.github.bumptech.glide:okhttp-integration:1.1.+'
    compile 'com.squareup.okhttp:okhttp:2.0.+'
}
```

Or with Maven:

```xml
<dependency>
    <groupId>com.github.bumptech.glide</groupId>
    <artifactId>okhttp-integration</artifactId>
    <version>1.1.0</version>
    <type>jar</type>
</dependency>
<dependency>
    <groupId>com.squareup.okhttp</groupId>
    <artifactId>okhttp</artifactId>
    <version>2.0.0</version>
    <type>jar</type>
</dependency>
```

Then in your Activity or Application, register the OkHttp based model loader:
```java
public void onCreate() {
  Glide.get(this).register(GlideUrl.class, InputStream.class,
        new OkHttpUrlLoader.Factory(yourOkHttpClient));
  ...
}
```

Android SDK Version
-------------------
Glide requires a minimum sdk version of 10.

License
-------
BSD, part MIT and Apache 2.0. See LICENSE file for details.

Status
------
Version 3.x is a stable public release used in multiple open source projects at Google including in the Android Camera
app and in the 2014 Google IO app. Comments/bugs/questions/pull requests welcome!

Build
------
Building Glide with gradle is fairly straight forward:

```
git clone git@github.com:bumptech/glide.git
cd glide
git submodule init && git submodule update
./gradlew jar
```

Note: Make sure your Android SDK has the Android Support Repository installed, and that your `$ANDROID_HOME` environment
variable is pointing at the SDK or add a `local.properties` file in the root project with a `sdk.dir=...` line.

Samples
-------
Follow the steps in the 'Build' section to setup the project and then:

```
./gradlew :samples:flickr:run
./gradlew :samples:giphy:run
./gradlew :samples:svg:run
```

Development
-----------
Follow the steps in the 'Build' section to setup the project and then edit the files however you wish.
[Intellij IDEA 14][4] cleanly imports both Glide's source and tests and is the recommended way to work with Glide.

To open the project in Intellij 14:

1. Go to File.
2. Click on 'Open...'
3. Navigate to Glide's root directory.
4. Select glide-parent.iml

Getting Help
------------
To report a specific problem or feature request, [open a new issue on Github][5]. For questions, suggestions, or
anything else, join or email [Glide's discussion group][6].

Contributing
------------
Before submitting pull requests, contributors must sign Google's [individual contribution license agreement][7].

Thanks
------
* The Android team and Jake Wharton for the [disk cache implementation][8] Glide's disk cache is based on.
* Dave Smith for the [gif decoder gist][9] Glide's gif decoder is based on.
* Chris Banes for his [gradle-mvn-push][10] script.
* Corey Hall for Glide's [amazing logo][11].
* Everyone who has contributed code and reported issues!

Author
------
Sam Judd - @samajudd

Disclaimer
---------
This is not an official Google product.

[1]: https://github.com/bumptech/glide/releases
[2]: https://github.com/bumptech/glide/wiki
[3]: http://bumptech.github.io/glide/javadocs/latest/index.html
[4]: https://www.jetbrains.com/idea/download/
[5]: https://github.com/bumptech/glide/issues/new
[6]: https://groups.google.com/forum/#!forum/glidelibrary
[7]: https://developers.google.com/open-source/cla/individual
[8]: https://github.com/JakeWharton/DiskLruCache
[9]: https://gist.github.com/devunwired/4479231
[10]: https://github.com/chrisbanes/gradle-mvn-push
[11]: static/glide_logo.png