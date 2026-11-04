Brand Nuxeo Nuxeo Agentic AI with the colours of <CUSTOMER NAME>, using their public website: <URL>

Nuxeo Agentic AI's source is at <PATH TO agentic-ui-poc> Use it for reference only:
do not change, add or delete anything there. Everything you write goes in this project.

1. Read the site. Open it (in a browser if you can, otherwise download the page and its
   CSS). Find the real colours of: page background, main text, header / top menu, primary
   buttons, links, and the selected tab or menu item. Show them in a small table, with
   where you found each one.

2. Write the file. Start from a copy of Nuxeo Agentic AI's
   nuxeo-agentic-ui-package/src/main/config/bootstrap.json and save it to
   the current directory as bootstrap.json. First read, in Nuxeo Agentic AI's source,
   libs/shared/app-config/src/lib/bootstrap-config.ts and Beat 3 of
   docs/beta-demo-runbook.md to see which colour variables the app reads. Then:
   - Add a theme for this customer and make it the default (defaultThemeId).
   - Put the colours in its "tokens" and fill its "preview" swatches.
   - Set branding.documentTitle and branding.applicationTitle to "<CUSTOMER NAME>".
   - Keep all text readable (contrast at least 4.5:1). If a brand colour is too light
     for text, use it for backgrounds and buttons and pick a darker shade for text.
   - Don't try to change the logo: it is not supported. Tell me if that has changed.

3. Test it. There is a Nuxeo running form a Docker Compose stack
   (<PATH TO DOCKER COMPOSE FOLDER).
   You can access it at http://localhost:8080/nuxeo/agentic-ui, user <TEST_USER>, password <TEST_PWD>.
   Never save the credentielas in a file or anywhere.
   The, for the test:
   
   - First, backup up the nxserver/nuxeo.war/agentic-ui-config/bootstrap.json original file,
   - Then, copy the new one in,
   - And then, screenshot http://localhost:8080/nuxeo/agentic-ui/ (sign-in page, browse page, a
     document with its tabs) next to the customer site. Tell me which areas took the new
     colours and which did not, and how to put the backup back. If you cannot test, say so;
     don't guess.