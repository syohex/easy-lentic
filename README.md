- [easy-lentic 使用说明](#easy-lentic-使用说明)
  - [安装](#安装)
    - [安装 easy-lentic](#安装-easy-lentic)
    - [安装 ox-gfm](#安装-ox-gfm)
  - [配置](#配置)
  - [使用](#使用)
    - [编写 org 格式的 Comment](#编写-org-格式的-comment)
    - [自动生成 README 文档](#自动生成-readme-文档)

# easy-lentic 使用说明<a id="orgheadline8"></a>

easy-lentic 是基于 lentic 的一个扩展，但它不是扩展了 lentic 的功能，而是让 lentic 更加专注于一个 **特定** 的使用场合，即：

    编写 emacs-lisp 时，使用 org 格式组织 comment。

注：[lentic](https://github.com/phillord/lentic) 是一个很有新意的包，引用作者的原话：

    Lentic allows two buffers to share the same or similar content but otherwise operate independently.
    This can be used for several different purposes.
    Different buffers can be in the same mode, with different locations of point,
    even different text sizes -- in effect, providing multiple persistent views.

    It is also possible to have the different lentic buffers in different modes,
    giving a form of multi-modal editing. Switching buffers effectively switches modes as well.

    While the content of two lentic buffers must be related, it does not need to be syntactically identical.
    This allows it to be used for a form of literate programming -- for example,
    one buffer may contain valid LaTeX source with blocks of Lisp,
    while in the other the LaTeX source is commented out, giving an entirely valid Lisp file.

    ...

## 安装<a id="orgheadline3"></a>

### 安装 easy-lentic<a id="orgheadline1"></a>

1.  配置melpa源，参考：<http://melpa.org/#/getting-started>
2.  M-x package-install RET easy-lentic RET

### 安装 ox-gfm<a id="orgheadline2"></a>

easy-lentic 可以使用 ox-gfm (Github Flavored Markdown exporter for Org Mode) 将 org 格式转换为 github markdown 格式，但这个功能需要用户 **手动安装 ox-gfm**, 具体安装方式：

1.  配置 org 源，具体请参考：<http://orgmode.org/elpa.html>
2.  M-x package-install RET org-plus-contrib RET

注意：

1.  ox-gfm 已合并到 org-plus-contrib，melpa 中找到的 ox-gfm 包已经 **停止开发** 了。
2.  如果用户没有安装 ox-gfm, 那么，easy-lentic 将使用 ox-md 后端生成 README.md。

## 配置<a id="orgheadline4"></a>

    (require 'easy-lentic)   ;; You need install lentic and gfm
    (easy-lentic-mode-setup) ;; Enable `owp/lentic-mode' for `emacs-lisp-mode' and `org-mode'

## 使用<a id="orgheadline7"></a>

### 编写 org 格式的 Comment<a id="orgheadline5"></a>

编辑 emacs-lisp 文件时，按 'C-c jj'（\`easy-lentic-switch-window'）会弹出一个
org-mode 窗口，这个窗口显示的内容和 emacs-lisp 文件内容在逻辑上具有高度的相似性。这样，comment 部份可以在 org buffer 中编辑，而 elisp 代码则可以到 emacs-lisp buffer中编辑，两个 buffer 中的内容实时自动的同步。

### 自动生成 README 文档<a id="orgheadline6"></a>

\`easy-lentic-generate-readme' 可以从当前 elisp 文件的 Commentary 部份提取相关内容，然后生成 README.md 文件，这个功能对 Commentary 的格式有一定的要求：

1.  必须使用 org 格式编写。
2.  Head1 必须包含 README tag。

比如：

    * This is Head1   :README:
    ** This is Head2
    *** This is Head3
    [[http://www.google.com][this is a link]]

    * This head1 will not export
