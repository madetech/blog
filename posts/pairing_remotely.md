# Remote Pairing

## Outline

- The problem
  - How we do pairing on-site
- The current solution
  - Screen sharing
    - Gui - Slack or Google Meets)
      - Pros: Zero install/setup (if you have Slack or Google Meets already installed)
      - Cons: Having to swap screens or use the other person's editor if you're swapping pairs.
    - Terminal - tmux
      - Pros: Highly responsive, lower bandwidth requirements.
      - Cons: Not friendly to non-Vim or emacs users
- The specialised alternatives:
  - Our requirements
    - Must work on a regular editor like Sublime Text, (Neo)vim, Emacs, Atom, ItelliJ IDEA (pycharm et al) or Visual Studio Code.
      - Which is why we excluded cloud based IDEs like cloud 9, codeanywhere or codeenvy.
    - Shared terminal access to provide access to specialised testing, debugging or deployment workflows.
  - Floobits
    - Details
      - Free trial tier, but with pricing tiers based on the number of private workspaces. Workspaces are centralized storage managed by Floobits that enable collaboration. These workspaces have one or more projects linked to them. 
    - How it works
      - Signup
      - You install the extension
    - Pros:
      - Supports a lot of editors (atom, sublime text, intellj, vim and emacs)
      - built-in video chat
    - Cons:
      - Confusing UX
      - Synchronisation story between local and remote is not clear (loss of data)
      - Setup per project requires importing of repo into a workspace
    - Trivia: code roulette
  - Teletype
    - How it works
      - You install the extension
      - Generate a github oauth token
      - You share the teletype portal url
    - Pros:
      - Free
    - Cons:
      - atom only
      - no shared debugger, test runner or terminal.
  - Visual Studio's Live Share
    - I used Visual Studio Code and the insider edition to test.
    - How it works
      - You install the extension
      - Signin using Live or Github
      - Share the project you're currently in
      - Send pairing partner the sharing URL
    - Pros:
      - Shared debugging
      - Shared terminal
      - Ability to nudge someone (follow me), to avoid voice chat (kinda goes against pairing)
    - Cons: 
      - Visual Studio Code and Pro only.
      - No shared test runner, this is probably a limitation of the Visual Studio Code's UI and the lack of a built in tester means this cannot be easily shared. A workaround is to use a console test runner in a shared terminal.
  - Summary
    - There's no clear winner, but floobit has the advantage of supporting so many editors and terminal support. Ideally we should adopt something similar to Language Support Protocol, a common protocol that allows us to share editor changes and allow the editor to implement.

### The problem

At MadeTech we try to spend at least 50% of our development time pairing with colleagues. We have dedicated pairing workstations, which consist of two screens mirrored one for the driver and the other for the navigator.

We also do a lot of remote working, our current solution for remote pairing is to use screen sharing via Slack or Google Meets.

This does have disadvantages:

- If video quality degrades sufficiently, you end up with a screen that is a mess of random pixels.
- If the audio quality degrades sufficiently, the flow of constant feedback is interrupted, so is productivity. Tip: get headsets to reduce the amount of background noise that will cause distraction.
- If you're swapping roles, you either stay on the shared screen and your pairing partner's editor or you swap screen sharing. Again these are disruptions to productiivity.

### The Solution

Specialised collaboration tools!

Our requirements were:

- The tool must work on a regular editor like Sublime Text, (Neo)vim, Emacs, Atom, ItelliJ IDEA (pycharm et al) or Visual Studio Code. We have a varied collection of editors or our own customisations.
- Shared terminal access to provide access to specialised testing, debugging or deployment workflows.


## Further Reading

- Read Richard's excellent https://www.madetech.com/blog/the-best-and-worst-times-to-pair-program
- Read the book: https://www.madetech.com/resources/ebook/building_high_performance_agile_teams
- https://teletype.atom.io/
- https://floobits.com/