# Supercharge Your Vim With CTags

Source: https://blog.sensible.io/2014/05/09/supercharge-your-vim-into-ide-with-ctags.html

CTags generates index file of all your classes, methods and all other identifiers. You can use that index in your editor to jump straight to the methods you’re interested in. In this article, I’ll show you how to use them with Vim and Rails.

 ## Installation

You need to install Exuberant CTags, on OSX just run
```
$ brew install ctags
```

or on Ubuntu/Debian
```
$ sudo apt-get install exuberant-ctags
```

## Generating CTags manually
In your rails project you can generate CTags for you project with
```
$ ctags -R --languages=ruby --exclude=.git --exclude=log .
```

But what about generating CTags for our bundled libraries too? Easy task, let’s add bundle paths
```
$ ctags -R --languages=ruby --exclude=.git --exclude=log . $(bundle list --paths)
```

## Usage
You can jump into the method with
```
:ta attr_accessor
```

or using regular expressions like that
```
:ta /^before_*
```

* If you position cursor over the method and hit `CTRL+]` it will take you into the method.
* `CTRL-T` will take you back from that method.
* `CTRL-I` and `CTRL-O` will take you In and Out from the method.

```
:ts [expr]  # Lists tags matching expression
:[count]tn  # Jumps to the next matching tag
:[count]tp  # Jumps to the previous matching tag
:[count]tf  # Jumps to the first matching tag
:[count]tl  # Jumps to the last matching tag
```

## CtrlP
If you’re using CtrlP, you can use CtrlPTag to browser your tags. You can bind that command to a key and add this line to your .vimrc
```
nnoremap <leader>. :CtrlPTag<cr>
```

## Getting Advanced
Since we want to DRY this workflow a little, we’ll install Ruby gem to auto-generate those tags for us.

We’ll be using [Guard-CTags-Bundler](https://github.com/ivalkeen/guard-ctags-bundler)

Install the gem:
```
$ gem install guard-ctags-bundler
```

Add it to your Gemfile (inside development group):
```
group :development do
  gem 'guard-ctags-bundler'
end
```

Now add it to your Guardfile with
```
$ guard init ctags-bundler
```

Now you can run `guard` and it will start watching your files will generate tags and gems.tags files. Since Vim is not looking for gems.tags by default, you’ll need to edit your .vimrc and add `set tags+=gems.tags` line, then restart Vim.

## .gitignore
Since you don’t want to commit those files into the GIT index, add them to *.gitignore* or I like to add them to my global *~/.gitignore*.
```
$ cat <<EOT >> ~/.gitignore
tags
gems.tags
EOT
```

Path depends on your configuration 
```
git config --global core.excludesfile "~/.gitignore"
```

## Questions?
Vim has very nice build-in help that can be accessed by
```
:help tags
```

## Bonus: Inspecting Gems
I like to inspect Gems a lot. Just set your `$EDITOR` variable and then run command `bundle open rails` to open it in your favourite editor. I recommend you to try Tim Pope’s automatic RubyGems CTags invoker [gem-ctags](https://github.com/tpope/gem-ctags).

Just install the gem
```
$ gem install gem-ctags
```

and generate CTags for already installed Gems (needs to be run only first time).
```
$ gem ctags
```
