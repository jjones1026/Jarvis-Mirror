![MagicMirror²: The open source modular smart mirror platform. ](.github/header.png)

<p align="center">
	<a href="https://david-dm.org/MichMich/MagicMirror/v2-beta"><img src="https://david-dm.org/MichMich/MagicMirror/v2-beta.svg" alt="Dependency Status"></a>
	<a href="https://david-dm.org/MichMich/MagicMirror/v2-beta#info=devDependencies"><img src="https://david-dm.org/MichMich/MagicMirror/v2-beta/dev-status.svg" alt="devDependency Status"></a>
	<a href="https://nodejs.org"><img src="https://img.shields.io/badge/node-v5.10.1-brightgreen.svg" alt="Node Version"></a>
	<a href="http://choosealicense.com/licenses/mit"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
	<a href="https://snyk.io/test/github/MichMich/MagicMirror/v2-beta"><img src="https://snyk.io/test/github/MichMich/MagicMirror/v2-beta/badge.svg" alt="Known Vulnerabilities" data-canonical-src="https://snyk.io/test/npm/name" style="max-width:100%;"></a>
</p>

**MagicMirror²** is an open source modular smart mirror platform. With a growing list of installable modules, the **MagicMirror²** allows you to convert your hallway or bathroom mirror into your personal assistant. **MagicMirror²** is built by the creator of [the original MagicMirror](http://michaelteeuw.nl/tagged/magicmirror) with the incredible help of a [growing community of contributors](https://github.com/MichMich/MagicMirror/graphs/contributors). 

MagicMirror² focuses on a modular plugin system and uses [Electron](http://electron.atom.io/) as an application wrapper. So no more web server or browser installs necessary!

**NOTE:** This version is in currently in beta stage. Please use the master branch if you need a thoroughly tested version.

## Table Of Contents

- [Usage](#usage)
- [Configuration](#configuration)
- [Modules](#modules)
- [Known Issues](#known-issues)
- [Contributing Guidelines](#contributing-guidelines)

## Usage 

#### Automatic Installer (Raspberry Pi Only!)

Execute the following command on your Raspberry Pi to install MagicMirror²:
````
curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/v2-beta/installers/raspberry.sh | bash
````

#### Manual Installation

1. Download and install the latest Node.js version.
2. Clone the repository and check out the beta branch: `git clone -b v2-beta https://github.com/MichMich/MagicMirror`
3. Enter the repository: `cd ~/MagicMirror`
4. Install and run the app: `npm install && npm start` (You may have to restart your terminal before this works!)

**Important:** `npm start` does **not** work via SSH, use `DISPLAY=:0 nohup npm start &` instead. This starts the mirror on the remote display.

#### Server Only

In some cases, you want to start the application without an actual app window. In this case, execute the following command from the MagicMirror folder: `node serveronly`. This will start the server, after which you can open the application in your browser of choice.

#### Raspberry Configuration & Auto Start.

The following wiki links are helpful in the configuration of your MagicMirror² operating system:
- [Configuring the Raspberry Pi](https://github.com/MichMich/MagicMirror/wiki/Configuring-the-Raspberry-Pi)
- [Auto Starting MagicMirror](https://github.com/MichMich/MagicMirror/wiki/Auto-Starting-MagicMirror)

## Configuration

1. Duplicate `config/config.js.sample` to `config/config.js`.
2. Modify your required settings.

The following properties can be configured:


| **Option** | **Description** |
| --- | --- |
| `port` | The port on which the MagicMirror² server will run on. The default value is `8080`. |
| `language` | The language of the interface. (Note: Not all elements will be localized.) Possible values are `en`, `nl`, `ru`, `fr`, etc., but the default value is `en`. |
| `timeFormat` | The form of time notation that will be used. Possible values are `12` or `24`. The default is `24`. |
| `modules` | An array of active modules. **The array must contain objects. See the next table below for more information.** |

Module configuration:

| **Option** | **Description** |
| --- | --- |
| `module` | The name of the module. This can also contain the subfolder. Valid examples include `clock`, `default/calendar` and `custommodules/mymodule`. |
| `position` | The location of the module in which the module will be loaded. Possible values are `top_ bar`, `top_left`, `top_center`, `top_right`, `upper_third`, `middle_center`, `lower_third`, `bottom_left`, `bottom_center`, `bottom_right`, `bottom_bar`, `fullscreen_above`, and `fullscreen_below`. This field is optional but most modules require this field to set. Check the documentation of the module for more information. Multiple modules with the same position will be ordered based on the order in the configuration file. |
| `classes` | Additional classes which are passed to the module. The field is optional. |
| `header` | To display a header text above the module, add the header property. This field is optional. |
| `config` | An object with the module configuration properties. Check the documentation of the module for more information. This field is optional, unless the module requires extra configuration. |

## Modules

The following modules are installed by default.

- [**Clock**](modules/default/clock)
- [**Calendar**](modules/default/calendar)
- [**Current Weather**](modules/default/currentweather)
- [**Weather Forecast**](modules/default/weatherforecast)
- [**News Feed**](modules/default/newsfeed)
- [**Compliments**](modules/default/compliments)
- [**Hello World**](modules/default/helloworld)
- [**Alert**](modules/default/alert)

The following modules are created by their respective authors.

- **[MMM-FRITZ-Box-Callmonitor by PaViRo](https://github.com/paviro/MMM-FRITZ-Box-Callmonitor)** <br> FRITZ!Box Callmonitor (Display an alert when someone is calling ...)

- **[MMM-Facial-Recognition by PaViRo](https://github.com/paviro/MMM-Facial-Recognition)** <br> Facial recognition and module swapping based on the current user ...

- **[MMM-Wunderlist by PaViRo](https://github.com/paviro/MMM-Wunderlist)** <br> Displays your Wunderlist todos on your mirror ...
 
- **[MMM-wordnik by Vendittelli](https://github.com/SVendittelli/MMM-wordnik)** <br> Get the word of the day, its definition, and origin ...

- **[MMM-SystemTemperature by MichMich](https://github.com/MichMich/mmm-systemtemperature)** <br> Display your Raspberry Pi's processor temperature on your MagicMirror.

**Note:** If you want to build your own modules, check out the [MagicMirror² Module Development Documentation](modules)

## Known issues

- Electron seems to have some issues on certain Raspberry Pi 2's. See [#145](https://github.com/MichMich/MagicMirror/issues/145).
- MagicMirror² (Electron) sometimes quits without an error after an extended period of use. See [#150](https://github.com/MichMich/MagicMirror/issues/150). 

## Contributing Guidelines

Contributions of all kinds are welcome, not only in the form of code but also with regards bug reports and documentation.

Please keep the following in mind:

- **Bug Reports**:  Make sure you're running the latest version. If the issue(s) still persist: please open a clearly documented issue with a clear title. 
- **Minor Bug Fixes**: Please send a pull request with a clear explanation of the issue or a link to the issue it solves.
- **Major Bug Fixes**: please discuss your approach in an GitHub issue before you start to alter a big part of the code.
- **New Features**: please please discuss in a GitHub issue before you start to alter a big part of the code. Without discussion upfront, the pull request will not be accepted / merged.

Thanks for your help in making MagicMirror² better! 
