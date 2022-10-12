We will enhance your VS Code as the slide deck writer. Mark `marp: true`, and write your deck!

![](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/screenshot.png)

See the documentation of [Marpit Markdown](https://marpit.marp.app/markdown) and [the features of Marp Core](https://github.com/marp-team/marp-core#features) about how to write.

> Please refer **[https://marp.app/](https://marp.app/)** for more details of Marp ecosystem. We have powerful tools for Marp Markdown: [Marpit Framework](https://marpit.marp.app/), [CLI tool](https://github.com/marp-team/marp-cli), [Web interface](https://web.marp.app/) and so on.

## Usage

Marp features will be enabled when `marp: true` is written in a front-matter of Markdown document.

```markdown
---
marp: true
---

# Your slide deck

Start writing!
```

You can create a new Marp Markdown document from **"New File..."** menu (Alt + Ctrl + Win + N / Alt + Cmd + Ctrl + N) to start writing a slide deck quickly.

![Create Marp Markdown](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/new-file.gif)

`marp: true` also can toggle by opening the quick picker from toolbar icon ![](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/toolbar-icon.png) and selecting **"Toggle Marp feature for current Markdown"**. (`markdown.marp.toggleMarpFeature`).

![Toggle Marp preview](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/toggle.gif)

## Features

### Preview Marp Markdown

While enabled Marp features by `marp: true`, Marp for VS Code can preview your Marp Markdown with the same way as [a built-in Markdown preview](https://code.visualstudio.com/docs/languages/markdown#_markdown-preview).

If you are not familiar with editing Markdown on VS Code, we recommend to learn what you can do in [VS Code documentation](https://code.visualstudio.com/docs/languages/markdown) at first.

### IntelliSense for Marp directives

[Directives](https://marpit.marp.app/directives), the inherited feature from [Marpit framework](https://marpit.marp.app/), is an important syntax to write the deck in Marp.

If enabled Marp feature by `marp: true`, Marp for VS Code extends [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense) to support auto completion, syntax highlight, hover help, and diagnostics for Marp directives.

#### Auto completion

Marp for VS Code can suggest global/local directives supported by Marp ecosystem. We remember all so you may forget them! 😛

Hit Ctrl + Space within [the front-matter](https://marpit.marp.app/directives?id=front-matter) or [HTML comment](https://marpit.marp.app/directives?id=html-comment) to show the list of directives. You can peek the help of selected directive by hitting Ctrl + Space again.

![Auto completion](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/auto-completion.gif)

Some directives such as `theme` and `paginate` are also supported auto completion for the value.

#### Highlight and hover help

The key of recognized directives are highlighted in the different color from the around. This visualization may help to find out meaningless definitions.

And you can see the help of a defined directive by hovering cursor on the recognized directive.

![Highlight and hover help](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/highlight-and-hover-help.png)

#### Diagnostics

Marp for VS Code can detect some basic problems in Marp directives. Diagnostics will help following our recommended way for writing slides.

![Diagnostics](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/diagnostics.png)

| Name | Description | [Quick Fix](https://code.visualstudio.com/docs/editor/refactoring#_code-actions-quick-fixes-and-refactorings) |
| --- | --- | --- |
| `define-math-global-directive` | Recommend to declare math typesetting library via [`math` global directive](https://github.com/marp-team/marp-core#math-global-directive) | ✅ |
| `deprecated-color-setting-shorthand` | Check [deprecated shorthands for setting slide colors](https://github.com/marp-team/marpit/issues/331) | ✅ |
| `deprecated-dollar-prefix` | Check [obsoleted directives prefixed by `$`](https://github.com/marp-team/marpit/issues/182) | ✅ |
| `ignored-math-global-directive` | Report ignored `math` global directive if disabled math by the extension setting |  |
| `overloading-global-directive` | Find out overloaded global directives |  |
| `unknown-size` | Notify if the specified [size preset](https://github.com/marp-team/marp-core/tree/main/themes#size-name-width-height) was not defined in a theme |  |
| `unknown-theme` | Notify a not recognized theme name |  |

### Export slide deck to HTML, PDF, PPTX, and image 🛡️

We have integrated [Marp CLI](https://github.com/marp-team/marp-cli/) to export your deck into several formats.

To export the content of active Markdown editor, open the quick pick from Marp icon on toolbar ![](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/toolbar-icon.png) and select **"Export slide deck..."**. (`markdown.marp.export`)

![Export slide deck](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/export.gif)

You can also execute command from the Command Palette (F1 or Ctrl/Cmd+Shift+P).

#### Supported file types

-   **HTML**
-   **PDF**
-   **PPTX** (PowerPoint document)
-   **PNG** (_First slide only)_
-   **JPEG** (_First slide only)_

Default file type can choose by `markdown.marp.exportType` preference.

> ⚠️ Export except HTML requires to install any one of [Google Chrome](https://www.google.com/chrome/), [Chromium](https://www.chromium.org/), or [Microsoft Edge](https://www.microsoft.com/edge). You may also specify the custom path for Chrome / Chromium-based browser by preference `markdown.marp.chromePath`.

### Use custom theme CSS 🛡️

You can register and use [custom theme CSS for Marpit](https://marpit.marp.app/theme-css) / [Marp Core](https://github.com/marp-team/marp-core/tree/main/themes#readme) by setting `markdown.marp.themes`, that includes remote URLs, or relative paths to local files in the current workspace.

```javascript
// Please put `.vscode/settings.json` on your workspace
{
  "markdown.marp.themes": [
    "https://example.com/foo/bar/custom-theme.css",
    "./themes/your-theme.css"
  ]
}
```

It's very similar to [a way for using custom styles in ordinary Markdown preview](https://code.visualstudio.com/docs/languages/markdown#_using-your-own-css). The registered theme can use by specifying theme name in [`theme` global directive](https://marpit.marp.app/directives?id=theme).

```css
/* @theme your-theme */

@import 'default';

section {
  background: #fc9;
}
```

```markdown
---
marp: true
theme: your-theme
---

# Use your own theme
```

Markdown preview will reload updated theme CSS automatically when you edited the registered local CSS file. It's very useful for creating your own theme.

![Use custom theme](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/custom-theme.gif)

### Outline extension

When Marp Markdown is enabled, you can use the extended [outline view](https://code.visualstudio.com/docs/languages/markdown#_outline-view) like following. They are enabled by default but you may disable by `markdown.marp.outlineExtension` preference.

#### Outline view for each slide

We extend the outline view to support slide pages in Marp Markdown.

![Outline view for each slide](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/outline.png)

> ℹ️ Please choose `Sort By: Position` from context menu of its panel if you see incorrect slide order.

#### Slide folding in editor

You can fold the content of slide in editor while editing Marp Markdown.

![Slide folding in editor](https://raw.githubusercontent.com/marp-team/marp-vscode/main/docs/fold.gif)

### Security

#### [Workspace Trust](https://code.visualstudio.com/docs/editor/workspace-trust)

Some features that may met malicious are restricted in the untrusted workspace/window. Please read [VS Code's user guide](https://code.visualstudio.com/docs/editor/workspace-trust) for details.

Features may be restricted are marked by the shield icon 🛡️ in this documentation. Marp for VS Code is available even if the current workspace is not trusted but you can use only a basic Marp preview and IntelliSense.

#### Enable HTML in Marp Markdown 🛡️

You can enable previsualization of HTML code within Marp Markdown with the `markdown.marp.enableHtml` option.

It could allow script injection from untrusted Markdown files. Thus, this feature is disabled as a default and will be _always ignored in the untrusted workspace_. Use with caution.

## Web extension

You can use Marp extension in VS Code for the Web environment like [vscode.dev](https://vscode.dev) and [github.dev](https://github.dev). Try opening [https://github.dev/marp-team/marp-vscode/blob/main/docs/example.md](https://github.dev/marp-team/marp-vscode/blob/main/docs/example.md), with an environment that has installed Marp extension.

The web extension has some limitations:

-   _Export command cannot use_ because it is depending on Marp CLI that is not designed for Web. Please use VS Code that is installed to your local environment, or [GitHub Codespaces](https://github.com/features/codespaces) if you wanted an environment working on Web.