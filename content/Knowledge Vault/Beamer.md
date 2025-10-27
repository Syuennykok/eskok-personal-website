---
created: 2025-10-27T15:19
updated: 2025-10-27T15:20
title: "Beamer: Create slides using LaTeX"
tags:
  - SoftwareHacks
---
Beamer is a useful tool to generate slides. Here is the [Documentation](https://texdoc.org/serve/beamer/0).

Below is some issues and notes I had recorded when using Beamer.

---
# Issues

!pdfTeX error: pdflatex (file mathkerncmssi10): Font mathkerncmssi10 at 657 not found

**Causes**
`pdttex.map` is not updating automatically.

**Solutions**
```
	cd Program Files/Miktex
	initexmf --mkmaps
	initexmf --update-fndb
```
---
# XeLatex Compile Error

Refer to :https://blog.csdn.net/Haulyn5/article/details/124128533

---
# Different Text Style

```latex
	\begin[fragile]{frame}{title}{subtitle}
		\verb|text|			% show original text
		\texttt{text}		% typewriter text
		\textbf{text}		% bold
		\textit{text}		% italic
	\end{frame}
```

## fragile frame

Ref: beamer user guide
> If a frame contains fragile text, different internal mechanism are used to typeset the frame to ensure that inside the frame the character codes can be reset. The price of switching to another internal mechanism is that either you cannot use overlays or an external file needs to be written and read back (which is not always desirable).

[中文解释](https://liam.page/2019/08/26/verbatim-environments-and-frame-in-beamer/)

In summary: Fragile made compile speed slower.

---
# Code Listing syntax

```latex
\usepackage{listings}

\begin{lslisting}
	your code here...
\end{lslisting}

% or
\begin{verbatim}
	your code here...
\end{verbatim}
```
