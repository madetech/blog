# Remote Pairing

Pairing is a great way to boost productivity and help crack a particularly complex problem.

At MadeTech we try to spend 50% of our development time pairing with colleagues. We have dedicated pairing workstations, which consist of two screens mirrored: one for the driver (the person write code) and the other for the navigator.

If you'd like to know more about pairing, we have the following articles and books:

- Read Richard's excellent "[The best and worse times to pair program][link_richard_pairing]"
- There is an entire chapter dedicated to pair programming in our "[Building high performance  agile teams][link_agile_book]"

Whilst pair programming on-site is an awesome experience, it's a less than stellar experience when one or more of you are working remotely.

## The problem

We also do a lot of remote working, our current solution for remote pairing is to use screen sharing via Slack or Google Meets.

This does have some disadvantages:

- If video quality degrades sufficiently, you end up with a screen that is a mess of random pixels.
- If the audio quality degrades sufficiently, the flow of constant feedback (from the navigator) is interrupted, so is productivity. Tip: get headsets to reduce the amount of background noise that will cause distraction.
- If you're swapping roles, you either stay on the shared screen and your pairing partner's editor or you swap screen sharing. Again these are disruptions to productivity.

## The solution

Real-time collaborative editing tools! 

Instead of relaying the entire screen (as used by screen sharing), these tools send editor/keystroke telemetry.

These could potentially address all of our disadvantages relating to bandwidth and swapping roles during pairing.

We also had additional requirements which were:

- The tool must work on our varied collection of editors: Sublime Text, (Neo)vim, Emacs, Atom, ItelliJ IDEA (pycharm et al) and Visual Studio Code.
- There should be a shared terminal to provide access to specialised testing, debugging or deployment workflows.

### The shortlist

We evaluated the following solutions in the market: [Floobits][link_floobits], [Teletype][link_teletype] and [Visual Studio Live Share][link_liveshare].

Because of one of our requirements was to use native editors we immediately discounted any cloud based solutions such as [Cloud 9 IDE][link_cloud9], [CodeAnywhere][link_codeanywhere] and [CodeEnvy][link_codeenvy] who provide an integrated web based editor.

#### Floobits

Floobits is a paid service, although there is free tier to allow you try out the service. This is the only tool, that is reliant on code repositories being imported into a workspace before collaboration can begin. The editor extensions/plugins allow you to do this from within your editor.

On initial inspection Floobits appears to cover most of our requirements. They support a lot of editors (Atom, Sublime Text, Intellij, Neovim and Emacs) and provide shared terminals.

How it works (how to start collaborating)

- Signup
- Install the extension
- You import your project into a workspace (this can be done in the editor)
- You share the name of your workspace with your collaborator

Pros:

- Baked in video chat - you could use this over a separate channel via Slack or Google Meets.

Cons:

- No support for Visual Studio Code.
- Workspaces could potentially leak code if you forget to set as private.
- The synchronisation story between local and remote is not clear, on your first connection to someone elses' workspace it should be a given you want a copy of the remote files.
- The shared terminal feels janky, why prevent remote users have sending the `enter` key, but let them type on the terminal?

#### Teletype

Teletype was created by the same GitHub team behind Atom.

How it works (how to start collaborating)

- You install the extension
- Generate a github oauth token
- In the command palette enter: `Teletype: Share Portal`
- Share the portal url

Pros:

- Free

Cons:

- Atom only
- No shared terminal

#### Visual Studio's Live Share

Pros:

- Free, but a paid tier is being evaluated for the the future which would have more advanced features.
- Shared debugging - whilst not a requirement, it was nice to be able to remotely inspect the contents of the code whilst it was running.
- Shared servers - think ngrok, but baked in
- Independant exploration - the navigator could look at other parts of the code base in anticipation of new or old problems without disrupting the driver.

Cons:

- Only supports Visual Studio Code and Professional editions

### Summary

There's no clear winner, but floobit has the advantage of supporting so many editors and terminal support. The user experience of the Visual Studio Live Share was exception and just worked.

This is still a relatively new field, and improvements as well as new players will appear in the market. So we'll be revisiting this space periodically.

It would be great if this market adopted an open standards protocol, in a similar fashion to how language support in code editors and IDEs has been simplifed with the advent of [Language Support Protocol][link_lsp].

This new protocol would be responsible for sending editor and shared terminal telemtry. The market leaders could provide their own features on the server implementation, but clients would be reduced to a single extension/plugin.


[link_richard_pairing]:  https://www.madetech.com/blog/the-best-and-worst-times-to-pair-program
[link_agile_book]: https://www.madetech.com/resources/ebook/building_high_performance_agile_teams
[link_floobits]: https://floobits.com/
[link_teletype]: https://teletype.atom.io/
[link_liveshare]: https://www.visualstudio.com/services/live-share/
[link_cloud9]: https://c9.io/
[link_codeanywhere]: https://codeanywhere.com/
[link_codeenvy]: https://codenvy.com/
[link_flootty]: https://floobits.com/help/flootty
[link_lsp]: https://en.wikipedia.org/wiki/Language_Server_Protocol