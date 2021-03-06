<img style="display: block; margin: auto;" src="docs/mbb.png" alt"Logo libmbb"/>

libmbb - Embedded Building Bricks
=================================

Synopsis
--------

*libmbb* is a [MIT-licensed](LICENSE.txt) C library targeted at embedded
systems.

The upstream repository is at <https://github.com/jawebada/libmbb/>.

Features
--------

* [Hierarchical state machines (HSMs)](docs/HSM.md), including timers
* [Fixed-cacpacity queues](docs/Queue.md)
* [Debugging macros](docs/Debug.md)
* [Unit tests](docs/Test.md)

*libmbb* does not allocate memory dynamically. It is up to the developer to
decide how memory is allocated. The HSM module supports both purely
event-driven and non-blocking, real-time suitable processing.

Tools
-----

The tools sub directory contains the following command line tools:

* `mhsm_scaffold` adds event processing function stubs to source files
* `munt_main` generates main functions for unit tests

Building
--------

*libmbb* uses the autotools for building. If you clone its upstream repository
you will have to call `./autogen.sh` to build the `configure` script.
`autogen.sh` just calls `autoreconf` which depends on `autoconf` and `automake`
being installed. If the `configure` script is built it is the usual game of

	./configure
	make
	make install

The `install` target will install the examples and unit tests along with libmbb
itself. These programs have rather unspecific names like `test_hsm`. Calling
`./configure --program-prefix=mbb_` will install them as `mbb_test_hsm`
instead. Alternatively, you might specify `./configure --prefix=/opt/mbb` to
install everything into `/opt/mbb`.

Call `make check` to run the unit tests.

Call `./configure --host=arm-linux` to cross-compile for arm-linux.

Call `./configure --help` for a general help message.

Dependencies
------------

* The [libev](http://software.schmorp.de/pkg/libev.html) timers backend and the
  examples using it are only compiled if `libev` and its header files are
  installed on your system.
* The tools are written in and thus depend on
  [Ruby](https://www.ruby-lang.org/).

Examples
--------

* [debugging](examples/debugging.c): debugging macros
* [monostable](examples/monostable.c): multiple HSM instances, libev timers
* [pelican](examples/pelican.c): [Miro Samek's](http://www.state-machine.com/)
  [PEdestrian LIght CONtrolled (PELICAN) Crossing
  Example](http://www.state-machine.com/resources/AN_PELICAN.pdf), periodic
  timers

Note that the terminal interfaces of some of the examples (`pelican` and
`monostable`) will be interfered with by the `stderr` output of the debugging
macros. You can either add `-DNDEBUG` to `CPPFLAGS` to disable these debugging
macros or redirect `stderr` like this:

	examples/pelican 2> log 
