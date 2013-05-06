nose.el
=======

This gives a bunch of functions that handle running nosetests on a
particular buffer or part of a buffer.

This is a fork from the the [bitbucket repository][fork].

What's different ?
------------------

This fork drop the support for non-global nose test runner which is
buggy under Windows. Globally available test runner is OK for my needs.

I also plan to make it work with test suites (available via
`easy_install nose-fixes`).

Install
-------

You'll need to add the directory containing `nose.el` to your `load-path`,
and then

    (require 'nose)

Usage
-------

If your global nose isn't called `nosetests`, then you'll want to
redefine `nose-global-name` to be the command that should be used.

By default, the root of a project is found by looking for any of the files
`setup.py`, `.hg` and `.git`. You can add files to check for to the file
list:

    (add-to-list 'nose-project-root-files "something")

or you can change the project root test to detect in some other way
whether a directory is the project root:

    (setq nose-project-root-test (lambda (dirname) (equal dirname "foo")))

If you want dots as output, rather than the verbose output:

    (defvar nose-use-verbose nil) ; default is t

Probably also want some keybindings:

    (add-hook 'python-mode-hook
              (lambda ()
                (local-set-key "\C-ca" 'nosetests-all)
                (local-set-key "\C-cm" 'nosetests-module)
                (local-set-key "\C-c." 'nosetests-one)
                (local-set-key "\C-cpa" 'nosetests-pdb-all)
                (local-set-key "\C-cpm" 'nosetests-pdb-module)
                (local-set-key "\C-cp." 'nosetests-pdb-one)))

Thanks
------

To the original author of nose.el:  `Jason Pellerin` and `Augie Fackler`


[fork]: https://bitbucket.org/durin42/nosemacs/overview
