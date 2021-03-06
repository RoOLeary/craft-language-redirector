# Language Redirector plugin for Craft CMS 3.x

This plugin automatically redirects visitors to their preferred language

## Requirements

This plugin requires Craft CMS 3.0.0 or later.

## Installation

To install the plugin, either use the Plugin Store (in the Craft Control Panel) or follow these instructions.

1. Open your terminal and go to your Craft project:

        cd /path/to/project

2. Then tell Composer to load the plugin:

        composer require pierrestoffe/craft-language-redirector

3. In the Control Panel, go to Settings → Plugins and click the “Install” button for Language Redirector.

## Language Redirector Overview

If you've ever developed a multilingual website, you've probably thought about automatically redirecting your visitors to their preferred language. While it may have sounded simple at first, you obviously eventually realised it wasn't. Indeed, you have to take quite a few parameters into account:
- The Sites defined in Craft
- The languages used in your Sites
- The language chosen in the language switcher
- The language(s) accepted by your visitor's browser
- Whether the Entry exists in the target language

Language Redirector mixes all these parameters and provides you with an easy-to-implement solution.

## Configuring Language Redirector

1. Copy the config.php file provided at the root of the plugin directory to the `config` folder of your Craft install.
2. Name it `language-redirector.php`.
3. Assign sites to languages in the `languages` array, either using their handle or their ID. For example: `'en' => 'english'` or `'fr' => 5`. Don't forget that the configuration file is multi-environment friendy, just like any other Craft config file.

If you feel like it, you can also rename the URL query parameter name and the session key. By default, they are both set to 'lang'.

## Using Language Redirector

Adding a language switcher to your website becomes way easier with this plugin.
As the `craft.languageSwitcher.getUrls()` function returns the URLs of the currently-visited element in all the languages defined in the config file, your language switcher could look like this:

```
{% set allLanguages = craft.languageSwitcher.getUrls() %}

<ul>
    {% for item in allLanguages %}
        <li>
            <a href="{{ item.url }}" hreflang="{{ item.id }}" lang="{{ item.id }}" title="{{ 'Switch to {language}'|translate({
                language: item.name
            }) }}">
                {{ item.nativeName|capitalize }}
            </a>
        </li>
    {% endfor %}
</ul>
```

Brought to you by [Pierre Stoffe](https://pierrestoffe.be)