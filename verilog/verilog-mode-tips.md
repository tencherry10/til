## Verilog Mode Tips & Tricks


1. Auto tie input to zero / output to float
1. Removing outputs from AUTOOUTPUT

#### Auto tie input to zero / output to float

Sometimes it is useful to tie inputs only if it is zero and leave floating if it is an output.

Here is how you would do it using verilog auto-mode

```
  .m\(.*\)_axis_\(.*\)  (@"(if (equal vl-dir \\"input\\") (concat \\"{\\"vl-width\\"{1'b0}}\\") \\"\\")"), 
```

[source](http://www.veripool.org/boards/15/topics/1565-Verilog-mode-how-to-assign-all-0-to-input-and-floating-all-output)

