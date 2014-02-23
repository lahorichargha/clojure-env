clojure-the-door-on-your-way-out
================================

Playing with Clojure


lein Basic Usage
----------------
The
[tutorial](https://github.com/technomancy/leiningen/blob/stable/doc/TUTORIAL.md)
has a detailed walk-through of the steps involved in creating a new
project, but here are the commonly-used tasks:

    $ lein new [TEMPLATE] NAME # generate a new project skeleton

    $ lein test [TESTS] # run the tests in the TESTS namespaces, or all tests

    $ lein repl # launch an interactive REPL session

    $ lein run -m my.namespace # run the -main function of a namespace

    $ lein uberjar # package the project and dependencies as standalone jar

Use `lein help` to see a complete list. `lein help $TASK` shows the
usage for a specific task.

You can also chain tasks together in a single command by using the
`do` task with comma-separated tasks:

    $ lein do clean, test foo.test-core, jar

Most tasks need to be run from somewhere inside a project directory to
work, but some (`new`, `help`, `search`, `version`, and `repl`) may
run from anywhere.
