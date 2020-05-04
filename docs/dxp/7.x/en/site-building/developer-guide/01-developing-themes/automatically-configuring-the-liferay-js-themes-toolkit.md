# Automatically Configuring the Liferay JS Themes Toolkit

In v8.2.0+ and v10.x.x of the Liferay JS Themes Toolkit, you can include a configuration file to provide answers when a generator (Theme, Themelet, etc.) is run, instead of manually answering the generator's prompts. You can use this to programmatically run the generators. Follow these steps to configure a generator with automated responses:

1. Create a `config.json` file in your home directory and add the `"answers"` entry to provide the answers to the generator's questions:

    ```json
    {
            "answers": {
              
            }
    }
    ```

1. Specify the target module as the first level (init, theme, etc.) and then provide the names of the question variables next. See the [Liferay JS Themes Tookit Configuration reference](./reference/liferay-js-themes-toolkit-configuration-options.md) for the available options. An example configuration for the Theme Generator is shown below:

    ```json
    {
            "answers": {
                    "theme": {
                            "themeName": "My Liferay Theme",
                            "themeId": "my-liferay-theme",
                            "liferayVersion": "7.3"
                    },          
                    "init": {
                            "appServerPath": "/opt/tomcat",
                            "deploymentStrategy": "LocalAppServer"
                    }
            }
    }
    ```

    ```note::
      If an answer isn't provided for a prompt, the default value is used for the missing answer.
    ```

1. Enable `batchMode` to run the generator with a configuration file:

    ```json
    {
            "answers": {
                    "theme": {
                            "themeName": "My Liferay Theme",
                            "themeId": "my-liferay-theme",
                            "liferayVersion": "7.3"
                    },          
                    "init": {
                            "appServerPath": "/opt/tomcat",
                            "deploymentStrategy": "LocalAppServer"
                    }
            },
            "batchMode": true
    }
    ```

1. Run the generator with the configuration file. The example below runs the Theme Generator with a configuration file:

    ```bash
    yo liferay-theme --config config.json
    ```

    ```note:: 
      If you pass a configuration file without `batchMode` enabled, the configuration values are used as the default values when the generator is run. For instance, you can specify the default deployment directory to use every time the generator is run. Alternatively, you can place a `.generator-liferay-theme.json` file in your home directory and run the generator without the `--config` option.
    ```

Great! Now you know how to configure the Liferay JS Themes Toolkit's generators.