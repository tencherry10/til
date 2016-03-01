## Verilog Mode Tips & Tricks


1. Auto tie input to zero / output to float(#auto-tie-input-to-zero--output-to-float)
1. Removing outputs from AUTOOUTPUT(##removing-outputs-from-autooutput)

#### Auto tie input to zero / output to float

Sometimes it is useful to tie inputs only if it is zero and leave floating if it is an output.

Here is how you would do it using verilog auto-mode

```
  .m\(.*\)_axis_\(.*\)  (@"(if (equal vl-dir \\"input\\") (concat \\"{\\"vl-width\\"{1'b0}}\\") \\"\\")"), 
```

[source](http://www.veripool.org/boards/15/topics/1565-Verilog-mode-how-to-assign-all-0-to-input-and-floating-all-output)

#### Removing outputs from AUTOOUTPUT

1. Just fake it out

  ```verilog
  `ifdef NEVER
    output a_out;   // Fake out Verilog-mode
    output b_out;   // Fake out Verilog-mode
  `endif
  ```
1. Use verilog-auto-output-ignore-regexp

  ```verilog
  /*Local Variables:
    verilog-auto-output-ignore-regexp: "" 
    eval:(setq verilog-auto-output-ignore-regexp (concat
      "^\\(" 
      "signal1_.*" 
      "\\|signal2_.*" 
      "\\)$" 
    )))
    End:
  */
  ```



