# Nuxeo Agentic UI — prompt library

Ready-to-use prompts to customise [Nuxeo Agentic UI](https://github.com/nuxeo/agentic-ui-poc)
(product name: Nuxeo Satori) with an AI coding agent such as Claude Code, without writing the
code yourself.

> [!CAUTION]
> Nuxeo Agentic UI / Nuxeo Satori is **Work in progress**, Satori is in Beta and a lot of things
> can change.

## Principles

- **You prompt, the agent builds.** Each prompt describes one customisation in plain
  language. The agent does the work and shows you the result.
- **Satori is never modified.** The agent reads Satori's source to learn how it works and
  writes everything into your own Nuxeo package, so upgrading Satori stays a version bump.
- **The result is a marketplace package.** That is how Nuxeo deploys configuration, so
  that is what every prompt produces or adds to.
- **One prompt, one customisation.** Small prompts are easier to tune, test and combine.
- **Proof, not promises.** Every prompt asks the agent to test its result, show
  screenshots, and say what it could not verify.

## How to use

1. **Get Satori's source.** Clone or fork <https://github.com/nuxeo/agentic-ui-poc>. The
   agent only reads it.
2. **Create your Nuxeo package project**, with Nuxeo CLI or by asking your agent to
   scaffold an empty marketplace package that depends on `nuxeo-agentic-ui`.
3. **Start your agent session from that package folder**, and give it read access to
   Satori's folder: `claude --add-dir /path/to/agentic-ui-poc` in the terminal, or add the
   folder to the session in the desktop app.
4. **Pick a prompt** in [`prompts/`](prompts) and replace its `<PLACEHOLDERS>`: customer
   name, Satori's path, the target path in your package… Tune the rest if needed.
5. **Paste it** into the session. Answer the agent's questions and review what it changed.
6. **Build, deploy, test.** Build the package, install it on your Nuxeo server
   (`nuxeoctl mp-install`) and check the result in the browser. For a quick check before
   packaging, a prompt can also copy its file straight into your local Nuxeo.

## Prompts

| Prompt                                                                    | What it does                                                                                                         | Level    | Status         |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------- | -------------- |
| [branding-s-prospect-website.md](prompts/branding-s-prospect-website.md) | Takes the colours of a prospect's public website, makes them Satori's default theme, and puts their name in the browser tab | Branding | Not tested yet |

## What can be customised today

| Level         | What you can change                                                                             | Where it goes                                    | Today                                                                         |
| ------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------ | ----------------------------------------------------------------------------- |
| Branding      | Colours, product name                                                                           | `bootstrap.json`, deployed by your package       | Supported. No logo                                                            |
| Configuration | Hide, show, reorder or rename menu entries, actions, tabs and columns; show them by permission | A JSON manifest, today stored in a Nuxeo Note    | Supported                                                                     |
| Code          | Layouts for your own document types, search forms, new screens                                  | Your own Angular code                            | Not yet: custom fields are not shown or editable, and adding code means forking Satori |

## Adding a prompt

- One file in `prompts/`, named after what it does.
- Plain language, numbered steps, `<PLACEHOLDERS>` in capitals.
- Say what the agent must not touch (Satori) and where it writes (your package).
- End with a test step that asks for screenshots and for what could not be verified.
- Add it to the table above, marked "Not tested yet" until it has been run for real.
