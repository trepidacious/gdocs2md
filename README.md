gdocs2md
========

A simple Google Apps script to convert a properly formatted Google Drive Document to the markdown (.md) format.

## Usage

### Adding to a document
This script must be added to a document to run it - the document doesn't need to be the one you wish to export:
 1. Tools > Script Editor > New
 2. Select "Blank Project", then paste the code from converttomarkdown.js into it and save.

### Preparing files
Put all documents you wish to convert into category folders within a folder in your docs list, called "DocsToConvertToMarkdown". Each category folder can contain multiple documents. You can use just one category folder, e.g. "default" if you don't want to use categories.

### Running the script
1. Tools > Script Manager
2. Select "convertDefaultFolder()" function.
3. Click Run button.
4. All documents in the folder will be converted to markdown, and resulting files put in a new subfolder called "ExportedMarkdown-TIMESTAMP" where TIMESTAMP is the current ISO GMT timestamp. Note that during conversion, the export folder will be named "ExportedMarkdown-IN-PROGRESS" - see notes below in Miscellaneous section on resuming.

### Settings
There are several optional features, convertDefaultFolder() runs with most features enabled, however most other functions take a settings object. The following fields should be set to true to enable the corresponding features:
 * **markdownTables** - Output tables in GitHub-Flavoured Markdown rather than HTML. This also supports bold and italic formatting, and inline code blocks, within table cells.

 * **plainTextOutput** - Output markdown to plaintext files (type "text/plain" with .txt extension),allowing for viewing directly in Google Docs. If this is not specified, files will be have type "text/x-markdown" and .md extension.

 * **boldItalicIsQuote** - Any lines starting with bold+italic formatting will become block quotes in the markdown output.

 * **codeBlocks** - Any lines starting with a tab and then containing at least one courier-new formatted character will be considered as code lines. In addition, any empty or whitespace-only lines following a code line will be considered to be code lines. Runs of code lines will be output with three backticks before and after the run, and with the first tab (if any) removed from each line, to form a standard markdown code block.

### Using different folders
You can call convertFolderByName(folderName, settings) with a different folder name as required

### Miscellaneous
  * There are also functions for emailing documents, see source for details.
  * You may find that for large sets of documents, the script will time out. In this case, please restart the script and it will attempt to resume the conversion from where it reached. Repeatedly running the script should allow it to complete. Files named "EXPORT-COMPLETE.txt" are used to track progress to allow resuming - these can safely be deleted or ignored after export is complete.

## Interpreted formats
  * Text:
    * paragraphs are separated by two newlines
    * text styled as heading 1, 2, 3, etc is converted to Markdown heading: #, ##, ###, etc
    * text formatted with Courier New is backquoted: ``text``
    * links are converted to MD format: `[anchortext](url)`
  * Lists:
    * Numbered lists are converted correctly, including nested lists
    * bullet lists are converted to "`*`" Markdown format appropriately, including nested lists
  * Images:
    * images are correctly extracted and sent as attachments
  * Blocks:
    * Table of contents is replaced by `[[TOC]]`
    * blocks of text delimited by "--- class whateverclassnameyouwant" and "---" are converted to `<div class="whateverclassnameyouwant"></div>`
    * Source code:
      * **UPDATED**: blocks of text delimited by "--- source code" or "--- src" and "---" are converted to `<pre></pre>`
      * **NEW**: blocks of text delimited by "--- source pretty" or "--- srcp" and "---" are converted to `<pre class="prettyprint"></pre>`
    * Tables:
      * **NEW**: Simple `<table>` processing
  * "--- jsperf `<testID>`" is replaced by an iframe that shows an interactive chart of a JSPerf test. The `<testID>` is the last part of the URL of the Browserscope anchor in your JSPerf test. Something like `"agt1YS1wcm9maWxlcnINCxIEVGVzdBjlm_EQDA"` in the URL `http://www.browserscope.org/user/tests/table/agt1YS1wcm9maWxlcnINCxIEVGVzdBjlm_EQDA`

## CONTRIBUTORS

* Renato Mangini - [G+](//google.com/+renatomangini) - [Github](//github.com/mangini)
* Ed Bacher - [G+](//plus.google.com/106923847899206957842) - [Github](//github.com/evbacher)
* Ben Webster - [Github](//github.com/trepidacious)

## LICENSE

Use this script at your will, on any document you want and for any purpose, commercial or not.
The MarkDown files generated by this script are not considered derivative work and
don't require any attribution to the owners of this script.

If you want to modify and redistribute the script (not the converted documents - those are yours),
just keep a reference to this repo or to the license info below:

```
Copyright 2013 Google Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
