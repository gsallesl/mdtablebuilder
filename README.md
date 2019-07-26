# Markdown lists to tables export tool

`mdtablebuilder` converts markdown lists to either LaTeX or HTML.

## Problem

Maintaining tables with text in a text file format (markdown, html, latex, etc) is not simple.

* Markdown tables formats are very varied and not universally supported by all platforms (github only support a couple afaik).
* Markdown tables poorly support multi-lines cells.
* Markdown tables are unreadable if the table doesn't fit in the editor screen (soft break).
* Markdown tables require editor plugins to edit efficiently (ex: emacs table mode, vim tables).
* Markdown tables are hard to parse and export.
* HTML (or LaTeX) tables require the HTML (or LaTeX) syntax to maintain the table. HTML inside a markdown file breaks the simplicity of the markdown syntax.
* HTML and LaTeX tables can also be hard to read if quite large.

## Proposed solution

 1. Maintain lists in Markdown. Prefix list entries with column name.
 2. Run `mdtablebuilder` to export to either LaTeX or HTML.

## Usage

```
./mdtablebuilder -v headers="Header1;Header2;Header3" [-v fmtout=html] file.md
```
where:
 * `"Header1;Header2;Header3"` are the column names you want to appear in the exported table.
 * `file.md` is the markdown file you want to extract the table from.
 * `-v fmtout=html` is an optional argument to generate an HTML output instead of a LaTex output (default).

### Dependencies
 * gawk

### Markdown list format

 * Note the use of the two HTML comments to delimit the list.
 * Each block of list, separated by a new line, represent a column in the resulting table.
 * The column the element goes in is indicated by the text before the ":".

```markdown
<!-- MDLISTTAB_START -->
# Android Data Protection Solutions

 * Project: Solution1 [^ref1]
   * Android (kernel) versions: 2.1
   * Granularity: File
   * Req. App. Changes: Limited to SMS, MMS, Email
   * Req. Sys. Changes: YES
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

 * Project: Solution2 [^ref2]
   * Android (kernel) versions: 2.2.1 (2.6.32)
   * Granularity: Two groups of Apps
   * Approach: Android middleware isolation + Tomoyo
   * Req. App. Changes: NO
   * Req. Sys. Changes: YES
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

 * Project: Solution3 [^ref3]
   * Android (kernel) versions: 2.1
   * Granularity: App
   * Approach: Application level policy to control other app access
   * Req. App. Changes: YES (adds a policy)
   * Req. Sys. Changes: YES (Partially)
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

 * Project: Solution4 [^ref4]
   * Android (kernel) versions: 4.0.4
   * Granularity: Groups of Apps + system service data
   * Approach: Policy based Android middleware + kernel hardening
   * Req. App. Changes: NO
   * Req. Sys. Changes: YES
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

<!-- MDLISTTAB_END -->
```

## Examples

 * The command:
```bash
# Generate LaTeX table from Markdown list in file test.md, with columns "Project;Granularity;Req. App. Changes;Req. Sys. Changes;Trusts App;Trusts System;Trusts Hardware"
./mdtablebuilder -v headers="Project;Granularity;Req. App. Changes;Req. Sys. Changes;Trusts App;Trusts System;Trusts Hardware;" test.md
```

generates: 

```latex
\begin{table}
\caption{Android Data Protection Solutions}
\begin{center}
\begin{tabular}{|c|c|c|c|c|c|c|}
Project	 & Granularity	 & Req. App. Changes	 & Req. Sys. Changes	 & Trusts App	 & Trusts System	 & Trusts Hardware\\
Solution1 \cite{ref1}	 & File	 & Limited to SMS, MMS, Email	 & YES	 & NO	 & YES	 & YES\\
Solution2 \cite{ref2}	 & Two groups of Apps	 & NO	 & YES	 & NO	 & YES	 & YES\\
Solution3 \cite{ref3}	 & App	 & YES (adds a policy)	 & YES (Partially)	 & NO	 & YES	 & YES\\
Solution4 \cite{ref4}	 & Groups of Apps + system service data	 & NO	 & YES	 & NO	 & YES	 & YES\\
\end{tabular}
\end{center}
\end{table}

```
* * *

 * The command:
```
# Same for HTML
./mdtablebuilder -v fmtout=html -v  headers="Project;Granularity;Req. App. Changes;Req. Sys. Changes;Trusts App;Trusts System;Trusts Hardware;" test.md
```

generates: 

<b>Android Data Protection Solutions</b>
<table>
<tr><th>Project</th><th>Granularity</th><th>Req. App. Changes</th><th>Req. Sys. Changes</th><th>Trusts App</th><th>Trusts System</th><th>Trusts Hardware</th></tr>
<tr><td>Solution1 (ref1)</td><td>File</td><td>Limited to SMS, MMS, Email</td><td>YES</td><td>NO</td><td>YES</td><td>YES</td></tr>
<tr><td>Solution2 (ref2)</td><td>Two groups of Apps</td><td>NO</td><td>YES</td><td>NO</td><td>YES</td><td>YES</td></tr>
<tr><td>Solution3 (ref3)</td><td>App</td><td>YES (adds a policy)</td><td>YES (Partially)</td><td>NO</td><td>YES</td><td>YES</td></tr>
<tr><td>Solution4 (ref4)</td><td>Groups of Apps + system service data</td><td>NO</td><td>YES</td><td>NO</td><td>YES</td><td>YES</td></tr>
</table>

