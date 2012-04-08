---
author: admin
date: '2009-01-31 12:51:10'
layout: post
slug: bpforb-is-now-pep-8-compliant
status: publish
title: BPforB is now PEP 8 compliant!
wordpress_id: '222'
? ''
: - Phase 2
---

As mentioned in the previous post, Robin Stocker kindly provided a git
patch with the required changes to all scripts stored on the repository
to be compliant with the PEP 8. The changes were mainly regarding
variable/object names, but they were important as make the code
available here more Pythonic following the rules of the Benevolent
Dictator for Life. I would like to thank Robin for spending his time
doing this. Much appreciated. Now, just a quick git tutorial on how to
apply patches: git apply \_\_patch\_file\_\_ git commit -a -m "patch
applied" git push That's it. Apply, commit, push and you're done. The
repository is already updated.
