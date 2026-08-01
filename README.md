<!-- GEEIQ-DOCS-BLOCK:START — added by the docs standardisation pass. Everything below the END marker is upstream's README, unmodified. -->
> **GeeIQ fork notice.** This repository is a fork of the public npm package
> [`timjcook/ember-cli-autocomplete-input`](https://github.com/timjcook/ember-cli-autocomplete-input).
> The README below is **upstream's**, kept as its author wrote it, and it documents the
> upstream addon's API.
>
> GeeIQ-side documentation is in **[`docs/geeiq.md`](./docs/geeiq.md)**: what this fork
> changes (the jQuery keyboard-nav dependency replaced with a local mixin, focus callbacks,
> a randomised input `name` to defeat Chrome autofill, and an Ember 3.13 upgrade), which ref
> holds the code, the publish story, the contract the component imposes on a caller, and
> what in this org consumes it.
>
> Four corrections to the text below, recorded here rather than edited into upstream's body:
>
> - **The install instruction does not deliver this fork.**
>   `ember install ember-cli-autocomplete-input` installs *upstream's* published package from
>   `registry.npmjs.org`. This fork is not published to any registry, under this name or any
>   other, so the only way to consume this code is a git dependency on this repository or a
>   vendored copy. See `docs/geeiq.md` → *Release*.
> - **The build badge describes upstream, not this repository.** It points at a Travis CI
>   build of `timjcook/ember-cli-autocomplete-input`. This repository has no GitHub Actions
>   workflow at any ref and no CI of its own, and the organisation does not use Travis CI.
> - **The `name` argument no longer behaves exactly as described.** It is set as the input's
>   `id`, but the `name` attribute now receives a generated value: when `name` is omitted the
>   input gets a random `autocomplete_<hex>` token as its `name` and an empty `id`. This was
>   deliberate, to stop Chrome inserting its own autofill options. When `name` *is* supplied,
>   the description below holds.
> - **The argument list below is no longer complete.** `placeholder`, `autocomplete`,
>   `on-focus-in` and `on-focus-out` are also accepted, and the block form yields each result
>   into the dropdown body. All are documented in `docs/geeiq.md` → *Export inventory* and
>   *The contract it imposes on a caller*.
<!-- GEEIQ-DOCS-BLOCK:END -->

# ember-cli-autocomplete-input

[![Build Status](https://travis-ci.org/timjcook/ember-cli-autocomplete-input.svg?branch=master)](https://travis-ci.org/timjcook/ember-cli-autocomplete-input)

An autocomplete text input for Ember.
* It provides a hook for updating a list of results based on a change to the current term in the input field.
* It also provides some basic keyboard navigation for quickly accessing items in the results list, including:
  * Enter key - select the currently highlighted result
  * Esc key - clear the search term and the current results
  * Up key - move the highlight to the result above the currently highlighted results
  * Down key - move the highlight to the result below the currently highlighted results

## Installation

* `ember install ember-cli-autocomplete-input`

## Using the component

You can include the component in any of your templates:

```
{{autocomplete-input name=name results=results updateTerm="updateTerm" selectResult="selectResult"}}
```

## Arguments

The `autocomplete-input` component takes the following arguments

### name - String

The name variable will be set on the input tag as both the name attribute as well as the id attribute, allowing focus to be triggered by clicking a label tag.

### results (required) - Array

The results array contains the current list of results objects.

### resultName (optional, default 'name') - String

The attribute on an object in the `results` array that will be used as the display in the results list.

### resultValue (optional, default 'value') - String

The attribute on an object in the `results` array that will be used to check a result to the currently highlighted result in the results list.

## Handling interactions

The `autocomplete-input` component exposes the following actions which respond to user interaction:

### selectResult(result)

This is fired when a result item is clicked or the `enter` key is pressed while a result is highlighted.
The selected result is passed as the only argument.

### updateTerm(term)

This is fired when the term is updated by typing into the bound input field.
Use this action to update your `results` array.

### clearSearch()

This is fired when the `esc` key is pressed.
Use this action handle a clear of the search, ie clear results array and search term.
