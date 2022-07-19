#################
Fancy Compilation
#################

This is a minimalist package that enhances ``compilation-mode`` in the following ways.

- Support color output.
- Support progress updates on a single line
  (as used by `ninja <https://ninja-build.org>`__, `sphinx <https://www.sphinx-doc.org>`__ and many other build systems).
- Use scrolling behavior similar to most terminals.
- Optionally use foreground & background independent of theme colors.

.. This is a PNG image.

.. figure:: https://codeberg.org/attachments/1a339b6c-fb62-499b-8acf-5f00092f28d2
   :scale: 50 %
   :align: center


Motivation
==========

There are some limitations with compilation output that I found make it less usable than building from a terminal.

- No color output from the compilers diagnostics.
- No support for printing text progress on a single line which works well to avoid the output
  being flooded by files that were compiled, making it easier to miss important warnings.

While this may seem small - improved diagnostics to help identifying an error and reducing the risk of missing a warning
make them both valuable features.
This package was written to conveniently support these as well as other minor quality of life features in Emacs.


Usage
=====

This can be lazily loaded after ``compile``.

.. code-block:: elisp

   (with-eval-after-load 'compile
     (fancy-compilation-mode))

Once this global mode is enabled, calling ``compile`` will use enhancements from this package.


Customization
-------------

``fancy-compilation-term``: ``"tmux-256color"``
   The ``TERM`` environment variable to use (set to an empty string to leave unset).

``fancy-compilation-override-colors``: t
   Override theme faces (foreground/background).

``fancy-compilation-default-face``
   The face to use for default text when ``fancy-compilation-override-colors`` is enabled.

``fancy-compilation-quiet-prelude``: t
   Suppress text such as "Compilation Started" which is otherwise included before compilation output.

``fancy-compilation-quiet-prolog``: t
   Use brief text output when compilation has completed.


Hints
=====

Since tools that output to the compilation buffer wont recognize it as a ``TTY``,
you may need to force color output.

GCC
   Pass ``-fdiagnostics-color=always``, typically via (``CFLAGS`` & ``CXXFLAGS``).
Clang
   Pass ``-fcolor-diagnostics``, typically via (``CFLAGS`` & ``CXXFLAGS``)
