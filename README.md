[2015-02-07 MadJS presentation +madjs due:2015-02-09 profile:imdone user:piascikj](#DOING:0)

iMDone
====
1. How many of you use, have used or have seen TODO/FIXME comments in code?
2. Developers have been doing this for years, but support is lacking.  Mostly static analysis tools and light IDE support.
3. Modern dev processes use some form of task board (scrum, kanban, agile etc.) because it works!
4. I wanted to write code or documentation and manage tasks without opening other apps.
5. I wanted context for my tasks.

Task formats
----
Style          | Example
:------------- | :----------
Code Style     | <pre>// TODO This is a task</pre>
&nbsp;         | <pre>// TODO: This is a task</pre>
&nbsp;         | <pre>// TODO:5 This is a task</pre>
Hash Style     | <pre>&#35;TODO:0 This is a task</pre>
&nbsp;         | <pre>&#35;to-do:0 This is a task</pre>
Markdown Style | <pre>&#91;This is a task&#93;&#40;todo:10&#41;</pre>
  
Task syntax
----
- Code style tasks are intended to be used to capture existing tasks in code, so hash or markdown style should be used for new tasks
- Code style tasks will only be detected if the list name matches a string in the `code.include_lists` attribute in `.imdone/config.json`
- List names in code style tasks must be at least 2 uppercase letters or underscores
- In Hash and markdown style tasks **list name** can be and combination of upper and lower case letters, underscores and dashes
- In Hash and markdown style tasks the **list name** must be followed by a `:` and a number which determines sort order in the list
  - Sort numbers can be reused, in which case tasks with the same sort number will be sorted alphabetically by text.
- In code, tasks can be any style but must be in a line or block comment
  - Code style tasks are only detected in comments for files with extensions listed in [imdone-core/languages.js](https://github.com/imdone/imdone-core/blob/master/lib/languages.js)
  - When a code style task is moved, all code style tasks in affected lists are rewitten as hash style tasks
- For code and hash style tasks, the task text is terminated by the end of line
- Task text can have [todo.txt formatting](https://github.com/ginatrapani/todo.txt-cli/wiki/The-Todo.txt-Format) but not todo.txt priority
- Task text can have markdown formatting

todo.txt syntax
----
todo.txt element | Example
:------ | :------
Create date | <pre>&#35;DOING:20 2015-02-09 This task was created on 2015-02-09</pre>
Completed date | <pre>&#35;DOING:20 x 2015-02-09 2015-02-08 This task was created on 2015-02-08 and completed on 2015-02-09</pre>
Due Date | <pre>&#35;doing:20 This task is due on 2015-02-09 due:2015-02-09</pre>
Tags | <pre>&#35;doing:20 This task has a &#42;madjs&#42; tag +madjs</pre>
Metadata | <pre>&#35;doing:20 This task has profile metadata profile:piascikj</pre>

Metadata links
----
- Tasks with metadata can be linked to external resources like other task mgmt systems and websites
- Add a `meta` attribute to `.imdone/config.json`  

```javascript
  "meta": {
    "user": {
      "urlTemplate": "#filter/user:%s",
      "titleTemplate": "Filter by user:%s"
    },
    "profile": {
      "urlTemplate": "https://github.com/%s",
      "titleTemplate": "github profile for %s"
    }
  }
```

Links
----
- [iMDone - Chrome Web Store](https://chrome.google.com/webstore/detail/imdone/kchfkmdhgpibgidhdllkbgfnpmefdldl)
- [The story behind imdone](http://blog.imdone.io)


