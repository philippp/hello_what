Objective: Maintain a single-page static webapp that allows the viewer to explore this strace readout with interactive annotations. Inline the CSS and JS, and save this file as hello_world.html

Files:
  * `hello_world.sh` - The program we are studying
  * `hello_world-strace.txt` - The strace output from running `strace ./hello_world.sh`
  * `hello_world.html` - A single-page webapp that allows the viewer to explore the strace readout
  
# Webapp Specification 

## Single-page app UX

### Fonts

The `program source` and `strace` should use the same monospace font. The Section and Line descriptions should use a serif font that balances gravitas and grace with legibility.

### Color scheme

Use a muted fall-leaves color scheme, optimized for text legibility.

### Page Layout

The page should be laid out as:

|----------------------|
|  Program    Source   |
|----------------------|
|        | section     |
| strace | description |
|----------------------|
| Line description     |
|----------------------|

## Page components

### Program source
Shows the syntax-highlighted source program (in our case, `hello_world.sh`). 

### Strace

Shows the strace log. Group the strace log into "sections" that are part of the same overall behavior (e.g. "find the 'bash' binary by looking in default locations" if the program starts with `/usr/bin/env bash`). Sections should be delineated by a horizontal solid line. Sections are selected when their lines are clicked or navigated to, and the currently selected section should have a muted bright background color. Lines are selected by clicking on them or using the up/down arrow keys, and should have a noticeably brighter background color when selected. Selecting a line also selects the section containing this line.

Clicking on a line or navigating with arrow keys should change the "selected" line to the targeted line. If the new line is part of a different section, we must also change the "selected" section to the new section. The first line should be selected automatically when the page loads.

Each line must hyperlink the function call to the appropriate http manpage. E.g. fnctl should link to `https://man7.org/linux/man-pages/man2/fcntl.2.html`


### Section Description
The first section should be selected automatically when the page loads.
Whenever a new section is selected, update the contents of this section to show:
Description of what the strace "section" is doing.
Best guess as to which part of the program is responsible for this section.

### Line description
The first line should be selected automatically when the page loads.
Whenever a new line is selected (by clicking or using arrow keys), update the contents of this section to show:
   + A description of what the line is doing in the context of the section.
   + Description of the arguments (if any)

### User Interaction
- **Click selection**: Users can click on any strace line to select it
- **Keyboard navigation**: Users can use the up and down arrow keys to navigate between lines
- **Initial state**: The first line is automatically selected when the page loads
- **Scrolling**: When navigating with arrow keys, the selected line scrolls into view