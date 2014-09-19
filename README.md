oomph-playground
================

## Why at all

The [Oomph installer](http://wiki.eclipse.org/Eclipse_Oomph_Installer) comes with its predifined set of available products and projects.
It is fairly easy to add your own project setups locally, but what if you want to ship setups for a team of developers.
Maybe they are not supposed to choose any version of Eclipse and they should not see all hosted projects, but only those you want...

This sample project is intended to give a first idea how this could be done.
The key point is that you can tell the Oomph installer where to look for its models.
If you take a look at the run configurations shipped with the Oomph project source code, you will notice the
start parameter "-Doomph.redirection.setups".

## How to try it out

Start the installer with the additional command line parameter:

-vmargs "-Doomph.redirection.setups=http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/->https://raw.githubusercontent.com/nittka/oomph-playground/master/setups/"

or add the following line to the installer's oomph.ini

-Doomph.redirection.setups=http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/->https://raw.githubusercontent.com/nittka/oomph-playground/master/setups/

## What was changed wrt to the original

As a proof of concept, I started with the initial setups, renaming the project and product setup files.
I stripped the products to contain only the Eclipse Standard/SDK and replaced projects in the project catalog by my own set.
The org.eclipse.setup file could not be renamed, as the installer actually tries to locate a file of that name as a starting point.
Other name tags were left intact as well, so that the variable logic with respect to the User setup would not break.