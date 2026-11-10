DOCUMENT TO HTML CONVERTER
==========================

A single-file, offline tool that turns pasted text, Markdown, or uploaded Word
(.docx) files into clean, simple HTML. No CSS is added to the output. No
libraries, no server, no internet connection needed.

File: document-to-html-converter.html


1. HOW TO USE
-------------
1. Open document-to-html-converter.html in a current browser
   (Chrome, Edge, Firefox 113+, or Safari 16.4+).
2. Paste text or Markdown into the left box, OR click "Upload file" (or drag
   a file onto the left box).
3. The right side updates live. Use the "Preview" tab to see the result and
   the "HTML code" tab to see the code.
4. Click "Copy HTML" to copy the code, or "Download .html" to save it as a file.

Buttons
  Upload file     Load a .docx, .md, .markdown or .txt file.
  Load sample     Fill the box with example content.
  Clear           Empty the input.
  Copy HTML       Copy the generated HTML to the clipboard.
  Download .html  Save a complete, plain HTML page (document.html).


2. OPTIONS
----------
Output style
  Standard                 Keeps bold, italic and links.
  Promo terms              Plain text lists: no bold/italic, no links,
                           simple <li>text</li> items (matches the promo
                           sample code).

Individual switches (they can be changed after choosing a style)
  Keep bold & italic       Off = bold/italic markers are removed, text kept.
  Keep links               Off = links become plain text.
  Wrap list items in <p>   On  = <li><p>text</p></li>
                           Off = <li>text</li>   (default)
  Auto-link plain URLs     On  = https://... in text becomes a link.
                           Off = stays plain text (default).
  Full HTML page (no CSS)  On  = output includes <!DOCTYPE>, <head>, <body>.
                           Off = only the HTML fragment (default).
  Match pasted spacing     Keeps single line breaks (<br>), indentation and
                           repeated spaces (&nbsp;), and extra blank lines
                           (<p>&nbsp;</p>).


3. SUPPORTED INPUT
------------------
Markdown / plain text
  # Heading 1 ... ###### Heading 6
  **bold**   *italic*   ~~strikethrough~~   `inline code`
  [text](https://example.com)   <https://example.com>
  ![alt](https://example.com/image.png)
  - bullet item            (also * and +)
  1. numbered item         (a numbered list starting at 7 gets start="7")
  a. b. c. / i. ii. iii.   Lettered/roman items become BULLETS.
  Nested lists by indenting (blank lines between items are fine)
  | Table | Header |       Tables with a |---|---| separator row
  > blockquote
  ```code block```         (optionally with a language name)
  ---                      Horizontal rule
  \* \_ \#                 Backslash escapes work.

Heading markers (for text copied from documents)
  A line that ends (or starts) with <h1> ... <h6> becomes a heading of that
  size, and the marker is removed:
      How to manage your finances <h1>   ->  <h1>How to manage ...</h1>
      Start with the right account <h2>  ->  <h2>Start with ...</h2>
  A heading that wrapped onto two lines is joined into one heading.

Word files (.docx)
  The file is read in your browser and converted to editable Markdown, which
  then becomes HTML. It keeps:
    - Bold, italic, strikethrough
    - Links (normal links and Word field links)
    - Headings: Word Heading 1-6 / Title styles, or typed <h1>-<h6> markers
    - Bulleted and numbered lists, including nested lists
    - Tables
    - Empty paragraphs (as spacing, when "Match pasted spacing" is on)
  Special handling
    - Lists pasted from the web (every item is its own list in Word): nesting
      is worked out from indentation.
    - Nested lettered/roman items (a. b. c.) become bullets.
    - Typed numbers/letters/bullets ("7. ...", "a. ...", "- ...") are turned
      into real list items.
    - An indented line right after a list item continues that item
      (for example "...must provide the" + "following details:").
  Not included
    - Images (the page tells you how many were skipped)
    - Underline, colors, highlights, text boxes, footnotes, headers/footers
    - Old .doc files (save as .docx in Word first)
  Tip: after uploading, you can edit the Markdown in the left box, for
  example to delete a title line you do not want in the output.


4. OUTPUT FORMAT
----------------
Plain HTML only: <h1>-<h6>, <p>, <strong>, <em>, <del>, <code>, <pre>, <a>,
<img>, <ul>, <ol>, <li>, <table>/<thead>/<tbody>/<tr>/<th>/<td>,
<blockquote>, <hr>, <br>.
No class, style or target attributes are added.
Text is escaped (& < > "). Apostrophes stay as a plain '.
The Preview uses light styling for readability; that styling is never put
into the copied or downloaded HTML.


5. SECURITY
-----------
- All raw HTML in the input is shown as text, never executed
  (for example <script> becomes harmless text).
- Link addresses are limited to http, https, mailto, tel, #anchors and
  relative paths. javascript: links are removed.
- Images only accept https URLs or base64 png/jpeg/gif/webp data.
- The preview runs in a sandboxed frame with scripts disabled.
- Everything runs locally. Your documents are never uploaded anywhere.


6. LIMITS AND NOTES
-------------------
- Maximum upload size: 30 MB.
- Upper-case list markers (A. B. C.) are not treated as lists, to avoid
  mistaking names such as "A. Smith".
- Text edits are not made for you (for example "P1,000" stays as it is in
  the document).
- Word title lines before the first list are converted too; delete them in
  the input box if you do not need them.
- .docx reading needs a browser with DecompressionStream support
  (Chrome/Edge 103+, Firefox 113+, Safari 16.4+).


7. TROUBLESHOOTING
------------------
"Old .doc files are not supported"
    Open the file in Word and use Save As -> .docx, then upload again.
"Your browser is too old to open .docx files"
    Update your browser or use a current Chrome, Edge, Firefox or Safari.
Links are missing in the output
    Check that "Keep links" is ticked and the style is not "Promo terms".
Bold/italic is missing in the output
    Check that "Keep bold & italic" is ticked and the style is "Standard".
Copy button does nothing
    Some browsers block clipboard access for local files. Select the text in
    the "HTML code" tab and copy it manually, or use "Download .html".
