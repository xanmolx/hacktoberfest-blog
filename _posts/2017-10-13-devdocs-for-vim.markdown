---
layout: post
title: Devdocs.io for Vim
author: Charles Maresh
twitter: https://twitter.com/cmaresh
website: https://maresh.us
github: https://github.com/zorab47
---

# DevDocs for vim

I've used [DevDocs.io][dd] for quite a while now and find it so very helpful. It has all the docs you might find in an app like Dash, but available in the browser on all OSes (it works offline too). If you aren't using a documentation tool already, I highly recommend [DevDocs][dd].

Once you're familiar with DevDocs, I suggest integrating it with your editor. There are probably many integrations but I'll be covering the installation of [devdocs.vim][ddv] to quickly access docs from vim.

## Installing devdocs.vim

Install the plugin using your vim plugin manager of choice, I like [vim-plug][p]. Add the following to your `.vimrc` between the plug begin/end functions:

```vimscript
" In your .vimrc
Plug 'rhysd/devdocs.vim'
```

Also, setup some basic configuration that scopes the search to specific sections of the documentation. Below we'll setup ruby files to search within Rails and JavaScript JSX files to search React.

```vimscript
" In your .vimrc:

let g:devdocs_filetype_map = {
    \   'ruby': 'rails',
    \   'javascript.jsx': 'react',
    \   'javascript.test': 'chai',
    \ }
```

Then install the plugin from within vim:

```vimscript
:source ~/.vimrc
:PlugInstall
```

## Rapid Doc Lookups

Now you can call `:DevDocsAll [search-term]` or `:DevDocsUnderCursor` to open the documentation of the word under your cursor, but this can be improved. Mapping `K`, which is normally the command to find documentation in the man pages, to instead open DevDocs making the flow much better:

```vimscript
" In your .vimrc:
nmap K <Plug>(devdocs-under-cursor)
```

Now anytime you'd like to find more information in the docs, hit the `K` in normal mode. It will open your browser to DevDocs with the search pre-filled for that specific word.

[dd]: https://devdocs.io
[ddv]: https://github.com/rhysd/devdocs.vim 
[p]: https://github.com/junegunn/vim-plug
