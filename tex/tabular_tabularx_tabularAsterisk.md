https://tex.stackexchange.com/questions/341205/what-is-the-difference-between-tabular-tabular-and-tabularx-environments/341212

```tex
\documentclass{article}

\usepackage{tabularx}

\begin{document}

\begin{tabular}{|l|c|r|}
  \hline
  foo   & bar    & fubar \\
  fubar & toobar & foo \\
  \hline
\end{tabular}

\vspace{1cm}

\begin{tabular*}{\textwidth}{@{\extracolsep{\fill}}|l|c|r|}
  \hline
  foo   & bar    & fubar \\
  fubar & toobar & foo \\
  \hline
\end{tabular*}

\vspace{1cm}

\begin{tabularx}{\textwidth}{|X|X|X|}
  \hline
  foo   & bar    & fubar \\
  fubar & toobar & foo \\
  \hline
\end{tabularx}

\end{document}
```