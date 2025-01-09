---
title: org.el notes
---
# Introduction

> Commentary:
>
> Org is a mode for keeping notes, maintaining ToDo lists, and doing
> project planning with a fast and effective plain-text system.
>
> Org mode develops organizational tasks around NOTES files that
> contain information about projects as plain text.  Org mode is
> implemented on top of outline-mode, which makes it possible to keep
> the content of large files well structured.  Visibility cycling and
> structure editing help to work with the tree.  Tables are easily
> created with a built-in table editor.  Org mode supports ToDo
> items, deadlines, time stamps, and scheduling.  It dynamically
> compiles entries into an agenda that utilizes and smoothly
> integrates much of the Emacs calendar and diary.  Plain text
> URL-like links connect to websites, emails, Usenet messages, BBDB
> entries, and any files related to the projects.  For printing and
> sharing of notes, an Org file can be exported as a structured ASCII
> file, as HTML, or (todo and agenda items only) as an iCalendar
> file.  It can also serve as a publishing tool for a set of linked
> webpages.
>
> - <cite>[Carsten Dominik](../lisp/org.el)</cite>

Org mode is implemented on top of outline-mode. 
It uses visibility cycling and structure editing.
Built in table editor.
ToDo items, including:
  - deadlines
  - time stamps
  - scheduling
Agenda System
Linking System
Exporting System
Publishing System

# Dependencies

- org-compat
- org-loaddefs
- org-macs
- org-keys
- ol
- oc
- org-table
- org-fold
- org-cycle

# Customisation sets

## org-startup-truncated

Non-nil means entering Org mode will set 'truncate-lines'. This is useful
since some lines containing links can be very long and uninteresting. Also
tables look terrible when wrapped.

The variable 'org-startup-truncated' enables you to configure truncation for
Org mode different to the other modes that use the variable 'truncate-lines'
and as a shortcut instead of putting the variable 'truncate-lines' into the
'org-mode-hook'.  If one wants to configure truncation for Org mode not
statically but dynamically e.g. in a hook like 'ediff-prepare-buffer-hook'
then the variable 'truncate-lines' has to be used because in such a case it is
too late to set the variable 'org-startup-truncated'.

## org-startup-folded

Initial folding state of headings when entering Org mode.

Allowed values are:

symbol 'nofold'

  Do not fold headings.

symbol 'fold'

  Fold everything, leaving only top-level headings visible.

symbol 'content'

  Leave all the headings and sub-headings visible, but hide their text. This
  is an equivalent of table of contents.

symbol 'show2levels', 'show3levels', 'show4levels', 'show5levels'

  Show headings up to Nth level.

symbol 'showeverything' (default)

  Start Org mode in fully unfolded state.  Unlike all other allowed values,
  this value prevents drawers, blocks, and archived subtrees from being folded
  even when 'org-cycle-hide-block-startup', 'org-cycle-open-archived-trees',
  or 'org-cycle-hide-drawer-startup' are non-nil.  Per-subtree visibility
  settings (see manual node '(org)Initial visibility)') are also ignored.

This can also be configured on a per-file basis by adding one of the following
lines anywhere in the buffer:

   #+STARTUP: fold              (or 'overview', this is equivalent)
   #+STARTUP: nofold            (or 'showall', this is equivalent)
   #+STARTUP: content
   #+STARTUP: show<n>levels (<n> = 2..5)
   #+STARTUP: showeverything

Set 'org-agenda-inhibit-startup' to a non-nil value if you want to ignore this
option when Org opens agenda files for the first time.

Default: showeverything

## org-loop-over-headlines-in-active-region

Shall some commands act upon headlines in the active region?

When set to t, some commands will be performed in all headlines within the
active region.

When set to 'start-level', some commands will be performed in all headlines
within the active region, provided that these headlines are of the same level
than the first one.

When set to a string, those commands will be performed on the matching
headlines within the active region. Such string must be a tags/property/todo
match as it is used in the agenda tags view.

The list of commands is: 'org-schedule', 'org-deadline', 'org-todo',
'org-set-tags-command', 'org-archive-subtree', 'org-archive-set-tag',
'org-toggle-archive-tag' and 'org-archive-to-archive-sibling'. The archiving
commands skip already archived entries.

See 'org-agenda-loop-over-headlines-in-active-region' for the equivalent
option for agenda views.

## org-support-shift-select

Non-nil means make shift-cursor commands select text when possible.

In Emacs 23, when 'shift-select-mode' is on, shifted cursor keys start
selecting a region, or enlarge regions started in this way. In Org mode, in
special contexts, these same keys are used for other purposes, important
enough to compete with shift selection. Org tries to balance these needs by
supporting 'shift-select-mode' outside these special contexts, under control
of this variable.

The default of this variable is nil, to avoid confusing behavior.  Shifted
cursor keys will then execute Org commands in the following contexts:
- on a headline, changing TODO state (left/right) and priority (up/down)
- on a time stamp, changing the time
- in a plain list item, changing the bullet type
- in a property definition line, switching between allowed values
- in the BEGIN line of a clock table (changing the time block).
- in a table, moving the cell in the specified direction. Outside these
contexts, the commands will throw an error.

When this variable is t and the cursor is not in a special context, Org mode
will support shift-selection for making and enlarging regions. To make this
more effective, the bullet cycling will no longer happen anywhere in an item
line, but only if the cursor is exactly on the bullet.

If you set this variable to the symbol 'always', then the keys
will not be special in headlines, property lines, item lines, and
table cells, to make shift selection work there as well. If this is
what you want, you can use the following alternative commands:

org-todo and org-priority

to change TODO state and priority,

C-u C-u org-todo

can be used to switch TODO sets,

org-ctrl-c-minus

to cycle item bullet types, and properties can be edited by
hand or in column view.

However, when the cursor is on a timestamp, shift-cursor commands will still
edit the time stamp - this is just too good to give up.

## org-modules {:custom-set}

Modules that should always be loaded together with org.el.

If a description starts with <C>, the file is not part of Emacs and Org mode,
so loading it will require that you have properly installed org-contrib
package from NonGNU Emacs Lisp Package Archive
https://elpa.nongnu.org/nongnu/org-contrib.html

You can also use this system to load external packages (i.e. neither Org core
modules, nor org-contrib modules). Just add symbols to the end of the list. If
the package is called org-xyz.el, then you need to add the symbol `xyz', and
the package must have a call to:

   (provide \\='org-xyz)

For export specific modules, see also `org-export-backends'.

| bbdb              | Links to BBDB entries ol-bbdb                                  |
| bibtex            | Links to BibTeX entries ol-bibtex                              |
| crypt             | Encryption of subtrees org-crypt                               |
| ctags             | Access to Emacs tags with links org-ctags                      |
| docview           | Links to Docview buffers ol-docview                            |
| doi               | Links to DOI references ol-doi                                 |
| eww               | Store link to URL of Eww ol-eww                                |
| gnus              | Links to GNUS folders/messages ol-gnus                         |
| habit             | Track your consistency with habits org-habit                   |
| id                | Global IDs for identifying entries org-id                      |
| info              | Links to Info nodes ol-info                                    |
| inlinetask        | Tasks independent of outline hierarchy org-inlinetask          |
| irc               | Links to IRC/ERC chat sessions ol-irc                          |
| mhe               | Links to MHE folders/messages ol-mhe                           |
| mouse             | Additional mouse support org-mouse                             |
| protocol          | Intercept calls from emacsclient org-protocol                  |
| rmail             | Links to RMAIL folders/messages ol-rmail                       |
| tempo             | Fast completion for structures org-tempo                       |
| w3m               | Special cut/paste from w3m to Org mode. ol-w3m                 |
| eshell            | Links to working directories in Eshell ol-eshell               |
| annotate-file     | Annotate a file with Org syntax org-annotate-file              |
| bookmark          | Links to bookmarks ol-bookmark                                 |
| checklist         | Extra functions for checklists in repeated tasks org-checklist |
| choose            | Use TODO keywords to mark decisions states org-choose          |
| collector         | Collect properties into tables org-collector                   |
| depend            | TODO dependencies for Org mode (partially obsolete)             |
| elisp-symbol      | Links to emacs-lisp symbols ol-elisp-symbol                    |
| eval-light        | Evaluate inbuffer-code on demand org-eval-light                |
| eval              | Include command output as text org-eval                        |
| expiry            | Expiry mechanism for Org entries org-expiry                    |
| git-link          | Links to specific file version ol-git-link                     |
| interactive-query | Interactive modification of tags query (partially obsolete)     |
| invoice           | Help manage client invoices in Org mode org-invoice            |
| learn             | SuperMemo's incremental learning algorithm org-learn           |
| mac-iCal          | Imports events from iCal.app to the Emacs diary org-mac-iCal   |
| mac-link          | Grab links and url from various mac Applications org-mac-link  |
| mairix            | Hook mairix search into Org for different MUAs org-mairix      |
| man               | Links to man pages in Org mode ol-man                          |
| mew               | Links to Mew folders/messages ol-mew                           |
| notify            | Notifications for Org mode org-notify                          |
| notmuch           | Provide Org links to notmuch searches or messages ol-notmuch   |
| panel             | Simple routines for us with bad memory org-panel               |
| registry          | A registry for Org links org-registry                          |
| screen            | Visit screen sessions through links org-screen                 |
| screenshot        | Take and manage screenshots in Org files org-screenshot        |
| secretary         | Team management with Org org-secretary                         |
| sqlinsert         | Convert Org tables to SQL insertions orgtbl-sqlinsert          |
| toc               | Table of contents for Org buffer org-toc                       |
| track             | Keep up with Org mode development org-track                    |
| velocity          | Something like Notational Velocity for Org org-velocity        |
| vm                | Links to VM folders/messages ol-vm                             |
| wikinodes         | CamelCase wiki-like links org-wikinodes                        |
| wl                | Links to Wanderlust folders/messages ol-wl                     |

## org
Group

Outline-based notes management and organizer.

Tag: Org
Group: outlines
Group: calendar

## org-clone-delete-id

Remove ID property of clones of a subtree. When non-nil, clones of a subtree
don't inherit the ID property. Otherwise they inherit the ID property with a
new unique identifier.

## org-babel-load-languages

This is a map of languages and booleans, the true elements are the
languages to enable babeling.

Parameter: org-mode-map, list of language and boolean pairs.

# Constants

## org-log-buffer-setup-hook

Hook that is run after an Org log buffer is created.

## org-load-hook

Obsolete

Hook that is run after org.el has been loaded.

## org-mode-hook

Mode hook for Org mode, run after the mode was turned on.

## org-effort-property

The property that is being used to keep track of effort estimates. Effort
estimates given in this property need to be in the format defined in
org-duration.el.

Value: "Effort"

## org-latex-regexps

Regular expressions for matching embedded LaTeX.

Value: 
  '(("begin" "^[ \t]*\\(\\\\begin{\\([a-zA-Z0-9\\*]+\\)\\(?:.\\|\n\\)+?\\\\end{\\2}\\)" 1 t)
    ;; ("$" "\\([ \t(]\\|^\\)\\(\\(\\([$]\\)\\([^ \t\n,.$].*?\\(\n.*?\\)\\{0,5\\}[^ \t\n,.$]\\)\\4\\)\\)\\([ \t.,?;:'\")]\\|$\\)" 2 nil)
    ("$1" "\\([^$]\\|^\\)\\(\\$[^ \t\r\n,;.$]\\$\\)\\(\\s.\\|\\s-\\|\\s(\\|\\s)\\|\\s\"\\|'\\|$\\)" 2 nil)
    ("$"  "\\([^$]\\|^\\)\\(\\(\\$\\([^ \t\n,;.$][^$\n\r]*?\\(\n[^$\n\r]*?\\)\\{0,2\\}[^ \t\n,.$]\\)\\$\\)\\)\\(\\s.\\|\\s-\\|\\s(\\|\\s)\\|\\s\"\\|'\\|$\\)" 2 nil)
    ("\\(" "\\\\(\\(?:.\\|\n\\)*?\\\\)" 0 nil)
    ("\\[" "\\\\\\[\\(?:.\\|\n\\)*?\\\\\\]" 0 nil)
    ("$$" "\\$\\$\\(?:.\\|\n\\)*?\\$\\$" 0 nil))

## org-comment-string

Entries starting with this keyword will never be exported.

Value: "COMMENT"

## org-tag-line-re

Regexp matching tags in a headline. Tags are stored in match group 1. Match
group 2 stores the tags without the enclosing colons.

Value: "^\\*+ \\(?:.*[ \t]\\)?\\(:\\([[:alnum:]_@#%:]+\\):\\)[ \t]*$"

## org-tag-group-re

Regexp matching the tag group at the end of a line, with leading spaces. Tags
are stored in match group 1. Match group 2 stores the tags without the
enclosing colons.

Value: "[ \t]+\\(:\\([[:alnum:]_@#%:]+\\):\\)[ \t]*$"

## org-tag-re

Regexp matching a single tag.

Value: "[[:alnum:]_@#%]+"

## org-archive-tag

The tag that marks a subtree as archived. An archived subtree does not open
during visibility cycling, and does not contribute to the agenda listings.

Value: "ARCHIVE"

## org-heading-keyword-maybe-regexp-format

Printf format for a regexp matching a headline, possibly with some keyword.
This regexp can match any headline with the specified keyword, or without a
keyword. The keyword isn't in any group by default, but the stars and the body
are.

Value: "^\\(\\*+\\)\\(?: +%s\\)?\\(?: +\\(.*?\\)\\)?[ \t]*$"

## org-heading-keyword-regexp-format

Printf format for a regexp matching a headline with some keyword. This regexp
will match the headline of any node which has the exact keyword that is put
into the format. The keyword isn't in any group by default, but the stars and
the body are.

Value: "^\\(\\*+\\)\\(?: +%s\\)\\(?: +\\(.*?\\)\\)?[ \t]*$"

## org-clock-drawer-re

Matches an entire clock drawer.

Value: (concat "\\(" org-clock-drawer-start-re "\\)\\(?:.\\|\n\\)*?\\("
	  org-clock-drawer-end-re "\\)\n?")

## org-property-drawer-re

Matches an entire property drawer.

Value: 
  (concat "^[ \t]*:PROPERTIES:[ \t]*\n"
	  "\\(?:[ \t]*:\\S-+:\\(?:[ \t].*\\)?[ \t]*\n\\)*?"
	  "[ \t]*:END:[ \t]*$")

## org-logbook-drawer-re

Matches an entire LOGBOOK drawer.

Value: 
```lisp
  (rx (seq bol (0+ (any "\t ")) ":LOGBOOK:" (0+ (any "\t ")) "\n"
	   (*? (0+ nonl) "\n")
	   (0+ (any "\t ")) ":END:" (0+ (any "\t ")) eol))
```
Creates a regex matching

- beginning of line 
- zero or more tabs or spaces
- ":LOGBOOK:" string
- zero or more tabs or spaces
- newline character
- any number of
  - zero or more not-newline characters
  - newline character
- zero or more tabs or spaces
- ":END:" string
- zero or more tabs or spaces
- end of line

## org-clock-drawer-end-re

Regular expression matching the last line of a clock drawer.

Value: "^[ \t]*:END:[ \t]*$"

## org-clock-drawer-start-re

Regular expression matching the first line of a clock drawer.

Value: "^[ \t]*:CLOCK:[ \t]*$"

## org-property-end-re

Regular expression matching the last line of a property drawer.

Value: "^[ \t]*:END:[ \t]*$"

## org-property-start-re

Regular expression matching the first line of a property drawer.

Value: "^[ \t]*:PROPERTIES:[ \t]*$"

## org-drawer-regexp

Matches first or last line of a hidden block. Group 1 contains drawer's name
or \

### Inline note

FIXME: Duplicate of org-element-drawer-re

## org-all-time-keywords

List of time keywords.

Value: org-scheduled-string, org-deadline-string, org-clock-string, org-closed-string

## org-keyword-time-not-clock-regexp

Matches any of the 3 keywords, together with the time stamp.

Value: (concat
   "\\<"
   (regexp-opt
    (list org-scheduled-string org-deadline-string org-closed-string) t)
   " *[[<]\\([^]>]+\\)[]>]")

## org-keyword-time-regexp

Matches any of the 4 keywords, together with the time stamp.

Value: (concat "\\<"
	  (regexp-opt
	   (list org-scheduled-string org-deadline-string org-closed-string
		 org-clock-string)
	   t)
	  " *[[<]\\([^]>]+\\)[]>]")

## org-closed-time-regexp

Matches the CLOSED keyword together with a time stamp.

Value: (concat "\\<" org-closed-string " *\\[\\([^]]+\\)\\]")

## org-scheduled-time-hour-regexp

Matches the SCHEDULED keyword together with a time-and-hour stamp.

Value: (concat "\\<" org-scheduled-string
	  " *<\\([^>]+[0-9]\\{1,2\\}:[0-9]\\{2\\}[0-9+:hdwmy/ \t.-]*\\)>")

## org-scheduled-time-regexp

Matches the SCHEDULED keyword together with a time stamp.

Value: (concat "\\<" org-scheduled-string " *<\\([^>]+\\)>")

## org-scheduled-regexp

Matches the SCHEDULED keyword.

Value: (concat "\\<" org-scheduled-string)

## org-deadline-time-hour-regexp

Matches the DEADLINE keyword together with a time-and-hour stamp.

Value: " *<\\([^>]+[0-9]\\{1,2\\}:[0-9]\\{2\\}[0-9+:hdwmy/ \t.-]*\\)>"

## org-deadline-regexp

Matches the DEADLINE keyword.

Value: (concat "\\<" org-deadline-string)

## org-deadline-time-regexp
Matches the DEADLINE keyword together with a time stamp.

Value: (concat "\\<" org-deadline-string " *<\\([^>]+\\)>")

## org-ds-keyword-length

Maximum length of the DEADLINE and SCHEDULED keywords.

Value: Calculated as two more that largest string in the set
(org-deadline-string, org-schedule-string, org-clock-string, and
org-closed-string)

``` clojure
(->> [org-deadline-string 
      org-scheduled-string 
      org-clock-string 
      org-closed-string]
    (map length)
    (reduce max)
    (+ 2))
```
Note: this constant is defined from variable values. Seems like a potential
issue.

## org-planning-line-re

Matches a line with planning info. Matched keyword is in group 1.

Value: 
```lisp
(concat "^[ \t]*" 
    (regexp-opt
	   (list org-closed-string org-deadline-string org-scheduled-string)
	   t))
```

## org-timestamp-formats

Formats 'format-time-string' which are used for time stamps.

The value is a cons cell containing two strings.  The 'car' and 'cdr' of the
cons cell are used to format time stamps that do not and do contain time,
respectively.

Leading \"<\"/\"[\" and trailing \">\"/\"]\" pair will be stripped from the
format strings.

Also, see 'org-time-stamp-format'.

Value: ("%Y-%m-%d %a" . "%Y-%m-%d %a %H:%M")

## org-clock-string

String used as prefix for timestamps clocking work hours on an item.

Value: "CLOCK:"

## org-version

## org-comment-regexp

Regular expression for comment lines.

Value: (seq bol (zero-or-more (any "\t ")) "#" (or " " eol))

## org-keyword-regexp

Regular expression for keyword-lines.

Value: "^[ \t]*#\\+\\(\\S-+?\\):[ \t]*\\(.*\\)$"

## org-block-regexp

Regular expression for hiding blocks.

Value: "^[ \t]*#\\+begin_?\\([^ \n]+\\)\\(\\([^\n]+\\)\\)?\n\\(\\(?:.\\|\n\\)+?\\)#\\+end_?\\1[ \t]*$"

## org-dblock-start-re

Matches the start line of a dynamic block, with parameters.

Value: "^[ \t]*#\\+\\(?:BEGIN\\|begin\\):[ \t]+\\(\\S-+\\)\\([ \t]+\\(.*\\)\\)?"

## org-dblock-end-re

Matches the end of a dynamic block.

Value: "^[ \t]*#\\+\\(?:END\\|end\\)\\([: \t\r\n]\\|$\\)"

## org-ts--internal-regexp

Regular expression matching the innards of a time stamp.

Value: (seq
       (= 4 digit) "-" (= 2 digit) "-" (= 2 digit)
       (optional " " (*? nonl)))

## org-ts-regexp

Regular expression for fast time stamp matching.

Value: (format "<\\(%s\\)>" org-ts--internal-regexp)

## org-ts-regexp-inactive

Regular expression for fast inactive time stamp matching.

Value: (format "\\[\\(%s\\)\\]" org-ts--internal-regexp)

## org-ts-regexp-both

Regular expression for fast time stamp matching.

Value: (format "[[<]\\(%s\\)[]>]" org-ts--internal-regexp)

## org-ts-regexp0

Regular expression matching time strings for analysis. This one does not
require the space after the date, so it can be used on a string that
terminates immediately after the date.

Value: "\\(\\([0-9]\\{4\\}\\)-\\([0-9]\\{2\\}\\)-\\([0-9]\\{2\\}\\)\\( +[^]+0-9>\r\n -]+\\)?\\( +\\([0-9]\\{1,2\\}\\):\\([0-9]\\{2\\}\\)\\)?\\)"

## org-ts-regexp1

Regular expression matching time strings for analysis.

Value: "\\(\\([0-9]\\{4\\}\\)-\\([0-9]\\{2\\}\\)-\\([0-9]\\{2\\}\\)\\(?: *\\([^]+0-9>\r\n -]+\\)\\)?\\( \\([0-9]\\{1,2\\}\\):\\([0-9]\\{2\\}\\)\\)?\\)"

## org-ts-regexp2

Regular expression matching time stamps, with groups.

Value: (concat "<" org-ts-regexp1 "[^>\n]\\{0,16\\}>")

## org-ts-regexp3

Regular expression matching time stamps (also [..]), with groups.

Value: (concat "[[<]" org-ts-regexp1 "[^]>\n]\\{0,16\\}[]>]")

## org-tr-regexp

Regular expression matching a time stamp range.

Value: (concat org-ts-regexp "--?-?" org-ts-regexp)

## org-tr-regexp-both

Regular expression matching a time stamp range.

Value: (concat org-ts-regexp-both "--?-?" org-ts-regexp-both)

## org-tsr-regexp

Regular expression matching a time stamp or time stamp range.

Value: (concat org-ts-regexp "\\(--?-?" org-ts-regexp "\\)?")

## org-tsr-regexp-both

Regular expression matching a time stamp or time stamp range. The time stamps
may be either active or inactive.

Value: (concat org-ts-regexp-both "\\(--?-?" org-ts-regexp-both "\\)?")

## org-repeat-re

Regular expression for specifying repeated events. After a match, group 1
contains the repeat expression.

Value: "<[0-9]\\{4\\}-[0-9][0-9]-[0-9][0-9] [^>\n]*?\\([.+]?\\+[0-9]+[hdwmy]\\(/[0-9]+[hdwmy]\\)?\\)"

Note: It might not work, it was a multi-line in the original code

# Functions

## org-set-modules

Set VAR to VALUE and call `org-load-modules-maybe' with the force flag.

They note a issue with circular dependencies in loading all the modules. And
this being called if some core modules are not loaded initially. I think this
wont directly be an issue, as the modules system in nvim is likely very
different.

## org-load-modules-maybe

Load all extensions listed in org-modules.

## org-version

Show the Org version. Interactively, or when MESSAGE is non-nil, show it in
echo area. With prefix argument, or when HERE is non-nil, insert it at point.
In non-interactive uses, a reduced version string is output unless FULL is
given.

## org-global-cycle 

Alias: org-cycle/org-cycle-global

## org-overview 

Alias: org-cycle/org-cycle-overview

## org-content

Alias: org-cycle/org-cycle-content

## org-reveal 

Alias: org-cycle/org-fold-reveal

## org-force-cycle-archived

Alias: org-cycle/org-cycle-force-archived

## org-babel-do-load-languages

Load the languages defined in 'org-babel-load-languages'.

## org-babel-load-file

Load Emacs Lisp source code blocks in the Org FILE. This function
exports the source code using 'org-babel-tangle' and then loads the resulting
file using 'load-file'. With optional prefix argument COMPILE, the tangled
Emacs Lisp file is byte-compiled before it is loaded.

# Vars

## org-export-registered-backends

From ox.el

## org-modules-loaded

Have the modules been loaded already?

## org-modules

List of loaded/autoload modules. See customization set [org-modules](#org-modules-custom-set)

## org-closed-string

String used as the prefix for timestamps logging closing a TODO entry.

Value: "CLOSED:"

## org-deadline-string

String to mark deadline entries.

A deadline is this string, followed by a time stamp. It must be a word,
terminated by a colon.

Value: "DEADLINE:"

## org-scheduled-string

String to mark scheduled TODO entries.

A schedule is this string, followed by a time stamp. It must be a word,
terminated by a colon.

Value: "SCHEDULED:"

## org-time-stamp-formats

Alias: org-timestamp-formats

## org-outline-regexp

Regexp to match Org headlines.

Value: "\\*+ "

## org-outline-regexp-bol

Regexp to match Org headlines. This is similar to `org-outline-regexp'
but additionally makes sure that we are at the beginning of the line.

Value: "^\\*+ "

## org-heading-regexp

Matches a headline, putting stars and text into groups. Stars are put
in group 1 and the trimmed body in group 2.

Value: "^\\(\\*+\\)\\(?: +\\(.*?\\)\\)?[ \t]*$"

Result: [ stars rest ]

