Add a "<PANEL NAME>" panel for <CUSTOMER NAME> to Nuxeo Agentic UI's document view,
as code in this project, built from the platform's own components.

Nuxeo Agentic UI's source is at <PATH TO NUXEO SATORI UI>. Use it for reference only:
do not change, add or delete anything there. Everything you write goes in this
project. Do not edit the installed platform package either.

1. Read first. In Nuxeo Agentic UI's source, read libs/platform/AGENTS.md (sections
   1 to 4 and 7), docs/extension-reference.md (the slot tables), and
   docs/installing-satori-platform.md. Check the installed package's AGENTS.md,
   extension-reference.md and type declarations too: use the contract for the
   installed version if the source differs. Tell me in two or three lines which
   slot the panel goes in (sidebar, tabs or documentView) and which nxs- components
   you will use. documentView replaces the View tab body; tabs adds another tab;
   sidebar adds a drawer. If the request only hides, shows, reorders or relabels
   existing entries, say so and stop: that is a manifest change, not code.

2. Check this project's prerequisites. It needs a customer-owned Angular/Nx host
   application that can register extension providers, and a configuration package
   for the manifest. A marketplace package containing only JSON cannot load a new
   Angular component by itself. If there is no such host, explain what is missing
   and stop before writing code; do not modify Nuxeo Agentic UI to create one.

   Install the published platform release in this project. Merge this scope mapping
   into its .npmrc, keeping the other settings and adding no credentials:

       @nuxeo:registry=https://packages.nuxeo.com/repository/npm-public/

   Then run:

       npm install @nuxeo/satori-platform@alpha

   Record the exact installed version and keep the lockfile. Follow that version's
   peer requirements and the project's Nx setup. Use the Material-backed
   /components entry point; /components-satori requires the optional
   @hylandsoftware/satori-ui peer and GitHub Packages access. If the alpha cannot
   be installed, report the actual error and stop. Do not silently substitute
   platform source or a local tarball and call it a published-package test.

3. Scaffold with the shipped generators, never by hand. Use <OWNER PREFIX> for
   customer IDs and selectors, <LIBRARY NAME> for the Nx library name and
   <COMPONENT NAME> for the component name. Use lowercase kebab-case names and a
   lowercase alphanumeric owner prefix. If this project has no extension library:

       npx nx g @nuxeo/satori-platform:extension-library <LIBRARY NAME> --owner=<OWNER PREFIX>

   Then add the panel:

       npx nx g @nuxeo/satori-platform:extension-component <COMPONENT NAME> --library=<LIBRARY NAME>

   Keep the generator's marker comments. Read its generated README and provider;
   remove or adapt starter navigation and sample contributions that this panel
   does not need. Use extension-component, not the internal satori-component
   generator. Keep the panel class out of the library's public barrel.

4. Build the panel from @nuxeo/satori-platform/components rather than re-creating
   what it has: nxs-empty-state for the empty case and nxs-error-state for failures,
   for example. Read their declared inputs and translate text before passing it.
   Put customer text under <OWNER PREFIX>.* translation keys, with an English
   catalogue loaded by this host. Ensure platform-owned translation keys resolve
   through the host catalogue or providePlatformEnglishFallback() from /ui.
   Colours come from theme variables (--mat-sys-*), never hex values. Data comes
   through the platform's services, never fetch(). Import only published entry
   points. Handle loading, empty, denied-access and other failure states separately.

5. Place it. A registered component is not on screen until a manifest places it.
   Add an entry to this project's manifest fragment for the slot from step 1, with
   componentId set to the exact ID the generator registered. Use the descriptor
   fields in the installed extension reference, including the translated tab or
   drawer label and any navigation needed to open it. For documentView, limit the
   entry to <DOCUMENT TYPE> using the documented matcher; that host passes the
   focused document through a document input. Do not assume tabs or sidebar pass
   the same inputs. Make inputs optional unless that slot actually supplies them.

   Add the generated provide<Owner>Extensions() provider to this project's host
   application, using the provider's actual generated name. Build that host so
   its bundle includes the contribution. Keep the manifest in this project's
   configuration package, depending on nuxeo-agentic-ui, and check its deployment
   path and overwrite settings. Explain how this customer's host build and
   configuration are deployed; a manifest alone does not ship the component code.

6. Check it. Add a spec that asserts ExtensionComponentRegistry.has() for the new
   component ID, and render the panel through ExtensionOutletComponent with the
   inputs its real slot supplies. Cover data, empty and denied-access states. Run
   the host build and the library's tests, typecheck and lint, then the shipped
   guardrail (use the actual generated library directory):

       npx nx test <LIBRARY NAME>
       npx nx typecheck <LIBRARY NAME>
       npx nx lint <LIBRARY NAME>
       node node_modules/@nuxeo/satori-platform/guardrails/check-extension-library.mjs <LIBRARY PATH>

   Fix every failure; never weaken a check or a test to pass it. Resolve guardrail
   warnings or report precisely what they leave unchecked. Build the configuration
   package too. Show the changed files, registered ID, manifest entry, installed
   platform version and command results.

7. Test it. Against my local Nuxeo, deploy this project's host and configuration,
   open a <DOCUMENT TYPE> document and screenshot the panel: with data, with none,
   and signed in as a user who cannot read that data. Confirm the correct tab,
   drawer or View body renders the panel and handles the inputs that host passes.
   Tell me what you could not verify, including any unavailable server, user or
   published package; do not guess or claim those checks passed.
