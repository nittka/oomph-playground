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

`-vmargs "-Doomph.redirection.setups=http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/->https://raw.githubusercontent.com/nittka/oomph-playground/master/setups/"`

or add the following line to the installer's oomph.ini

`-Doomph.redirection.setups=http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/->https://raw.githubusercontent.com/nittka/oomph-playground/master/setups/`

That way both product and project catalog are replaced.

The common prefix `http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/` may be abbreviated by `index:/`

## What was changed wrt to the original

As a proof of concept, I started with the initial setups, renaming the project and product setup files.
I stripped the products to contain only the Eclipse Standard/SDK and replaced projects in the project catalog by my own set.
The org.eclipse.setup file could not be renamed, as the installer actually tries to locate a file of that name as a starting point.
Other name tags were left intact as well, so that the variable logic with respect to the User setup would not break.

## Redirecting the project catalog only
Replacing the project catalog only seems not to be less simple. Running the installer with the following parameter looks good at first
`-Doomph.redirection.projectCatalog=http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/org.eclipse.projects.setup->https://raw.githubusercontent.com/nittka/oomph-playground/master/setups/my.projects.setup`
but unfortunately, it does not work. You will notice that project setups pointed to relative to the project catalog are not resolved correctly.
The others will not be installed as the eclipse installation created by the installer is missing the redirecting start parameter, so the project setup to be installed will not be found, once the base installation is materialized.

See the projectCatalogRedirection branch for an attempt to overcome these problems.