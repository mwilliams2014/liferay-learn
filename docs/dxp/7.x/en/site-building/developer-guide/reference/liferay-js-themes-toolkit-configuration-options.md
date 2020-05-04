# Liferay JS Themes Tookit Configuration Options

In v8.2.0+ and v10.x of the Liferay JS Themes Toolkit, you can provide a configuration file to provide answers when a generator is run, instead of manually answering the generator's prompts.
Depending on the Liferay JS Themes Toolkit generator you use (Theme, Themelet, or Layout), you have a few prompts you can [define answers for](../automatically-configuring) in your configuration file. These are listed in the tables below:

## Generator Options

**Theme Generator**, **Classic (Theme) Generator** or **Admin (Theme) Generator**

| Config Entry | Options | Default |
| --- | --- | --- |
| `themeName` | Any name | `My Liferay Theme` |
| `themeId` | Any lowercase name joined by hyphens | `my-liferay-theme` |
| `liferayVersion` | The supported versions for the Liferay JS Themes Toolkit version (v8.2.0+: `7.0` or `7.1`; v10.x.x: `7.2` or `7.3` )| The latest supported version for the Liferay JS Themes Toolkit version |
| `fontAwesome` | Whether to add Font Awesome support (`true` or `false`) | `true` |

**Themelet Generator**

| Config Entry | Options | Default |
| --- | --- | --- |
| `themeletName` | Any name | `My Liferay Themelet` |
| `themeletId` | Any lowercase name joined by hyphens | The Themelet's name lowercased, with spaces replaced with hyphens (e.g. `my-liferay-themelet`) |
| `liferayVersion` | The supported versions for the Liferay JS Themes Toolkit version (v8.2.0+: `7.0` or `7.1`; v10.x.x: `7.2` or `7.3` ) or `Any` | The latest supported version for the Liferay JS Themes Toolkit version |

**Layout Generator**

| Config Entry | Options | Default |
| --- | --- | --- |
| `layoutName` | Any name | `My Liferay Layout` |
| `layoutId` | Any lowercase name joined by hyphens | `my-liferay-layout` |
| `liferayVersion` | The supported versions for the Liferay JS Themes Toolkit version (v8.2.0+: `7.0` or `7.1`; v10.x.x: `7.2` or `7.3` )| The latest supported version for the Liferay JS Themes Toolkit version |

```note::
  Only the Layout's name and ID can be configured. The Layout itself (rows and columns) must be created through the standard (interactive) mode. You can add a configuration file and run the Layout Generator in standard mode (`"batchMode": false`) to define default values for the `deployment <#app-server-options>`_.
```

## App Server Options

| Config Entry | Options | Default |
| --- | --- | --- |
| `deployPath` | Path to Liferay's deploy directory | `[current-folder]/deploy]` |
| `appServerPath` | Path to the application server (e.g. `/liferay/tomcat`) | `[current-folder]/tomcat]` |
| `deploymentStrategy` | `LocalAppServer`, `DockerContainer`, or `Other` | `LocalAppServer` |
| `dockerContainerName` | The Docker container's name | `liferay_portal_1` |
| `url` | The URL of the Liferay Portal server instance | `http://localhost:8080` |

```note::
  These options can be set after automatic configuration by running `npm run init` from the project's root folder.
```