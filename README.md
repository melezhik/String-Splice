NAME
====

String::Splice - Splice; but for Strings instead of Arrays

SYNOPSIS
========

```perl6
use String::Splice;

say 'Perl 6 is awesome'.splice(0, 6, 'Raku');
# Raku is awesome

say 'This is Rakudo'.splice(*-2, 2);
# This is Raku

say "Tonight I'm gonna party like it's 1999"
  .splice(18, 5, 'program').splice(*-4, 2, 20);
# Tonight I'm gonna program like it's 2099
```

DESCRIPTION
===========

String::Splice is intended to give a simple interface to slicing and dicing Strings much in the same way that CORE Array.splice makes it easy to slice and dice Arrays.

Works very similarly on strings as the CORE splice works on Arrays.

Available as both a method (augmenting strings) or as a subroutine (that primarily operates on strings).

```perl6
multi sub    splice($String:D, $start, $chars?, Str $replacement = '' --> Str)
multi method splice($String:D: $start, $chars?, Str $replacement = '' --> Str)
```

Need to supply a defined string to operate on, a starting point (in chars), optionally the number of chars to affect, and an optional replacement string (defaults to ''). The starting point may be a positive integer, any Real numeric value that can be coerced to a positive integer, or a WhateverCode that will offset from the string end.

Use a WhateverCode if you want to modify a string some set offset from the end of an unknown length string rather than from the start.

`'Be home by 6:00PM'.splice(*-2, 1, 'A')` # Be home by 6:00AM

You may supply a start point larger than the string and the string will be padded with spaces to achieve that starting point.

`splice('Raku', 9, 'rocks')` is valid, as is `splice('Raku', *+5, 'rocks')` # Raku rocks

The major difference in how String.splice differs from Array.splice is in that the starting position does not default to zero. It must be given.

When using 4 argument splice: (String, start, chars, replace) the replace parameter does not need to ba a string. Anything that may be coerced to a string may be used. With 3 argument splice: (String, start, replace), replace MUST be a string to disambiguify the signature to the dispatcher.

AUTHOR
======

Steve Schulze (thundergnat)

COPYRIGHT AND LICENSE
=====================

Copyright 2020 Steve Schulze

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.
