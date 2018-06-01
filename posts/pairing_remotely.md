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
- The new alternatives:
  - Floobits
    - Pros: 
      - supports a lot of editors (atom, sublime text, intellj, vim and emacs)
      - terminal support
    - Cons: requires storing of "shared" workspaces
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

 at Madetech we try to spend at least 50% pairing with colleagues. We have dedicated pairing workstations. Where there are two screens one for the driver and one for the navigator.


## Further Reading

- Read Richard's excellent https://www.madetech.com/blog/the-best-and-worst-times-to-pair-program
- Read the book: https://www.madetech.com/resources/ebook/building_high_performance_agile_teams
- https://teletype.atom.io/
- https://floobits.com/