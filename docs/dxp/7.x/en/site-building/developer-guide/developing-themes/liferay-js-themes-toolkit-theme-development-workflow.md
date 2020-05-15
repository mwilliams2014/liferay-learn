# Liferay JS Themes Toolkit Theme Development Workflow

Themes are built on top of one of these base themes: 

**Unstyled:** provides basic markup, functions, and images for Liferay DXP
**Styled:** inherits from the Unstyled base theme and adds some styling on top

Follow the workflow below to develop a Theme generated with the Liferay JS Themes Toolkit:

1. Mirror the [structure of the files](./theme-anatomy) you want to modify in the Theme's `/src/` folder. The main modifications are placed in the files listed below:

    * `/src/templates/portal_normal.ftl`: main markup
    * `/src/css/_custom.scss`: custom CSS styling
    * `/src/js/main.js`: the JavaScript

1. Build and deploy the Theme to your Liferay Portal server.
1. Apply the Theme [through the Look and Feel menu](applying-themes.md) by selecting your [Theme's thumbnail](./creating-a-thumbnail-preview-for-your-theme.md). 

The finished Theme is bundled as a WAR (Web application ARchive) file. 

```note::
  While developing your theme, we recommend that you enable `Developer Mode <./using-developer-mode-with-themes>`_. This un-minifies JavaScript files and disables caching for CSS and FreeMarker template files, making the debugging process much easier.
```

Theme's generated with the Liferay Theme Generator can access several helpful Gulp tasks to make the process easier:

- **build:** builds your theme's files based on the specified base theme. See the [gulp build tutorial](./building-your-themes-files.md) for more information.
- **extend:** sets the base theme or themelet to extend. See the [gulp extend tutorial](./changing-your-base-theme.md) for more information.
- **init:** specifies the app server to deploy your theme to (automatically run during the initial creation of the theme). See the [gulp init tutorial](./configuring-your-themes-app-serve.mdr for more information. 
- **kickstart:** copies files from an existing theme into your theme to help kickstart it. See the [gulp kickstart tutorial](./copying-an-existing-themes-files.md) for more information.
- **status:** lists the base theme/themelets that your theme extends. See the [gulp status tutorial](./listing-your-themes-extensions.md) for more information.
- **watch:** watches for changes to your theme's files and automatically deploys them to the server when a change is made. See the [gulp watch tutorial](./automatically-deploying-theme-changes.md) for more information.

## Theme Workflow

1. Install the [Liferay Theme Generator](./reference/installing-the-theme-generator-reference.md), if it's not installed.
1. Build the Base Files. Run the build script for your Liferay JS Toolkit version. If you're unsure of your version run `npm list -g generator-liferay-theme` from your command line to print it.

    **v9.5.0+:**

    ```bash
    npm run build
    ```

    **Older versions:**

    ```bash
    node_modules\.bin\gulp build
    ```

CSS: Add custom CSS to the Theme's `/src/css/_custom.scss` file.

JavaScript: Add custom JavaScript to the generated `/src/js/main.js` file. If this folder doesn't exist, you must create it. You can copy the `main.js` file from the `/build/js/` folder to get started.

HTML: Add your HTML markup customizations to the Theme templates in the `/src/templates/` folder. If this folder doesn't exist, you must create it. Copy the Theme templates from the `/build/templates/` folder to the `/src/templates/` folder to modify them.

```note::
  Since Liferay DXP Fix Pack 2 and Liferay Portal 7.2 CE GA2, Font Awesome is available globally as a system setting, which is enabled by default. If you're using Font Awesome icons in your theme, answer yes (y) to the Font Awesome question in v9.x.x+ of the Theme Generator to include Font Awesome imports in your theme. This ensures that your icons won't break if they are disabled in the global setting.
```

```note::
   Starting with Liferay DXP 7.1+, the overall design of `Content Pages <../../creating-pages/building-and-managing-content-pages/content-pages-overview.md>`_ can be accomplished with `Page Fragments <../../displaying-content/using-fragments/page-fragments-intro.md>`_. Starting with Liferay DXP 7.3+ users can define the common elements of a page (Header and Footer) in the `Master Page Template <../../creating-pages/defining-headers-and-footers-with-master-pages/master-page-templates-intro.md>`_ .
```


<!--
You can use the development tools you're most comfortable with so you can focus on creating a well designed theme. The following Liferay tools help you build themes:

* [Theme Builder Gradle Plugin](/docs/7-1/reference/-/knowledge_base/r/theme-builder-gradle-plugin)
* [Liferay Theme Generator](/docs/7-1/tutorials/-/knowledge_base/t/creating-themes)
* [Dev Studio](/docs/7-1/tutorials/-/knowledge_base/t/creating-themes-with-liferay-ide)
* [Blade CLI](/docs/7-1/tutorials/-/knowledge_base/t/blade-cli)'s 
  [Theme Template](/docs/7-1/reference/-/knowledge_base/r/theme-template). 

Depending on the tool you choose 
(
  [Theme Generator](/docs/7-1/reference/-/knowledge_base/r/theme-reference-guide), 
  [Gradle](/docs/7-1/reference/-/knowledge_base/r/theme-builder-gradle-plugin), 
  [Blade CLI](/docs/7-1/reference/-/knowledge_base/r/theme-template), 
  [Maven](/docs/7-1/reference/-/knowledge_base/r/theme-template), 
  or 
  [Dev Studio](/docs/7-1/reference/-/knowledge_base/r/theme-template)
), 
the theme anatomy is a bit different. The overall development process is the 
same though: 
-->