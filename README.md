colbibtex
=========

a simple and poor alternative of mcite(plus), i.e., multiple BibTeX references in one cite key.



### mcite / mciteplus mode

```latex
\cite{Bennett:2006fi,*Roberts:2010cj}
```

### collapsed entries mode

* add "targets" to `ENTRY` fields.

* add a function to resolve `collapsed` entries in your bst file, such as

```
STRINGS  { col.targets }
INTEGERS { col.length col.pos }
FUNCTION {collapse} {
  output.bibitem pop$
  "COLLAPSED ENTRY." write$ newline$

  targets 'col.targets :=
  {col.targets "" = not}
    {
      col.targets text.length$ 'col.length :=
      #1 'col.pos :=
      {col.targets col.pos #1 substring$ "," = not col.length col.pos > and }
        {col.pos #1 + 'col.pos :=}
      while$
      "% ENTRY: " write$
      col.length col.pos =
        { "" col.targets }
        { col.targets col.pos #1 + col.length   substring$
          col.targets #1           col.pos #1 - substring$}
      if$
      write$ newline$
      'col.targets :=
    }
  while$
  newline$
}
```

* add `collapsed` entries to your bib files, like

```
@Collapse{g-2_bnl2010,
  Targets = {Bennett:2006fi, Roberts:2010cj}
}
```

