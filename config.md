<!--
Add here global page variables to use throughout your website.
-->
+++
author = "hinagata"
mintoclevel = 2
prepath = "monotonica"

# Add here files or directories that should be ignored by Franklin, otherwise
# these files might be copied and, if markdown, processed by Franklin which
# you might not want. Indicate directories by ending the name with a `/`.
# Base files such as LICENSE.md and README.md are ignored by default.
ignore = ["node_modules/", "drafts/"]

# RSS (the website_{title, descr, url} must be defined to get RSS)
generate_rss = true
website_title = "monotonica"
website_descr = "Engimono Notebook and more"
website_url   = "https://hinata152.github.io/monotonica/"
+++

<!--
Add here global latex commands to use throughout your pages.
-->
\newcommand{\R}{\mathbb R}
\newcommand{\scal}[1]{\langle #1 \rangle}
