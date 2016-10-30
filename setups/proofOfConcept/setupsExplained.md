## useroption.setup

Sometimes it may be desirable to allow the user choices with respect to the setup, like enabling the installation of further tooling, importing certain projects etc.

The technical solution are filters that activate tasks. These filter can test system and environment properties (https://www.eclipse.org/forums/index.php?t=msg&th=1080068&goto=1742042&#msg_1742042). So what we do is define a boolean variable whose value the user can chose before the installation, write its value to the eclipse.ini and evaluate it in the task filter.

It is important that the filtered task must not run in the bootstrap phase as the correct value from the eclipse.ini is not available during that phase.

In our example setup we chose scope://Installation as Storage URI for the variable declaration. This should cause the variable not to be stored in the user setup, so the user should be asked for the option everytime a new instance of the project is to be installed. If the user should be asked only once (as the answer is expected to be the same every time), just use the default scope://.

Make sure that `value` in the `VariableTask` is not present (this is not the same as value being an empty string)! Otherwise, the value is assumed to be known and the user will not be asked on the Variables page. Checking this is best done by opening the model as text (this can also be done from the Setup editor's context menu -> Open in Text Editor).