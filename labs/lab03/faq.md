---
layout: page
title: "FAQ - Lab 03: Debugging & Test-Driven Development"
categories: lab
released: false
searchable: true
---

## I'm getting merge conflicts after re-pulling the skeleton

First, add and commit your local changes so that `git status` reads that your working
tree is clean.

Then, refer to the [Git WTFs](../../guides/git/wtfs) section on resolving merge
conflicts. You'll need to incorporate both your local changes (this likely
includes your `BombMain` passwords) and the bug fixes
from the skeleton.

After you've resolved the merge conflicts in the files, you'll need to re-add and commit them
to complete the merge.

Come into office hours or lab if you're unsure on what to do!


## There's a lot of red in my IntelliJ

First, be sure you've imported the libraries correctly. Refer back to step 5 of the
[Assignment Workflow](../../../materials/guides/assignment-workflow/#opening-in-intellij)
if you need a refresher on how to do this.

If that doesn't work, be sure that `src` is blue and `tests` is green. Refer to
the [IntelliJ WTFS](../../../materials/guides/intellij/wtfs/#i-cant-run-my-java-filefiles-dont-show-up-as-java-files)
to mark your `src` and `tests` folders appropriately.


