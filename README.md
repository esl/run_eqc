

<h1>The run_eqc application</h1>

run_eqc - An escript wrapper for Quviq QuickCheck

==================================================
.

Copyright (c) 2010 Erlang Solutions Ltd.

__Version:__ 0.1



Run_eqc packages QuickCheck Mini as a single escript file and provides 
a command-line interface for running QuickCheck tests. with some 
additional support for output filtering.



*Note:* The description and examples apply almost precisely also to the 
`run_proper.ez` file, which wraps PropEr in the same way.
PropEr is an EQC-compatible Open Source component designed by 
Kostis Sagonas and Manolis Papadakis. You can fetch it at 
[http://github.com/manopapad/proper.git](http://github.com/manopapad/proper.git)



The file `run_eqc.ez` should be a runnable version of the wrapper,
including `eqc-1.0.1` - the current version of EQC Mini. To build a new 
version, ensure that you have EQC Mini installed, update the location of
it in the Makefile, and call `make script`.


<pre>
Usage: escript run_eqc.ez [ Option ]
-n NumTests    run NumTests number of tests (default 100)
-m Module      run eqc:module([ Option, ] Module)
-pa Dir        prepend Dir to the code path
-pz Dir        append Dir to the code path
-rpt all       set reporting level - 'all': report everything
| none     'none': (as silent as possible)
| error    'error': report on failing tests.
</pre>




The `-rpt error` option buffers all output produced by QuickCheck and 
discards it for all successful properties. If a property fails, all output
for that run is printed.



Example:



Using the (broken) property in [run_eqc_test.erl](http://github.com/esl/run_eqc/blob/master/../test/run_eqc_test.erl), we can illustrate the use of num_tests (the error is unlikely to appear with only 100 tests), and `-rpt error`. We also note that `run_eqc.escript` signals test case failure appropriately to the make script.


<pre>
$ make test
./rebar compile
==> edown (compile)
==> run_eqc (compile)
escript ebin/run_eqc_gen.beam run_eqc.ez /Users/uwiger/lib/eqc-1.0.1/ebin eqc
escript ebin/run_eqc_gen.beam run_proper.ez /Users/uwiger/git/proper/ebin proper
erlc -W -o test test/run_eqc_test.erl
escript ./run_eqc.ez -m run_eqc_test -n 1000 -rpt error -pa test
Starting eqc mini version 1.0.1 (compiled at {{2010,6,13},{11,15,30}})
FAILED property prop_lists_delete:
...........................................................................................................................................................................................................................................................................................Failed! After 284 tests.
{-41,[5,-30,35,-2,23,-37,26,-7,-41,-2,-41,-13,41,-19,-17]}
Shrinking....(4 times)
{-41,[-41,-41]}
Failed properties in run_eqc_test:
[prop_lists_delete]
make: *** [test_eqc] Error 1
</pre>




If we test the same module using default values:


<pre>
$ escript ./run_eqc.ez -m run_eqc_test -pa test
Starting eqc mini version 1.0.1 (compiled at {{2010,6,13},{11,15,30}})
....................................................................................................
OK, passed 100 tests
....................................................................................................
OK, passed 100 tests
....................................................................................................
OK, passed 100 tests
...tests passed (run_eqc_test)
</pre>




<h2>Running EQC Mini interactively</h2>





You can load and run the EQC Mini code directly from the escript file,
using OTP's ability to load code from a zip archive.



Example:


<pre>
$ erl -pa run_eqc.ez/eqc/ebin
Erlang R14B02 (erts-5.8.3) [source] [smp:4:4] [rq:4] [async-threads:0] [hipe] [kernel-poll:false]

Eshell V5.8.3  (abort with ^G)
1> eqc:start().
Starting eqc mini version 1.0.1 (compiled at {{2010,6,13},{11,15,30}})
<0.35.0>
</pre>



<h2 class="indextitle">Modules</h2>



<table width="100%" border="0" summary="list of modules">
<tr><td><a href="http://github.com/esl/run_eqc/blob/master/doc/run_eqc.md" class="module">run_eqc</a></td></tr>
<tr><td><a href="http://github.com/esl/run_eqc/blob/master/doc/run_eqc_app.md" class="module">run_eqc_app</a></td></tr>
<tr><td><a href="http://github.com/esl/run_eqc/blob/master/doc/run_eqc_gen.md" class="module">run_eqc_gen</a></td></tr>
<tr><td><a href="http://github.com/esl/run_eqc/blob/master/doc/run_eqc_sup.md" class="module">run_eqc_sup</a></td></tr>
<tr><td><a href="http://github.com/esl/run_eqc/blob/master/doc/run_proper.md" class="module">run_proper</a></td></tr></table>

