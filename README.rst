git-family
----------

Repository commit messages::

            a---b--------c----d---e     feature
           /                 /
  0---1---2---3---4---------5---6---7   master
               \
                ------z                 unrelated

- All commit a file with the same name but:

  - Commit "d" doesn't commit any file.

  - Commit "7" commits the readme.

- Refs listed in the side column.

- HEAD pointing to e (but not actually relevant).

- --oneline included to help with visualization.

- Consider adding --no-merges if needed by the use case.

(1) All commits visible from e, branching at merges following both parents)
---------------------------------------------------------------------------

Command::

 git rev-list --oneline feature

Output::

 aadd169 e
 59bb7e6 d
 9366c7a 5
 c2a24eb c
 caf2955 4
 4dd76ec b
 7191789 3
 f95deab a
 11356dd 2
 4f625fa 1
 aaeee73 0

- We see both feature and master history w/o unrelated commits.

(2) Same as (1), but following first parents
--------------------------------------------

Command::

 git rev-list --first-parent --oneline feature

Output::

 aadd169 e
 59bb7e6 d
 c2a24eb c
 4dd76ec b
 f95deab a
 11356dd 2
 4f625fa 1
 aaeee73 0

- We only see history of 'feature' but commits before first merge are
  included even if they are not in 'feature'.

- Because commit "a" doesn't know about branches, "2" is the first parent
  from its point of view.

(3) Same as (1), but remove commits visible from master
-------------------------------------------------------

Command::

 git rev-list --oneline feature ^master

Output::

 aadd169 e
 59bb7e6 d
 c2a24eb c
 4dd76ec b
 f95deab a

- This works as if they were sets and you substract one from another.

Shorthand for ^ syntax if HEAD in e::

 git rev-list --oneline master..

Voila!
