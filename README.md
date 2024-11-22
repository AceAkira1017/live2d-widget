# Live2D Widget

![](https://forthebadge.com/images/badges/built-with-love.svg)
![](https://forthebadge.com/images/badges/uses-html.svg)
![](https://forthebadge.com/images/badges/made-with-javascript.svg)
![](https://forthebadge.com/images/badges/contains-cat-gifs.svg)
![](https://forthebadge.com/images/badges/powered-by-electricity.svg)
![](https://forthebadge.com/images/badges/makes-people-smile.svg)

[English](README.en.md)

## Features

Add Live2D characters to your webpage. Compatible with PJAX, supports seamless loading.

<img src="assets/screenshot-2.png" width="280"><img src="assets/screenshot-3.png" width="280"><img src="assets/screenshot-1.png" width="270">

(Note: The character models above are for demonstration purposes only; this repository does not include any models.)

You can also check out example webpages:

- View the effect in the bottom left corner of [Mimi's Blog](https://zhangshuqiao.org)
- [demo.html](https://stevenjoezhang.github.io/live2d-widget/demo/demo.html), showcasing basic functionality
- [login.html](https://stevenjoezhang.github.io/live2d-widget/demo/login.html), simulating an NPM login interface

## Usage

If you are a beginner or only need the most basic functionality, simply add this line of code to the `head` or `body` of your HTML page to load the character:

```xml
<script src="https://fastly.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/autoload.js"></script>
```

The placement of this code depends on how your website is built. For example, if you are using [Hexo](https://hexo.io), you need to add the above code in the theme's template files. The modification method is similar for pages generated with various template engines.  
If your website has PJAX enabled, since the character does not need to refresh on every page, be sure to place this script outside the PJAX refresh area.

**However! We strongly recommend configuring it yourself to make the character more suitable for your website!**  
If you are interested in tinkering, please see the detailed instructions below.

## Configuration

You can refer to the source code of `autoload.js` to see the optional configuration items. `autoload.js` will automatically load three files: `waifu.css`, `live2d.min.js`, and `waifu-tips.js`. `waifu-tips.js` creates the `initWidget` function, which is the main function for loading the character. The `initWidget` function accepts an Object type parameter as the configuration for the character. Here are the configuration options:

| Option       | Type     | Default Value                                                                 | Description                                                                 |
|--------------|----------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `waifuPath`  | `string` | `https://fastly.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/waifu-tips.json` | Path to character resources, can be modified by yourself                  |
| `apiPath`    | `string` | `https://live2d.fghrsh.net/api/`                                             | API path, optional parameter                                                |
| `cdnPath`    | `string` | `https://fastly.jsdelivr.net/gh/fghrsh/live2d_api/`                         | CDN path, optional parameter                                                |
| `tools`      | `string[]` | See `autoload.js`                                                            | Buttons for loading small tools, optional parameter                        |

Among these, you only need to set one of the `apiPath` or `cdnPath` parameters. The `apiPath` is the URL of the backend API, which you can set up yourself and add models (this requires more modifications, which will not be elaborated here). You can refer to [live2d_api](https://github.com/fghrsh/live2d_api). The `cdnPath` loads resources through a CDN service like jsDelivr, which is more stable.

## Customization

If the options provided in the "Configuration" section are not sufficient for your needs, you can modify them yourself. The directory structure of this repository is as follows:

- `src/waifu-tips.js` contains the logic for buttons and dialogs;
- `waifu-tips.js` is automatically generated from `src/waifu-tips.js`, direct modification is not recommended;
- `waifu-tips.json` defines the trigger conditions (`selector`, CSS selector) and the text displayed when triggered (`text`);
- `waifu.css` is the stylesheet for the character.

The default CSS selector rules in `waifu-tips.json` are effective for Hexo's [NexT theme](http://github.com/next-theme/hexo-theme-next). You may need to modify them or add new content to suit your own webpage.  
**Warning: The content in `waifu-tips.json` may not be suitable for all age groups or appropriate for access during work hours. Please ensure they are appropriate for use.**

To set up a local development testing environment for this project, you need to install Node.js and npm, then execute the following commands:

```bash
git clone https://github.com/stevenjoezhang/live2d-widget.git
npm install
npm run build
```

If you have any questions, feel free to open an issue. If you have any modification suggestions, feel free to submit a pull request.

## Deployment

After making modifications locally, you can deploy the modified project on a server or load it via CDN for use on your webpage.

### Using CDN

To customize the content, you can fork this repository and push the modified content to your repository via git. The usage method will then change to:

```xml
<script src="https://fastly.jsdelivr.net/gh/username/live2d-widget@latest/autoload.js"></script>
```

Replace `username` with your GitHub username. To ensure the CDN content refreshes properly, you need to create a new git tag and push it to your GitHub repository; otherwise, `@latest` will still point to the previous version. Additionally, the CDN itself has caching, so changes may take some time to take effect. Related documentation:
- [Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
- [Managing releases in a repository](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)

### Self-host

You can also directly place these files on your server instead of loading them via CDN.

- If you can connect to your host via `ssh`, clone the forked and modified code repository to the server.
- If your host cannot connect via `ssh` (like typical shared hosting), modify the code locally and upload the files to the website's directory via `ftp` or similar methods.
- If you are deploying a static blog using tools like Hexo, place the project's code in the blog's source file directory (e.g., the `source` directory). When you redeploy the blog, the relevant files will automatically upload to the corresponding paths. To prevent these files from being incorrectly modified by Hexo plugins, you may need to set `skip_render`.

This way, the entire project can be accessed via your domain. Try to see if you can open `autoload.js` and `live2d.min.js` in your browser and confirm that the content of these files is complete and correct.  
If everything is normal, then modify the constant `live2d_path` in `autoload.js` to the URL of the `live2d-widget` directory. For example, if you can access `live2d.min.js` via:

```
https://example.com/path/to/live2d-widget/live2d.min.js
```

Then set the value of `live2d_path` to:

```
https://example.com/path/to/live2d-widget/
```

Make sure to include the trailing `/` at the end of the path.  
After completing this, add the following line to the interface where you want to add the character:

```xml
<script src="https://example.com/path/to/live2d-widget/autoload.js"></script>
```

## Acknowledgments

<a href="https://www.browserstack.com/">
  <picture>
    <source media="(prefers-color-scheme: dark)" height="80" srcset="https://d98b8t1nnulk5.cloudfront.net/production/images/layout/logo-header.png?1469004780">
    <source media="(prefers-color-scheme: light)" height="80" srcset="https://live.browserstack.com/images/opensource/browserstack-logo.svg">
    <img alt="BrowserStack Logo" height="80" src="https://live.browserstack.com/images/opensource/browserstack-logo.svg">
  </picture>
</a>

> Thanks to [BrowserStack](https://www.browserstack.com/) for providing the infrastructure that allows us to test in real browsers!

<a href="https://www.jsdelivr.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" height="80" srcset="https://raw.githubusercontent.com/jsdelivr/jsdelivr-media/master/white/svg/jsdelivr-logo-horizontal.svg">
    <source media="(prefers-color-scheme: light)" height="80" srcset="https://raw.githubusercontent.com/jsdelivr/jsdelivr-media/master/default/svg/jsdelivr-logo-horizontal.svg">
    <img alt="jsDelivr Logo" height="80" src="https://raw.githubusercontent.com/jsdelivr/jsdelivr-media/master/default/svg/jsdelivr-logo-horizontal.svg">
  </picture>
</a>

> Thanks to jsDelivr for providing public CDN service.

The code is derived from this blog post:  
https://www.fghrsh.net/post/123.html

Thanks to [Hitokoto](https://hitokoto.cn) for providing the statement API.

When clicking the paper airplane button of the character, an Easter egg will appear, which comes from [WebsiteAsteroids](http://www.websiteasteroids.com).

## More

For more content, you can refer to:  
https://nocilol.me/archives/lab/add-dynamic-poster-girl-with-live2d-to-your-blog-02  
https://github.com/xiazeyu/live2d-widget.js  
https://github.com/summerscar/live2dDemo

Regarding backend API models:  
https://github.com/xiazeyu/live2d-widget-models  
https://github.com/xiaoski/live2d_models_collection

In addition, there are desktop versions:  
https://github.com/amorist/platelet  
https://github.com/akiroz/Live2D-Widget  
https://github.com/zenghongtu/PPet  
https://github.com/LikeNeko/L2dPetForMac

And for Wallpaper Engine:  
https://github.com/guansss/nep-live2d

## License

Released under the GNU General Public License v3  
http://www.gnu.org/licenses/gpl-3.0.html

This repository does not include any models; all Live2D models, images, action data, etc., used for demonstration are copyrighted by their original authors and are for research and learning purposes only, not for commercial use.

Live2D official website:  
https://www.live2d.com/en/  
https://live2d.github.io

Live2D Cubism Core is provided under the Live2D Proprietary Software License.  
https://www.live2d.com/eula/live2d-proprietary-software-license-agreement_en.html  
Live2D Cubism Components are provided under the Live2D Open Software License.  
http://www.live2d.com/eula/live2d-open-software-license-agreement_en.html

> The terms and conditions do prohibit modification, but obfuscating in `live2d.min.js` would not be considered illegal modification.  
https://community.live2d.com/discussion/140/webgl-developer-licence-and-javascript-question

## Changelog

On October 31, 2018, the original API provided by fghrsh was deprecated; please update to the new address. Reference article:  
https://www.fghrsh.net/post/170.html

As of January 1, 2020, this project no longer depends on jQuery.

As of November 1, 2022, this project no longer requires users to load Font Awesome separately.
