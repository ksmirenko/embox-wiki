These commit message agreements are based on the excellent [How to write a Git
Commit Message](http://chris.beams.io/posts/git-commit/) guide. Each rule
below helps to keep the history clean and consistent and requires zero effort
to follow once you get used to.

### The rules

 1. **Start the subject by specifying the subsystem / module**
    - For example, **`util: list: `**`Add unsafe version of list_foreach()`
  
    - Want a label? Put it after the subsystem: 
      `util: `**`(minor) `**`Fix a typo in ...`
  
    > `subsys:` is where the change belongs to: `arch`/`kernel`/`driver`/`util`/`mk`/...<br/>
    > `(label)` is what kind of change it is: `docs`/`template`/`refactor`/`minor`/`MAJOR`

 2. Use the imperative mood in the subject line
    - `Fix` instead of fix~~ing~~ / fix~~ed~~

 3. Capitalize the sentence after the subsystem / labels
    > Except for words that must be lowercased, like a module / source name.

 4. Do not end the subject line with a period
    > Except for ending a sentence with common abbreviations, *e.g. etc.*

 5. **Separate subject from body with a blank line**

 6. **Wrap the body at 72 characters**:
    [stopwritingramblingcommitmessages.com](http://stopwritingramblingcommitmessages.com)

    > Except for code blocks, long URLs, references to other commits: paste
    > these verbatim, but indent with 4 spaces and surround with empty lines.
    >
    > Keep the subject concise: 50-60 characters as a rule of thumb;
    > and again, **the hard limit is 72 characters**.

 7. Subject: **what** is changed; body: **why** that, but not **_how_** (see below)

***

#### The subject line

The first commit line — the subject — is the most important. Make it **as
specific and definite as possible**

  - The subject appears on the project feed, in the output of
    `git log --oneline`, in the tree view of `gitk`, etc. This is what a
    person sees when looking through a history in order to track changes
    to a certain topic

  - In the subject, summarize **what is actually changed**, not just the
    effect of that change. Compare:

    | Good | Bad |
    | ---- | --- |
    | *fs: Add missing 'foo -> bar' dependence*                     | *Fix build*
    | *arm/stm32: (template) Decrease thread pool size to fit RAM*  | *Fix arm/stm32 template*
    | *util: (refactor) Extract foo_check_xxx() from foo_func()*    | *util: Work on foo refactoring*

#### The message body

Use the body to **explain *what and why*, not _how_**

In most cases, you can leave out details about how a change has been made.
Just focus on making clear **the reasons you made the change** in the first
place — the way things worked before the change (and what was wrong with
that), the way they work now, and why you decided to solve it the way you did.

Whenever possible, please include references to issues or links to
discussions on the mailing list:

  - `#123` to refer an issue; `owner/repo#234` - an issue of an arbitrary
    repository

  - Use [closing keywords](https://help.github.com/articles/closing-issues-via-commit-messages/):
    *`This fixes #765 and closes #700`*; this way, once your branch gets
    merged the mentioned issues will close automatically.

### Example

To put everything together:

<table>
<tr>
<td>
<pre>
<b>subsystem: Capitalized, short summary</b>

More detailed description, if necessary. It should be wrapped to 72
characters. The blank line separating the summary from the body is
critical (unless you omit the body entirely); various tools like
`log`, `shortlog` and `rebase` can get confused if you run the two
together.

The description section can have multiple paragraphs separated with
blank lines.

Try to be as descriptive as you can. Even if you think that the
commit content is obvious, it may not be obvious to others.

    /* Code examples can be embedded by indenting them with 4 spaces.
     * This makes the whole commit message more readable. */
    int main(int argc, char **argv) {
        printf("Hello world!\n");
        return 0;
    }

You can also add bullet points:

- Typically a hyphen (-) or an asterisk (*) is used for the bullet
  point, with blank lines in between

- As always, wrap lines at 72 characters, and indent any additional
  lines with 2 spaces for better readability

Provide references to issue tracker, if any.

See also: #741 "README: Add Getting Started guide"
Closes #721 "New README and contributing guides"
</pre>
</td>
<td>
<pre>
⟵ 50-60 chars <b>subject</b>

⟵ <b>72 characters</b>
    the hard wrapping
    limit









⟵ 4-space <b>indented
    code blocks</b>
    may exceed
    the hard limit













⟵ <u>#NNN</u> references
    turn into links
</pre>
</td>
</tr></table>
