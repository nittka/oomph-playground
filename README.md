oomph-playground
================

See the master branch for a general introduction.

## Redirection of project catalog only

Redirecting the project catalog only is more tricky. The main problem is making sure that the eclipse installation created is using the same project catalog. Otherwise, a project may me visible in the installer but not in the installation created.

This branch shows an example.

## How to try it out

Add the following lines to the installer's eclipse-inst.ini

`-Doomph.redirection.projectCatalog=index:/org.eclipse.projects.setup->https://raw.githubusercontent.com/nittka/oomph-playground/projectCatalogRedirection/setups/my.projects.setup`
`-Doomph.redirection.setupDir=index:/setups/->https://raw.githubusercontent.com/nittka/oomph-playground/projectCatalogRedirection/setups/setups/`


## What was changed wrt to the original

The first line redirects the Eclipse project catalog to another catalog (note that the GitHub catalog is still in place because the original index itself is still used). The second redirection makes sure that files located relative to my.projects.setup are still found. These two redirections are also part of the project catalog itself.

In order to keep things simple, I recommend using only absolute URIs in the catalog. In that case you only need to redirect the catalog itself. It also prevents problems caused by two catalogs using the same subdirectory names for relative URIs.

There is a pending enhancement request for introducing a placeholder catalog to the index shipped with Oomph. Having that you can keep both Eclipse and GitHub catalog and simply add your own project catalog rather than replacing one of the defaults.