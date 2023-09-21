he handling of the :: marker is smart:

If it occurs as a paragraph of its own, that paragraph is completely left out of the document.

If it is preceded by whitespace, the marker is removed.

If it is preceded by non-whitespace, the marker is replaced by a single colon.

That way, the second sentence in the above example’s first paragraph would be rendered as “The next paragraph is a code sample:”.

Code highlighting can be enabled for these literal blocks on a document-wide basis using the highlight directive and on a project-wide basis using the highlight_language configuration option. The code-block directive can be used to set highlighting on a block-by-block basis. These directives are discussed later.

