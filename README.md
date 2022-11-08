# Comparison of generalized diff libraries for Python

It is often said there are more generalized diff libraries for Python than
stars in the Milky Way. Here I compare them all.

*Did I miss one or do you have suggestions for other criteria? Feel free to
[open an issue](https://github.com/smheidrich/comparison-of-generalized-diff-libraries-for-python/issues/new)!*

## What do I mean by "generalized diff"?

While regular UNIX `diff` is well-suited to comparing files / strings of
characters, there are libraries for most programming languages that allow
comparing structured data like JSON or that language's JSON equivalent (in
Python: dicts, lists and primitives, called "JSON-ish" from here on), producing
patches written in terms of that structure rather than in terms of lines and
characters. That's what I mean by "generalized diff". I guess other terms would
be "data diff", "structure diff", "structured data diff", "JSON diff", or
something along those lines.

## Comparison

<table>
  <tr>
    <th>Name / URL</th>
    <th>Supported data structures</th>
    <th>Diff/patch output formats</th>
    <th>Can apply patches</th>
    <th>Diffing time complexity</th>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/jsonpatch/">
        jsonpatch
      </a>
    </td>
    <td>
      <ul>
        <li>JSON-ish</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>JSON Patch (RFC 6902)</li>
      </ul>
    </td>
    <td>
      ✔
    </td>
    <td>
      ?
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/deepdiff/">
        DeepDiff
      </a>
    </td>
    <td>
      <ul>
        <li>JSON-ish</li>
        <li>arbitrary Python objects that define <code>__slots__</code> or <code>__dict__</code></li>
      </ul>
    </td>
    <td>
      <ul>
        <li><code>DeepDiff</code> objects</li>
        <li>dict representation of <code>DeepDiff</code></li>
        <li>JSON representation of <code>DeepDiff</code></li>
      </ul>
    </td>
    <td>
      ❌
    </td>
    <td>
      O(n) when not ignoring order, otherwise ?
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/jycm/">
        jycm
      </a>
    </td>
    <td>
      <ul>
        <li>JSON-ish</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>own JSON-ish format</li>
      </ul>
    </td>
    <td>
      ❌
    </td>
    <td>
      ?
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/jsondiff/">
        jsondiff
      </a>
    </td>
    <td>
      <ul>
        <li>JSON-ish</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>own JSON-ish format</li>
      </ul>
    </td>
    <td>
      ✔ (undocumented)
    </td>
    <td>
      ?
    </td>
  </tr>
</table>

## Excluded

These projects have names that might suggest they'd fit the bill, but were
excluded from the comparison for the stated reasons:

- [json-diff](https://pypi.org/project/json-diff/):
  Is just a CLI tool with no (documented) API.
- [json-diff-patch](https://github.com/apack1001/json-diff-patch):
  Is just a CLI tool with no (documented) API (yet). Also not released to PyPI
  yet.


## Summary

To my surprise, I couldn't find a single package that a) provides
a Python API and b) can both produce and apply JSON patches in the [RFC 6902
JSON Patch](https://jsonpatch.com/) format.

JavaScript looks a lot better positioned on that front, with libraries like
[jiff](https://github.com/cujojs/jiff) being able to not only diff and patch
but also manipulate the patches in various ways, like "rebasing" or changing
the order of operations.