# Sanity checks — Universal


## Audit before accepting any AI output

Before I accept these changes: (1) identify every cell that was modified, (2) confirm each modified cell was a blue input cell and not a black formula cell, (3) confirm no values were hard-coded into calculation cells, and (4) show me one downstream output that changed as a result, to confirm the model is responding correctly.

## Check internal consistency

Look at the key output metrics in this model [e.g. revenue, gross margin, cash balance]. Do the numbers tell a consistent and coherent story? Flag anything that seems mathematically inconsistent or economically implausible given the inputs.

## Check for hard-coded values

Scan the model for any cells where a value appears to be hard-coded (a raw number in a cell that should contain a formula). List any you find and confirm whether they should be formulas referencing inputs instead.
