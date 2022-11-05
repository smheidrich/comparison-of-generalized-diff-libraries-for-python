# Comparison of generalized diff libraries for Python

It is often said there are more generalized diff libraries for Python than
stars in the Milky Way. Here I compare them all.

*Did I miss one or do you have suggestions for criteria? Feel free to
[open an issue](https://github.com/smheidrich/comparison-of-pytest-data-file-access-libraries/issues/new)!*

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
  {%- for library in libraries %}
  <tr>
    <td>
      <a href="{{ library.pypi_url }}">
        {{ library.name }}
      </a>
    </td>
    <td>
      <ul>
      {%- for data_structure in library.supported_data_structures %}
        <li>{{ data_structure }}</li>
      {%- endfor %}
      </ul>
    </td>
    <td>
      <ul>
      {%- for patch_format in library.patch_formats %}
        <li>{{ patch_format }}</li>
      {%- endfor %}
      </ul>
    </td>
    <td>
      {% if library.can_apply_patches is true %}✔{% elif library.can_apply_patches is false %}❌{% else %}{{ library.can_apply_patches }}{% endif %}
    </td>
    <td>
      {{ library.diffing_time_complexity }}
    </td>
  </tr>
  {%- endfor %}
</table>

## Excluded

These projects have names that might suggest they'd fit the bill, but were
excluded from the comparison for the stated reasons:

{% for library in excluded_libraries -%}
- [{{ library.name }}]({{ library.pypi_url }}):
  {{ library.reason|wordwrap(77)|indent(2) }}
{% endfor %}

## Summary

To my surprise, I couldn't find a single package that a) provides
a Python API and b) can both produce and apply JSON patches in the [RFC 6902
JSON Patch](https://jsonpatch.com/) format.

JavaScript looks a lot better positioned on that front, with libraries like
[jiff](https://github.com/cujojs/jiff) being able to not only diff and patch
but also manipulate the patches in various ways, like "rebasing" or changing
the order of operations.
