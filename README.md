This package helps restate theorems, lemmas, other envs again somewhere else in the document.
Unlike the popular restatable package, the location of the source code for the theorem/lemma/etc. doesn't need to be the first instance of the theorem/lemma/etc.
Also, includes the ability to provide minor alterations in the restatement.

## Example Usage

General Use
```
  \begin{restatethis}{(the env type to wrap the body in, e.g theorem, lemma)}{(a label - a hyperref label will be automatically included)}
    This is the the body of what is to be stated.
  \end{restatethis}
```


Anywhere in document the command below puts "There is a line between every two points." in a theorem environment.
```
  \begin{restatethis}{theorem}{aLabelForMyImportantTheorem}
    There is a line between every two points.
  \end{restatethis}
```
There is no need to include `\begin{theorem}...\end{theorem}` or `\label{aLabelForMyImportantTheorem}` yourself.

Anywhere else in the document, include the command below to create a verbatim copy within a theorem env (with same number).
Unlike restatable, this command can come before the restatethis env.

```
\restate{aLabelForMyImportantTheorem}
```

Note, the original and any restatements of the theorem will have the same number (e.g. Theorem 2). The number is based upon the positioning of the number of the source (`\begin{restatethis}{}{}...\end{restatethis}`).

# Additional Commands

If only the body of `\begin{restatethis}{}{}...\end{restatethis}` is desired to be copied (without the surrounding environment), the `\restateBody` command can be used.
Example
```
  \begin{lemma}
    \restateBody{aLabelForMyImportantTheorem}
    %now the body text of Important Theorem is in a lemma
  \end{lemma}
```

Note, the label also works with hyperref.
Example
```
  I am referencing \autoref{aLabelForMyImportantTheorem}.
```

If minor variations between the restatements are desired, this can be achieved with `\restateAlt` in the source version. It has the syntax 
```
  \restateAlt{(a label for enabling and disabling this option)}{the default source text when the option is not enabled}{the alternative source when the option is enabled}
```

More than one labeled option is possible.

Example
```
  \begin{restatethis}{lemma}{lemma1}
    Lots going on here. 
    \restateAlt{aLabeltoTriggerThisOpt}%
    {This is the default text that will appear in the restatethis env%
    and anywhere without aLabeltoTriggerThisOpt enabled}%
    {This will be appear when aLabeltoTriggerThisOpt is enabled}
    \restateAlt{opt2}{You can have more than 1!}{More than 1 is possible}
  \end{restatethis}

  %Somewhere else - The command below produces "Lots going on here.
  %This will be appear when aLabeltoTriggerThisOpt is enabled. More than 1 is possible."
  \restate[aLabeltoTriggerThisOpt,opt2]{lemma1}

  %Somewhere else - The command below produces "Lots going on here.
  %This is the default text that will appear in the restatethis env
  %and anywhere without aLabeltoTriggerThisOpt enabled More than 1 is possible."
  \restateBody[opt2]{lemma1}

  %or no alternatives at all - The command below produces"Lots going on here.
  %This is the default text that will appear in the restatethis env
  %and anywhere without aLabeltoTriggerThisOpt enabled You can have more than 1!."
  \restate{lemma1}
```

Labels for the options should be unique across all restatethis -es
