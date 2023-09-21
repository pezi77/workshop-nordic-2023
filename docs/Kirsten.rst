Inline markup
The standard reST inline markup is quite simple: use

one asterisk: *text* for emphasis (italics),

two asterisks: **text** for strong emphasis (boldface), and

backquotes: ``text`` for code samples.

If asterisks or backquotes appear in running text and could be confused with inline markup delimiters, they have to be escaped with a backslash.

Be aware of some restrictions of this markup:

it may not be nested,

content may not start or end with whitespace: * text* is wrong,

it must be separated from surrounding text by non-word characters. Use a backslash escaped space to work around that: thisis\ *one*\ word.

These restrictions may be lifted in future versions of the docutils.

It is also possible to replace or expand upon some of this inline markup with roles. Refer to Roles for more information.
