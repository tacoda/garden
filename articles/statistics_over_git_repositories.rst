Statistics over Git Repositories
================================

Get the revision list.

..code: bash

   git rev-list HEAD

Notice that the commits are in order of newest to oldest.

..code: bash

   git log -1

Reverse the rev list.

..code: bash

   git rev-list --reverse HEAD

Now listing oldest to newest.

We need to loop to get information and print things:

..code: bash

   git rev-list --reverse HEAD | while read rev; do git log -1 $rev; done

This command duplicates the output of ``git log``.

..code: bash

   git rev-list --reverse HEAD | while read rev; do git ls-tree $rev; done
   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree $rev; done
   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev; done
   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev | awk '{print $3}'; done

``awk`` is a very complex tool that is really useful for grabbing fields out of text.

``git show`` with a file blob will show the contents of that file as of that revision.
We need to be able to grab hashes to pass as arguments. We will do this with =xargs=.

..code: bash

   echo '1
   2
   3'

   echo '1
   2
   3' | xargs

This solves the problem of mapping stdout to arguments.

..code: bash

   echo '1
   2
   3' | xargs ls

..code: bash

   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev | awk '{print $3}' | xargs git show | cat; done
   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev | awk '{print $3}' | xargs git show | cat; done | view -

Pipe to ``cat`` because otherwise ``git`` will page the output.

Pipe the whole thing to ``view``, which is a view-only vim.
Or we could use ``less``.

**Note:**

..epigraph:

   Here we are performing a command, piping it into a control structure,
   and then piping it into another command.

   Control structures have a stdin and stdout, just like anything else.

Starting from that and removing the output commands to pipe it into another command.
Use it to count the number of lines.

..code: bash

   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev | awk '{print $3}' | xargs git show; done
   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev | awk '{print $3}' | xargs git show | wc -l; done

To fix the log output, but that will involve a lot of =M-b=.
This is a smell that you need a script instead of a one-liner.

*Turn into a script*

..code: bash

   touch stats.sh
   chmod u+x stats.sh

``stats.sh``

Copy command into the script. Add a shebang.

..code: bash

   #!/bin/bash

   git rev-list --reverse HEAD | while read rev; do echo; echo REV $rev; git ls-tree -r $rev | awk '{print $3}' | xargs git show | wc -l; done

Add error flag and break the command up into separate lines.

..code: bash

   #!/bin/bash
   set -e # If any command in the script fails, then abort the rest of the script.

   git rev-list --reverse HEAD |
   while read rev; do
   echo
   echo REV $rev
   git ls-tree -r $rev |
   awk '{print $3}' |
   xargs git show |
   wc -l
   done



