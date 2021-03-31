# flat's guix channel

This is a personal collection of [GNU Guix][guix] package definitions.  Refer
to the manual for more information on [Guix Channels][guix-channel].

## Packages

### emacs-native-comp

Emacs built from the experimental `feature/native-comp` branch, which adds
support for native compilation of Elisp.

See [GccEmacs][gccemacs] for more information.

### emacs-pgtk-native-comp

Emacs built from an unofficial `pgtk-nativecomp` branch, which is a merge of
the `feature/pgtk` and `feature/native-comp` branches on savannah.  PGTK
provides a "pure" GTK3 rendering engine, bringing support for Wayland and
improved performance on X.

See [masm11's branch][masm11-pgtk] for more information on PGTK.

See [fejfighter's branch][fejfighter-pgtk] for the original pgtk-nativecomp
merge.

This package builds from [my pgtk-nativecomp branch][flatwhatson-pgtk] which
is frequently updated from the upstream branches on savannah.

### libgccjit-10

An updated `libgccjit` package based on `gcc-10`.  The `libgccjit` package in
Guix is based on `gcc-9`, which is missing some changes that are important for
`emacs-native-comp` performance.

## Usage

### via load-path

The simplest way to use this channel is to temporarily add it to Guix's
load-path:

``` shell
git clone https://github.com/flatwhatson/guix-channel.git
guix install -L ./guix-channel emacs-native-comp
```

### via channels.scm

A more permanent solution is to configure Guix to use this channel as an
*additional channel*.  This will extend your package collection with
definitions from this channel.  Updates will be received (and authenticated)
with `guix pull`.

To use the channel, add it to your configuration in
`~/.config/guix/channels.scm`:

``` scheme
(cons* (channel
        (name 'flat)
        (url "https://github.com/flatwhatson/guix-channel.git")
        (introduction
         (make-channel-introduction
          "33f86a4b48205c0dc19d7c036c85393f0766f806"
          (openpgp-fingerprint
           "736A C00E 1254 378B A982  7AF6 9DBE 8265 81B6 4490"))))
       %default-channels)
```

With the channel configured, it can be used as follows:

``` shell
guix pull
guix search emacs-native-comp
guix install emacs-native-comp
```

## License

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation, either version 3 of the License, or (at your option) any later
version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program.  If not, see <http://www.gnu.org/licenses/>.

See [COPYING](COPYING) for details.

[guix]: https://guix.gnu.org/
[guix-channel]: https://guix.gnu.org/manual/en/html_node/Channels.html
[gccemacs]: https://www.emacswiki.org/emacs/GccEmacs
[masm11-pgtk]: https://github.com/masm11/emacs/tree/pgtk
[fejfighter-pgtk]: https://github.com/fejfighter/emacs/tree/pgtk-nativecomp
[flatwhatson-pgtk]: https://github.com/flatwhatson/emacs/tree/pgtk-nativecomp
