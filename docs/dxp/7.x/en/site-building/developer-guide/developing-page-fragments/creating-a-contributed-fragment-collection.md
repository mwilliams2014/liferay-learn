# Creating a Contributed Fragment Collection

Contributed Fragment Collections are deployable modules containing Page Fragments. The Fragments in a contributed Collection can be used just like regular Fragments, but aren't contained in the database.

```note::
  If you're running Liferay DXP 7.3+, use `Automatically deployed Fragments <./auto-deploying-fragments.md>`_ created in compressed ZIP Collections (either `with your own tools <developing-page-fragments-with-the-fragments-toolkit.md#collection-format-overview>`_ or the `Liferay Fragments Toolkit <developing-page-fragments-with-the-fragments-toolkit.md>`_ instead, as they are easier to maintain and can be modified from the UI.
```

This example runs on Liferay DXP 7.3+. 

<!-- The two statements above seem contradictory. First you say if you're running 7.3+, do something else. Then you say this example is for 7.3+. Which is it? -Rich -->
 
```note::
  All Fragments added through a Contributed Fragment Collection are available globally to all Sites.
```

<!-- Below, you should link to the Javadoc if you don't have a link to a tutorial. Either that, or make your best guess. Putting TODO links in makes it seem like we published docs that aren't ready. I'd actually rather have a broken link we can detect and correct later than put known TODO links out there. -Rich -->

To add a contributed Fragment Collection, you extend the [`BaseFragmentCollectionContributor` Class](TODO), which itself implements the [`FragmentCollectionContributor` interface](TODO).

Here, you'll learn how to contribute a Fragment Collection:

1. [Deploy a Contributed Fragment Collection](#deploy-a-contributed-fragment-collection)
1. [Add the Fragment Resources](#add-the-fragment-resources)
1. [Include the Fragment Entry in the Collection JSON](#include-the-fragment-entry-in-the-collection-json)
1. [Deploy and Test](#deploy-and-test)

## Deploy a Contributed Fragment Collection

First, deploy an example to see what a contributed Fragment Collection looks like:

1. Run the command below to start the Docker container:

<!-- If this is truly for 7.3, we should use the latest docker image (GA2 right now; probably GA3 by the time this is published). -Rich -->

    ```bash
    docker run -it -p 8080:8080 liferay/portal:7.3.0-ga1
    ```

1. Download and unzip the [Marketing Fragment Collection](https://github.com/liferay/liferay-learn/tree/master/docs/dxp/7.x/en/site-building/developer-guide/developing-fragments/creating-a-contributed-fragment-collection/liferay-l3m9.zip):

    ```bash
    curl https://github.com/liferay/liferay-learn/tree/master/docs/dxp/7.x/en/site-building/developer-guide/developing-fragments/creating-a-contributed-fragment-collection/liferay-l3m9.zip

    unzip liferay-l3m9.zip
    ```

1. Build the contributed Collection's JAR.

    ```bash
    cd contributed-marketing-fragments-collection
    ./gradlew build
    ```

1. Copy the contributed Collection's JAR to the Docker container:

<!-- The instructions below are incorrect. It should be `docker cp` and the path should be exact, which I think is `/opt/liferay/deploy`. -->

    ```bash
    cp com.liferay.learn.fragments-1.0.0.jar docker-container-name:/path/to/deploy/folder
    ```

1. Confirm the deployment to the Liferay Docker container console. The log message below should appear in the Docker console:

    ```bash
    INFO  [fileinstall-/opt/liferay/osgi/modules][BundleStartStopLogger:39] STARTED com.liferay.learn.fragments_1.0.0 [1121]
    ```

1. Verify that the contributed Collection and Fragment are available. Open your browser to `https://localhost:8080`, open the Product Menu, and go to *Site Builder* &rarr; *Page Fragments* under the Site Menu.

    ![The contributed Collection Fragment appears with the default Fragments.](./creating-a-contributed-fragment-collection/images/01.png)

Great! You successfully deployed a contributed Fragment Collection.

As you can see, the contributed Fragment Collection appears with the other default Fragment Collections, and the Fragments can't be modified from the UI. The only way to modify the Collection is to either update the module they came from or [copy the Fragment to another Collection](../../04-fragments/managing-page-fragments.md#managing-individual-page-fragments) and modify the Fragment copy.

<!-- You might want to change the above link: we know none of the folders will have numbers at this point. -Rich -->

## Contributed Fragment Collection Logic and metadata

The Fragment Collection contributor overrides two methods in the `*FragmentCollectionContributor` Class to provide information about the Collection.

The `getFragmentCollectionKey()` method returns the key/name of the Fragment Collection where these fragments are contributed:

```java
@Override
public String getFragmentCollectionKey() {
    return "Marketing Collection";
}
```

The `getServletContext()` method returns the servlet context for the contributed Fragment Collection module:

```java
@Override
public ServletContext getServletContext() {
    return _servletContext;
}
```

The `ServletContext` points to the bundle's symbolic name so it can find the Fragment resources: 

```java
@Reference(
  target = "(osgi.web.symbolicname=com.liferay.learn.fragments)"
)
private ServletContext _servletContext;
```

The `bnd.bnd` file includes a few properties that must be defined for the Collection:

* The `osgi.web.symbolicname` matches the `Bundle-SymbolicName` in the `bnd.bnd` file.
* The `Web-ContextPath` Header indicates the module folder that contains the Collection, so the `ServletContext` is correctly generated.
* The `-dsannotations-options` enables the Declarative Service annotations found in the class hierarchy of the Component class. 

See the example project's [`bnd.bnd`](https://github.com/liferay/liferay-learn/tree/master/docs/dxp/7.x/en/site-building/developer-guide/developing-fragments/creating-a-contributed-fragment-collection/liferay-l3m9.zip) for a reference of these values.

Now you'll modify the project to include another Fragment in the contributed Collection.

## Add the Fragment Resources

<!-- I think you can combine the below two sections so that you have two numbered steps: 1) Copy the Fragment into the folder, and 2) Edit the JSON. 

You'll notice also that I added a short paragraph explaining there was an included fragment, because I got confused without it. :-p

-Rich -->

Fragments in the contributed collection must be in a folder structure that mirrors the `*FragmentCollectionContributor` class package with a `/dependencies` folder appended to the end. The example has the structure `resources/com/liferay/learn/fragments/dependencies/`.

Inside the example .zip file is a completed Fragment that implements a marketing jumbotron. See [Developing Page Fragments with the Fragments Toolkit](./developing-page-fragments-with-the-fragments-toolkit.md) for more information on creating Fragments.

New packaged Fragments go in the `dependencies` folder. Move the `liferay-l3m9/marketing-jumbotron` folder in the example's ZIP file into the `resources/com/liferay/learn/fragments/dependencies/` folder. 

```note::
    The class package name and resources package name must match (e.g. ``[my.class.package.structure].dependencies``).
```

## Include the Fragment Entry in the Collection JSON

Besides including the packaged Fragment, you must also include its entry in the Collection's metadata. In the `collection.json` in the `[my.class.package.structure].dependencies` folder, add the marketing jumbotron Fragment to the `fragments` entry, as defined in the Fragment's `fragment.json` `fragmentEntryKey` entry:

<!-- You don't need to indent if you use the three tick marks to denote code. Of course, if you follow my previous comment's instructions, this will be a numbered step, and then you'll have to indent it again. I'm just mentioning this for future reference. -Rich -->

```json
{
    "fragments": [
        "marketing-card",
        "marketing-jumbotron"
    ],
    "name": "Marketing Collection"
}
```

```note::
  Contributed Fragment Collections do not support `included resources <./including-default-resources-with-fragments.md>`_.
```

## Deploy and Test

You can build and deploy the updated contributed Fragment Collection as you did above:

1. Build the updated contributed Collection's JAR.

    ```bash
    cd contributed-marketing-fragments-collection
    gradlew build
    ```

1. Copy the updated JAR to the Docker container:

    ```bash
    cd build/libs
    cp com.liferay.learn.fragments-1.0.0.jar docker-container-name:/path/to/deploy/folder
    ```

<!-- Again, the above command should be a `docker cp` and it should point to the actual deploy folder, which I believe is `/opt/liferay/deploy`. -Rich -->

1. Verify that the updated Fragment is included in the contributed Collection. Open your browser to `https://localhost:8080`, and open the Product Menu and go to *Site Builder* &rarr; *Page Fragments* under the Site Menu.

    ![The Custom Banner Fragment is included in the contributed Collection.](./creating-a-contributed-fragment-collection/images/02.png)

Congratulations! You now know how to create a contributed Fragment Collection, and have added a new contributed Fragment Collection to Liferay DXP.

## Related Information

* [Developing Page Fragments with the Fragments Toolkit](./developing-page-fragments-with-the-fragments-toolkit.md)
* [Developing Page Fragments with the Editor](./developing-page-fragments-with-the-editor.md)
