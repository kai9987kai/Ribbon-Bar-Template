# Advanced Adaptive Ribbon Interface

A modern, single-file HTML/CSS/JavaScript template for building an adaptive ribbon-style editor interface. It includes tabbed ribbon controls, rich text editing, command search, themes, local saving, exporting, accessibility improvements, and responsive behavior.

## Overview

This template is inspired by desktop productivity apps that use a ribbon toolbar. It provides a polished browser-based editing experience while keeping everything self-contained in one HTML file.

The template is useful for:

* Browser-based document editors
* Admin panels with ribbon-style controls
* Internal tools
* Prototypes for productivity software
* Learning how to build accessible UI controls with vanilla JavaScript

## Features

### Ribbon Interface

* Sticky adaptive ribbon toolbar
* Collapsible ribbon
* Tabbed sections: Home, Insert, View, and Review
* Grouped controls for better organization
* Responsive layout for smaller screens
* Tooltips for ribbon buttons
* Keyboard-accessible tabs and controls

### Rich Text Editor

* Editable document canvas using `contenteditable`
* Bold, italic, and underline formatting
* Font family and font size controls
* Text color picker with recent colors
* Alignment controls
* Ordered and unordered lists
* Headings and paragraph formatting
* Clear formatting
* Undo and redo support

### Insert Tools

* Insert tables
* Insert links
* Insert images from local files
* Insert decorative shape cards
* Insert horizontal dividers
* Insert current date
* Insert starter content sections
* Insert callout blocks

### View and Appearance

* Light theme
* Dark theme
* System theme option
* Accent color picker
* Editor zoom control
* Focus/fullscreen mode
* Optional editor outline toggle

### Review and Document Tools

* Word count
* Character count
* Estimated reading time
* Save draft locally
* Autosave to `localStorage`
* Export document as an HTML file
* Print-friendly styles
* Reset document to starter content

### Command Palette

Press `Ctrl + K` or click the command search bar to open the command palette.

The command palette lets users quickly search and run actions such as:

* Bold
* Insert Table
* Export HTML
* Save Draft
* Word Count
* Toggle Focus Mode

## Keyboard Shortcuts

| Shortcut   | Action                  |
| ---------- | ----------------------- |
| `Ctrl + K` | Open command palette    |
| `Ctrl + S` | Save draft locally      |
| `Ctrl + B` | Bold selected text      |
| `Ctrl + I` | Italicize selected text |
| `Ctrl + U` | Underline selected text |
| `Ctrl + Z` | Undo                    |
| `Ctrl + Y` | Redo                    |
| `Ctrl + P` | Print document          |

On macOS, use `Cmd` instead of `Ctrl` for most browser shortcuts.

## Getting Started

### 1. Save the File

Save the template as:

```text
advanced-adaptive-ribbon.html
```

### 2. Open in a Browser

Open the file directly in a modern browser such as Chrome, Edge, Firefox, or Safari.

No build step, package manager, server, or framework is required.

### 3. Start Editing

Click inside the document area and begin typing. Use the ribbon controls to format content, insert elements, change themes, save, export, or print.

## File Structure

The template is self-contained and organized into three main sections:

```text
advanced-adaptive-ribbon.html
├── <style>
│   ├── Theme variables
│   ├── Ribbon layout
│   ├── Editor styles
│   ├── Command palette styles
│   ├── Toast notifications
│   ├── Responsive styles
│   └── Print styles
│
├── <body>
│   ├── Ribbon toolbar
│   ├── Editable document frame
│   ├── Command palette modal
│   └── Toast notification stack
│
└── <script>
    ├── Command definitions
    ├── Editor formatting helpers
    ├── Insert actions
    ├── Theme and appearance logic
    ├── Autosave and export logic
    ├── Ribbon tab behavior
    ├── Color picker behavior
    ├── Command palette behavior
    └── Initialization
```

## Main Components

### Ribbon Tabs

Ribbon tabs are controlled by buttons with `role="tab"` and matching content panels with `role="tabpanel"`.

Example:

```html
<button
  id="home-tab"
  class="ribbon-tab active"
  role="tab"
  aria-selected="true"
  aria-controls="home-content"
  data-tab="home"
>
  Home
</button>
```

Each tab is connected to a content panel:

```html
<div
  class="ribbon-content active"
  id="home-content"
  role="tabpanel"
  aria-labelledby="home-tab"
>
  ...
</div>
```

### Editor Area

The editable document uses a `contenteditable` article:

```html
<article
  id="editor"
  class="content-area"
  contenteditable="true"
  spellcheck="true"
  aria-label="Editable document canvas"
>
  ...
</article>
```

### Command System

Commands are defined in a single array:

```js
const commands = [
  { id: 'bold', label: 'Bold', hint: 'Ctrl+B', run: () => execEditorCommand('bold') },
  { id: 'insertTable', label: 'Insert Table', hint: '', run: insertTable },
  { id: 'exportHtml', label: 'Export HTML', hint: '', run: exportHtml }
];
```

To add a new command, add a new object to the `commands` array and create a matching button using `data-command`.

Example:

```html
<button class="ribbon-button-large" type="button" data-command="insertTable">
  <span>▦</span>
  <span class="ribbon-button-text">Table</span>
</button>
```

## Customization

### Change the Accent Color

The accent color is controlled by the CSS variable:

```css
:root {
  --accent: #2563eb;
}
```

Users can also change the accent color at runtime using the View tab.

### Add a New Ribbon Tab

1. Add a new tab button inside `.ribbon-tabs`.
2. Add a matching `.ribbon-content` panel.
3. Make sure `aria-controls` on the tab matches the content panel `id`.
4. Make sure `aria-labelledby` on the content panel matches the tab `id`.

Example:

```html
<button
  id="tools-tab"
  class="ribbon-tab"
  role="tab"
  aria-selected="false"
  aria-controls="tools-content"
  data-tab="tools"
>
  Tools
</button>

<div
  class="ribbon-content"
  id="tools-content"
  role="tabpanel"
  aria-labelledby="tools-tab"
  data-tab-content="tools"
  aria-hidden="true"
>
  ...
</div>
```

### Add a New Button

Add a button with a `data-command` value:

```html
<button class="ribbon-button-large" type="button" data-command="myCommand">
  <span aria-hidden="true">★</span>
  <span class="ribbon-button-text">My Tool</span>
</button>
```

Then add a command definition:

```js
commands.push({
  id: 'myCommand',
  label: 'My Tool',
  hint: '',
  run: () => {
    alert('My custom command ran.');
  }
});
```

### Change the Starter Document

Edit the `defaultDocument` variable in the script:

```js
const defaultDocument = `
  <h1>Your Starter Title</h1>
  <p>Your starter content goes here.</p>
`;
```

Also update the initial HTML inside the `#editor` element if you want the first page load to match the reset content.

## Browser Support

This template is designed for modern browsers.

Recommended browsers:

* Google Chrome
* Microsoft Edge
* Mozilla Firefox
* Safari

Some editing commands use `document.execCommand()`. Although widely supported, this API is considered legacy. For production-grade editors, consider replacing it with a dedicated editor engine such as ProseMirror, TipTap, Slate, Lexical, or Quill.

## Accessibility Notes

The template includes several accessibility-focused improvements:

* `role="tablist"`, `role="tab"`, and `role="tabpanel"`
* `aria-selected` for active tabs
* `aria-hidden` for inactive panels
* `aria-expanded` for collapsible controls
* `aria-pressed` for toggle buttons
* Keyboard navigation for tabs
* Keyboard-accessible command palette
* Focus-visible styles
* Reduced-motion support
* Live regions for status and toast messages

For production use, test with screen readers and keyboard-only navigation.

## Local Storage

The template stores user preferences and draft content in `localStorage`.

Stored values include:

| Key                       | Purpose              |
| ------------------------- | -------------------- |
| `advancedRibbon.theme`    | Selected theme       |
| `advancedRibbon.accent`   | Accent color         |
| `advancedRibbon.document` | Saved editor content |
| `advancedRibbon.zoom`     | Editor zoom level    |

To clear saved data, use the browser developer tools or call:

```js
localStorage.removeItem('advancedRibbon.document');
localStorage.removeItem('advancedRibbon.theme');
localStorage.removeItem('advancedRibbon.accent');
localStorage.removeItem('advancedRibbon.zoom');
```

## Known Limitations

* Uses `contenteditable`, which can behave differently across browsers.
* Uses `document.execCommand()`, which is legacy but still commonly supported.
* Clipboard paste may require browser permission.
* Image insertion embeds images as base64 data URLs, which can make the document large.
* Saved drafts are stored only in the current browser on the current device.
* The template does not include authentication, cloud sync, collaboration, or server-side storage.

## Suggested Improvements

Possible next upgrades:

* Replace `execCommand()` with a modern editor framework.
* Add document templates.
* Add table row and column editing.
* Add drag-and-drop image insertion.
* Add Markdown import/export.
* Add PDF export.
* Add comments and review mode.
* Add collaborative editing.
* Add custom keyboard shortcut settings.
* Add plugin support for custom ribbon groups.
* Add better mobile toolbar behavior.

## Security Notes

Because the editor inserts HTML into the page, sanitize user-generated content before storing or rendering it in a production environment. This is especially important if content is loaded from external sources, shared between users, or saved to a server.

For production use, consider a sanitizer such as DOMPurify.

## License

You can adapt this template for personal, educational, or commercial projects. Add your preferred license
