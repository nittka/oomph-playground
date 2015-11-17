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

## Recommendations for shipping your own project catalog

* Keep things simple and use only absolute URIs in your catalog. In this case you only need to redirect the catalog itself. It also prevents problems caused by two catalogs using the same subdirectory names for relative URIs.
* Make use of the redirectable catalogs recently introduced to the Oomph index. `redirectable.projects.setup` for your own project catalog (and `redirectable.products.setup` for your own product catalog) are empty place holder setups that you can redirect in the way described above without disabling any of the other hosted catalogs.
* Do not forget to add the EclipseIniTask (catalog redirection) to your catalog.