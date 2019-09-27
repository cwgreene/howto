= How To Make a completion for a command =
== How does completion work? ==
Shell completion is handled at the shell level, so the
specific code that is invoked will be handled by the shell
in question.

`zsh` has `bash` compatibility, but others may not.

Anyhow, the way this works in bash is that when tab is hit,
readline parses the command line and works out whether a 

== Shell Compatibility ==
=== `zsh` ===
zsh has bash compatibility. Generally encouraged not to be used.
```
      bashcompinit
              This function provides compatibility  with  bash’s  programmable
              completion system.  When run it will define the functions, comp-
              gen and complete which correspond to the bash builtins with  the
              same names.  It will then be possible to use completion specifi-
              cations and functions written for bash.
```

https://stackoverflow.com/questions/3249432/can-a-bash-tab-completion-script-be-used-in-zsh

```
autoload bashcompinit
bashcompinit
source /path/to/your/bash_completion_file
```

=== `fish` ===
To be added. Maybe. I don't use `fish`.

=== Autogeneration ===
`argcomplete` for python's `argparse` works by invoking the executable, which is not a solution
I like. I'd much prefer for it to take the parser object and generate the invocation script.

Might be possible though to get this to work.

== Simple Cases ==
=== What File Do I update? ===
The only thing that is needed to be done in bash is to run the `complete` command. Typically you'll
also want to attach a special completion function as well (but a simple wordlist doesn't need that)
Ideally, you would only need to update the file in `~/.shell_setup/bash_completions.d` but this
doesn't seem to work for some reason. So instead, just update the completions file manually.

=== List of Words Only, Don't worry about placement ===
Simple!

```
complete -W 'do all the things' command_name
```

See above for shell persistence. The command name _must_ be the last thing in the line,
otherwise, it won't work.
