This is the tools and patch for an (AI-generated) translation of *Die Fugger II*
into English.

Specifically, this patch applies to the version which the README calls a
“überarbeitete” version, which has the following sha1sum:

```
22c603f21b010dbd8782a7e2cdfd56aea0c0da21  FUGGER2.EXE
```

It may work with other versions, and at least should be relatively easy to adapt
to other versions with some expertise, but has only been tested with this one.

A translation of the handbook is also available, in
[handbook-en.txt](handbuch/handbook-en.txt). It was translated in a similar way.
Thanks to archive.org user Eulisker for uploading the [original German
handbook](https://archive.org/details/fugger-ii-die-1996-das-handbuch-de), in
higher quality than the copy that came with my version of the game.

A translation of the mission cards that came in my box—I have no idea whether
they're the same in every box—is available in
[cards-en.txt](mission-cards/cards-en.txt). It was translated the same as the
manual.


## Applying the patch

The patch is provided as a .ips file, which can be applied with any IPS patcher
(such as flips). Or, you can use `tools/apply.js`.


## How the patch was made

`tools/extract.js` extracts strings, and converts them to Unicode, in
`strings.json`.

Irrelevant strings, error codes, random string-like sequences, and other cruft
was removed from `strings.json` by hand.

Those strings were then run through ChatGPT for translation, using
`tools/trans.js`. It leaves the translation as `en` fields in `strings.json`.

Because this is raw bit-banging string patching, the string must fit into the
same space. `tools/check.js` checks for this issue, as well as the related issue
of the translation removing or reordering special tokens (e.g. %s).

Any mistakes made in automatic translation are corrected into `en2` fields by
hand.

Finally, the patch is applied with `tools/apply.js`.

I created the .ips file with flips, as a further convenience.
