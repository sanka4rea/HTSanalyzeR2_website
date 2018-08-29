+++
# Custom widget.
# An example of using the custom widget to create your own homepage section.
# To create more sections, duplicate this file and edit the values below as desired.
widget = "projects"
active = true
date = "2018-04-11"

# Note: a full width section format can be enabled by commenting out the `title` and `subtitle` with a `#`.
title = "Resources"
subtitle = "Contains the preprocessing, Hypergeometrics, Enrichment Subnetwork"

# Order that this section will appear in.
weight = 10

# Content.
# Display content from the following folder.
# For example, `folder = "project"` displays content from `content/project/`.
folder = "resources"

# View.
# Customize how projects are displayed.
# Legend: 0 = list, 1 = cards.
view = 1

# Filter toolbar.

# Default filter index (e.g. 0 corresponds to the first `[[filter]]` instance below).
filter_default = 0

# Add or remove as many filters (`[[filter]]` instances) as you like.
# Use "*" tag to show all projects or an existing tag prefixed with "." to filter by specific tag.
# To remove toolbar, delete/comment all instances of `[[filter]]` below.

[[filter]]
  name = "Preprocessing"
  tag = ".preprocessing"
  
[[filter]]
  name = "Hypergeometrics"
  tag = ".Hypergeometric"

[[filter]]
  name = "Enrichment Subnetwork"
  tag = ".Enrichment"


+++

