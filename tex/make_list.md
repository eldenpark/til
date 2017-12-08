```tex
\newcommand{\mySubHeadingDescStart}{
  % \begin{list}{}{\leftmargin=\parindent\rightmargin=0pt}
  \begin{enumerate}[noitemsep,topsep=0pt,leftmargin=*]
    \vspace{3pt}
}
\newcommand{\mySubHeadingDescEnd}{
  % \end{list}
  \end{enumerate}
  \vspace{4pt}
}
\newcommand{\mySubHeadingDescItem}[1]{
  % \vspace{-20pt}
  \item[-] \hspace{-2pt}#1
}
```