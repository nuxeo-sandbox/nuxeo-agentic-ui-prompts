# Nuxeo Agentic UI — prompt library

Ready-to-use prompts to customise [Nuxeo Agentic UI](https://github.com/nuxeo/agentic-ui-poc)
(product name: Nuxeo Satori) with an AI coding agent such as Claude Code, without writing the
code yourself.

> [!CAUTION]
> Nuxeo Agentic UI / Nuxeo Satori are **Work in progress**, in Beta and a lot of things
> can change.

## Principles

- **You prompt, the agent builds.** Each prompt describes one customisation in plain
  language. The agent does the work and shows you the result.
- **Nuxeo Agentic UI is never modified.** The agent reads Nuxeo Agentic AI's source to
  learn how it works and writes everything into your own Nuxeo package, so upgrading
  Nuxeo Agentic UI stays a version bump.
- **Configuration goes in a marketplace package.** Code extensions also need a
  customer-owned Angular host build that registers their providers; a configuration
  package alone cannot load new component code.
- **One prompt, one customisation.** Small prompts are easier to tune, test and combine.
- **Proof, not promises.** Every prompt asks the agent to test its result, show
  screenshots, and say what it could not verify.

## How to use

1. **Get Nuxeo Agentic UI's source.** Clone or fork <https://github.com/nuxeo/agentic-ui-poc>.
   The agent only reads it.
2. **Create your Nuxeo package project**, with Nuxeo CLI or by asking your agent to
   scaffold an empty marketplace package that depends on `nuxeo-agentic-ui`.
   For a code prompt, also provide a customer-owned Angular/Nx host application
   that consumes `@nuxeo/satori-platform`; follow the
   [consumer installation guide](https://github.com/nuxeo/Nuxeo-Satori-UI/blob/main/docs/installing-satori-platform.md)
   for the registry and peer requirements. The panel prompt assumes the alpha is
   published. Until then, its registry install and end-to-end validation remain pending.
3. **Start your agent session from that package folder**, and give it read access to
   Nuxeo Agentic UI's folder: `claude --add-dir /path/to/agentic-ui-poc` in the terminal,
   or add the folder to the session in the desktop app.
4. **Pick a prompt** in [`prompts/`](prompts) and replace its `<PLACEHOLDERS>`: customer
   name, Nuxeo Agentic UI's path, the target path in your package… Tune the rest if needed.
5. **Paste it** into the session. Answer the agent's questions and review what it changed.
6. **Build, deploy, test.** Build the package, install it on your Nuxeo server
   (`nuxeoctl mp-install`) and check the result in the browser. For a quick check before
   packaging, a prompt can also copy its file straight into your local Nuxeo.

## Prompts

| Prompt                                                                   | What it does                                                                                                                          | Level    | Status                                                               |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------------- |
| [branding-s-prospect-website.md](prompts/branding-s-prospect-website.md) | Takes the colours of a prospect's public website, makes them Nuxeo Agentic UI's default theme, and puts their name in the browser tab | Branding | Not tested yet                                                       |
| [panel-on-a-document.md](prompts/panel-on-a-document.md)                 | Adds a document panel built from platform components, registered under the customer's prefix and placed by a manifest                 | Code     | Not tested yet — published-package and live Nuxeo validation pending |

## What can be customised today

| Level         | What you can change                                                                            | Where it goes                                                                    | Today                                                                                                                   |
| ------------- | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Branding      | Colours, product name                                                                          | `bootstrap.json`, deployed by your package                                       | Supported. No logo                                                                                                      |
| Configuration | Hide, show, reorder or rename menu entries, actions, tabs and columns; show them by permission | A JSON manifest, today stored in a Nuxeo Note                                    | Supported                                                                                                               |
| Code          | Customer components placed in the documented sidebar, tabs or documentView slots               | Your own Angular extension library and host build, plus a configuration manifest | Requires the published platform package and a customer host that registers the extension provider; see the panel prompt |

## Adding a prompt

- One file in `prompts/`, named after what it does.
- Plain language, numbered steps, `<PLACEHOLDERS>` in capitals.
- Say what the agent must not touch (Nuxeo Agentic UI) and where it writes (your package).
- End with a test step that asks for screenshots and for what could not be verified.
- Add it to the table above, marked "Not tested yet" until it has been run for real.

## Support

**These features are not part of the Nuxeo Production platform.**

These solutions are provided for inspiration and we encourage customers to use them as code samples and learning
resources.

This is a moving project (no API maintenance, no deprecation process, etc.) If any of these solutions are found to be
useful for the Nuxeo Platform in general, they will be integrated directly into platform, not maintained here.

## Licence

[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)

## About Nuxeo

Nuxeo Platform is an open source highly scalable, cloud-native, enterprise content management product with rich multimedia support, written in Java. Data can be stored in both SQL & NoSQL databases.

The development of the Nuxeo Platform is mostly done by Nuxeo employees with an open development model.

The source code, documentation, roadmap, issue tracker, testing, benchmarks are all public.

More information is available at [Hyland/Nuxeo](https://www.hyland.com/en/solutions/products/nuxeo-platform).
