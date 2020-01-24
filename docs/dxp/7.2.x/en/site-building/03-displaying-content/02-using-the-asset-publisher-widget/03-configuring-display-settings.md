# Configuring Display Settings

Once you've [selected your assets](./02-selecting-assets.md) for the Asset Publisher, you can configure several display settings to specify how users view your content. Follow these steps:

1. Hover over the Asset Publisher and click the Options icon (![Options](../../../images/icon-app-options.png)) in the widget's menu and select *Configuration*.

1. With the *Setup* tab selected, click on the *Display Settings* tab.

1. Under the *Display Settings* panel, choose a display template. These templates are in every site by default:

  * *Abstracts*: Displays the first 200-500 characters of the content, defined by the **Abstract Length** field. This is the default display template. 
  
  * *Table*: Displays the content in an HTML table which can be styled by a theme developer
  
  * *Title List*: Displays the content's title as defined by the user who entered it
  
  * *Full Content*: Displays the entire content of the entry

  These templates are available for the global scope:

  * *Rich Summary*: Displays a summary view of each asset along with a *Read More* link to the article's full content.
  
  * *Map* displays [geo-localized assets](TODO) in either a Google Map or an Open Street Map provider. The map provider can be configured in Instance Settings, and Site Settings in the Advanced section.

1. Configure the remaining options under the *Display Settings* tab:

  **Abstract Length**: Select the number of characters to display for abstracts. The default is `200`. Note this option is only available for the Abstracts display template.

  **Asset Link Behavior:** The default value is *Show Full Content*, which displays the full asset in the current Asset Publisher. *View in Context* displays the asset in the application that it belongs to. For example, a blog entry is displayed in Blogs where it was created. See the section below on display pages for more information.

  ```tip::
     When the Asset Publisher displays web content articles with an associated small image, the small image links to the full article. To use this feature, add or edit a web content article that the Asset Publisher should display. Before clicking *Publish*, click on *Abstracts*, flag *Small Image*, and upload an image. Then click *Publish*. Once your web content article appears in the Asset Publisher's list, click the small image to view the full article.
  ```

  **Number of Items to Display**: the maximum number of assets that can be displayed. If pagination is enabled, this number represents the maximum number of assets that can be displayed per page.

  **Pagination Type**: the type of UI to display for pagination. These options are available:

  * *None*: displays no pagination controls

  * *Simple*: adds Previous and Next buttons for browsing through pages of assets

  * *Regular*: adds more options and information including First and Last buttons, a dropdown selector for pages, the number of items per page, and the total number of results (assets displayed)

1. Expand the *Set and Enable* panel and check the boxes for the options you want to enable. Many of these, such as printing, flags, ratings, comments, comment ratings, and social bookmarks work the same way they do in other applications. These options are available:

  **Show Add Content Button**: When selected, an *Add New* button appears that lets users add new assets directly from the Asset Publisher application. This is checked by default.

  **Show Metadata Descriptions:** Enables Metadata descriptions such as *Content Related to...* or *Content with tag...* to display with the published assets.

  **Show Available Locales:** Since content can be localized, you can have different versions of it based on locale. Enabling this option shows the available locales, so users can view the content in their languages.

  **Set as the Default Asset Publisher for This Page**: The Asset Publisher app is an instanceable app: multiple Asset Publishers can be added to a page and each has an independent configuration. The default Asset Publisher for a page is the one used to display content associated with the page.

  **Show only assets with [current Display Page Template] as its display page template:** Display assets that only exist for the specified Display Page Template.

  **Include tags specified in the URL:** Incorporate tags specified in the URL.

  **Enable ...**: Enable/disable these options for displayed assets. The Print option adds a *Print* link to the full view of an asset. Clicking *Print* opens a new browser window with a print view of the asset. Enabling flags, related assets, ratings, comments, comment ratings, or social bookmarks add links to the corresponding social features to the full view of the asset.

  * Print
  * Flags
  * Ratings
  * Related Assets
  * Subscribe
  * Comments
  * Comment Ratings
  * View Count Increment

  ```tip::
     An alternate way to add flags, comments, and ratings to a page is through the *Page Flags*, *Page Comments*, and *Page Ratings* applications. Just add the applications in the appropriate location near the asset that should have feedback.
  ```

1. Expand the *Metadata* panel and move options from the Available box to the Current box to display the metadata for each asset. For example, you can select tags and categories for display. Then users can click on the tags and categories to filter the displayed assets manually. 

  ![You can configure the Asset Publisher to display various kinds of metadata about the displayed assets.](./configuring-display-settings/images/01.png)

1. Expand the *Grouping* panel and optionally establish grouping rules. You can group assets by type or by vocabulary. For example, suppose you have a vocabulary called *Membership Type* with two categories: *Premium* and *Regular*. If you group assets by Membership Type, all assets with the Premium category appear in one group and all assets with the Regular category appear in another group. Grouping rules are applied before any ordering rules: they're a way to divide up the displayed assets into separate lists. The ordering rules are applied separately to each group of assets.

1. Click *Save* to apply your display settings.