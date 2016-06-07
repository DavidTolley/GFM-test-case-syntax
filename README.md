On the @github/quality team we keep our manual tests in markdown docs within the associated project repo. So the manual test manifest for GitHub Enterprise would go in: `https://github.com/github/enterprise/blob/master/tests/manifest.md`.

We developed a certain syntax for writing test cases in [GFM](https://help.github.com/categories/writing-on-github/). The benefit of this syntax is that:

- It is descriptive without being overly verbose
- It is modular
    - Groups of tests can be added, removed and rearranged easily
    - Sections are easier to navigate when executing the tests

## The syntax

### Nesting structure  

Tasks list items are used to represent a single, actionable test. Here's an example:

`- [ ] Drag an image in`

However, that single test case doesn't provide a lot of context. So we nest task list items within unordered lists as a way to create descriptive headings. Sometimes the nesting can be quite deep, depending on the hierarchy and context. An example of that nesting:

```
- Profiles
  - User profile (http://github.com/[user name])
    - Change profile picture (http://github.com/settings/profile)
      - With drag and drop
        - [ ] Drag in an image
        - [ ] Tweak crop box and save
        - [ ] Confirm that the profile picture changes
      - With the file selector dialog
        …
```

Note in the example above that we use parentheses to include extra information such as a URL. If we need to include a lot of extra information – we'll include a link to a doc somewhere else on the repo.

Using this format means that you can use nesting to separate an entire app's UI, or a feature set, into its different views/areas/boxes. You'll then be able to use a text editor to collapse these down when testing, which is super-useful for navigating around a manifest when testing.

### Placeholders

If a URL or something else is subject to change then we use a descriptive placeholder within square brackets. For example:

`- Visit https://[hostname]/setup`

### Emphasis

We like to italicise clickable UI elements such as buttons and text links. It doesn't hurt to be descriptive about clickable elements so that you're not hunting around a page for it when testing. e.g.:

`- [ ] Click the *Test email settings* button`

If there is text on a page that is being described in a test, we'll use single quotes to distinguish it. If the text is a message for the user (such as an error) we use double quotes. e.g.:

`- [ ] "There were problems creating your account." warning is shown above 'Username'`

### The test execution flow

When writing a large number of nested test cases, try to think about the flow that an end-user would take. Think about how a user might navigate around the UI and attempt to group tests together in that way. This will not only make executing test runs quicker, but also serves to highlight missing tests and increases the chance of finding issues as you act as they would.

## Bonus

A number of teams currently use [Testpad](https://ontestpad.com) for their test runs. Unfortunately Testpad doesn't support markdown rendering, but upon import it *should* convert all parent items into headings leaving only task list items (#nochildren) as actionable tests cases.
