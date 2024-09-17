# How to install

To use toncli, you will need to install a special version of the Ton Virtual Machine  for the test engine. This version includes a special debug op, developed by SpyCheese, which is necessary for working with the test engine.

Currently, there are two live repositories where you can find the updated Fift & Func:

* [SpyCheese repo](https://github.com/SpyCheese/ton/tree/toncli-local) - toncli-local branch
* [Disintar repo](https://github.com/disintar/ton/tree/toncli-local) - toncli-local branch
  * Contains `~strdump` and other necessary features

To use toncli, you will need to install the special version of the Ton Virtual Machine and use the updated Fift & Func from one of these repositories. This will allow you to take advantage of the custom test engine and the necessary debug op.



To install from those repos we provide simple guides:



<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>Docker image</td><td></td><td><a href="docker-image.md">docker-image.md</a></td></tr><tr><td></td><td>Pre-builds</td><td></td><td><a href="pre-builds.md">pre-builds.md</a></td></tr><tr><td></td><td>Compile source code</td><td></td><td><a href="compile-source-code.md">compile-source-code.md</a></td></tr></tbody></table>



### Special TVM OPs

| <p>xxxxxxxxxxxxxxxx<br>Name</p> | <p>xxxxxxxx<br>Opcode</p> | <p>xxxxxxxxxxxx<br>Stack</p> | <p>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx<br>Description</p>                                                                                                                                                                                                                                                                                                       |
| ------------------------------- | ------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `GASLIMITSTEMP`                 | **`FEEF10`**              | _`- g_l g_r`_                | Returns the current gas limit `g_l` and remainig gas `g_r`.                                                                                                                                                                                                                                                                                                                                |
| `PRIVTOPUB`                     | **`FEEF11`**              | _`priv - pub`_               | <p>Converts Ed25519 private key into a public key.<br>Both keys are represented as 256-bit unsigned integers.</p>                                                                                                                                                                                                                                                                          |
| `SIGN`                          | **`FEEF12`**              | _`x p - s`_                  | <p>Signs a 256-bit unsigned integer <code>x</code> using a private key <code>p</code>.<br>Key is represented as a 256-bit unsigned integer.<br>Signature is returned as a slice. It can be checked using <a href="https://ton.org/docs/#/smart-contracts/tvm-instructions/instructions?id=instr-chksignu"><code>CHKSIGNU</code></a>.</p>                                                   |
| `SIGNS`                         | **`FEEF14`**              | _`x p - s`_                  | <p>Signs data portion of slice <code>x</code> using a private key <code>p</code>. Bit length of <code>x</code> should be divisible by 8.<br>Key is represented as a 256-bit unsigned integer.<br>Signature is returned as a slice. It can be checked using <a href="https://ton.org/docs/#/smart-contracts/tvm-instructions/instructions?id=instr-chksigns"><code>CHKSIGNS</code></a>.</p> |
| `RESETLOADEDCELLS`              | **`FEEF13`**              | _`-`_                        | Future cell loads will consume gas as if no cells were loaded before `RESETLOADEDCELLS`.                                                                                                                                                                                                                                                                                                   |



