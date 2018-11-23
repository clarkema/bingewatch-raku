# bingewatch

`bingewatch` is a utility to automatically download the most recent videos
from any YouTube channel for offline viewing.

It will download the YouTube RSS feed for the requested channel and then fetch
any videos that it doesn't already see under its working directory.

# Installation

Before getting started, ensure that you have Perl 6 (and its package manager,
`zef`) available on your system, along with `youtube-dl` and `ffmpeg`.  Once
everything's in place:

```
$ zef --force-test install Terminal::Print
$ zef install https://github.com/clarkema/bingewatch.git
```

(Note that `Terminal::Print` has issues with its test harness that mean that
`zef` doesn't see the tests as passing even though they do—hence it needing to
be installed with `--force-test`.  If you _still_ see an error about `@valid-terminals`, see the Caveats section below for a workaround.)

# Usage

For one-off usage, just run `bingewatch` and pass the name of the channel
you're interested in:

```
$ bingewatch clojuretv
```

If you want to run `bingewatch` regularly to watch a list of channels,
make a configuration file at `$HOME/.config/bingewatch/channels.txt` with one
channel name per line:

```
$ cat $HOME/.config/bingewatch/channels.txt
clojuretv
PapersWeLove
theRSAorg
```

Then run `bingewatch` with no arguments to automatically synchronise everything.

```
$ bingewatch
```

# Caveats

This is currently a very early version; there are many features that could be
added (and requests and patches are welcome) but right now it's very bare-bones.
Even so, I already find it useful for fetching talks and videos I want to watch
when travelling without a high-bandwidth connection.

One particular limitation is that `bingewatch` only works with YouTube
_users_ at the moment, not _channels_.

## Terminal::Print

`bingewatch` uses `Terminal::Print` to display download progress in a way that
copes with running multiple downloads in parallel.  However, `Terminal::Print`
only works with specific whitelisted terminals.  If you see a message along
the lines of `Please update @valid-terminals with your desired TERM...` try
running both the `zef install` command and `bingewatch` itself inside `tmux`,
which is one of the supported options.
