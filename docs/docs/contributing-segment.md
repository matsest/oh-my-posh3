---
id: contributing-segment
title: Add Segment
sidebar_label: Add Segment
---

## Create the logic

Add a new file following this convention: `new_segment.go`.
Ensure `new` is a single verb indicating the context the segment renders.

You can use the following template as a guide.

```go
package main

type new struct {
    props          *properties
    env            environmentInfo
}

const (
    //NewProp switches something
    NewProp Property = "newprop"
)

func (n *new) enabled() bool {
    true
}

func (n *new) string() string {
    newText := n.props.getString(NewProp, "n00b")
    return newText
}

func (n *new) init(props *properties, env environmentInfo) {
    n.props = props
    n.env = env
}
```

For each segment, there's a single test file ensuring the functionality going forward. The convention
is `new_segment_test.go`, have a look at existing segment tests for inspiration.

## Create a name for your Segment

[`segment.go`][segment-go] contains the list of available `SegmentType`'s, which gives them a name we can map from the
`.json` [themes][themes].

Add your segment.

```go
//New is brand new
New SegmentType = "new"
```

## Add the SegmentType mapping

Map your `SegmentType` to your Segment in the `mapSegmentWithWriter` function.

```go
New: &new{},
```

## Test your functionality

Even with unit tests, it's a good idea to build and validate the changes.

```shell
go build -o $GOPATH/bin/oh-my-posh
```

## Add the documentation

Create a new `markdown` file underneath the [`docs/docs`][docs] folder called `new-segment.md`.
Use the following template as a guide.

````markdown
---
id: new
title: New
sidebar_label: New
---

## What

Display something new.

## Sample Configuration

```json
{
  "type": "new",
  "style": "powerline",
  "powerline_symbol": "",
  "foreground": "#193549",
  "background": "#ffeb3b",
  "properties": {
    "newprop": "w00p"
  }
}
```

## Properties

- newprop: `string` - the new text to show
````

## Map the new documentation in the sidebar

Open [`sidebars.js`][sidebars] and add your document id (`new`) to the items of the Segments category.

## Create a pull request

And be patient, I'm going as fast as I can 🏎

[segment-go]: https://github.com/JanDeDobbeleer/oh-my-posh3/blob/main/segment.go
[themes]: https://github.com/JanDeDobbeleer/oh-my-posh3/tree/main/themes
[docs]: https://github.com/JanDeDobbeleer/oh-my-posh3/tree/main/docs/docs
[sidebars]: https://github.com/JanDeDobbeleer/oh-my-posh3/blob/main/docs/sidebars.js
