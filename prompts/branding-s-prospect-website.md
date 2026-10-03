Brand Nuxeo Satori with the colours of <CUSTOMER NAME>, using their public website: <URL>

Satori's source is at <PATH TO agentic-ui-poc>. Use it for reference only: do not change,
add or delete anything there. Everything you write goes in this project.

1. Read the site. Open it (in a browser if you can, otherwise download the page and its
   CSS). Find the real colours of: page background, main text, header / top menu, primary
   buttons, links, and the selected tab or menu item. Show them in a small table, with
   where you found each one.

2. Write the file. Start from a copy of Satori's
   nuxeo-agentic-ui-package/src/main/config/bootstrap.json and save it to
   <CONFIG PATH>/bootstrap.json in this project. First read, in Satori's source,
   libs/shared/app-config/src/lib/bootstrap-config.ts and Beat 3 of
   docs/beta-demo-runbook.md to see which colour variables the app reads. Then:
   - Add a theme for this customer and make it the default (defaultThemeId).
   - Put the colours in its "tokens" and fill its "preview" swatches.
   - Set branding.documentTitle and branding.applicationTitle to "<CUSTOMER NAME>".
   - Keep all text readable (contrast at least 4.5:1). If a brand colour is too light
     for text, use it for backgrounds and buttons and pick a darker shade for text.
   - Don't try to change the logo: it is not supported. Tell me if that has changed.

3. Check the package. This project's install.xml must copy the file to
   nxserver/nuxeo.war/agentic-ui-config/ with overwrite="true": Satori's package already
   installed a bootstrap.json there, and a copy with overwrite="false" onto an existing
   file makes the install fail. package.xml must depend on nuxeo-agentic-ui. Fix them if
   needed and tell me what you changed.

4. Test it. If my local Nuxeo (Docker container "nuxeo") has Satori installed: back up its
   nxserver/nuxeo.war/agentic-ui-config/bootstrap.json, copy the new one in, and
   screenshot http://localhost:8080/nuxeo/agentic-ui/ (sign-in page, browse page, a
   document with its tabs) next to the customer site. Tell me which areas took the new
   colours and which did not, and how to put the backup back. If you cannot test, say so;
   don't guess.