# IEEE Latex Template Repository

A highly structured, modular LaTeX template for preparing and writing academic papers for IEEE conferences and journals. This repository splits a traditional monolithic `main.tex` file into modular components (sections, metadata, macros, and figures), making collaboration, version control, and multi-author editing seamless.

Additionally, this repository comes equipped with automated continuous integration (CI) via GitHub Actions to automatically compile and build your paper into a PDF on every commit.

> [!NOTE]
> This repository uses the [official IEEE Latex template](https://www.ieee.org/conferences/publishing/templates), adding additional utilities and opinionated code organization on top of it.

---

## 📁 Repository Structure

```text
├── .github/workflows/
│   └── build_latex.yaml       # GitHub Actions CI configuration for auto-compilation
├── build/
│   └── main.pdf               # Compiled output PDF target
├── figures/
│   └── figure.pdf             # Vector or raster figures/images
├── meta/
│   ├── authors.tex            # Author details, affiliations, and blocks
│   ├── macros.tex             # Custom commands, packages, and shortcuts
│   └── references.bib         # BibTeX bibliography database
├── sections/
│   ├── _index.tex             # Order/orchestration file for sections
│   ├── 00-abstract.tex        # Abstract and keywords
│   ├── 01-introduction.tex    # Section 1: Introduction
│   ├── 02-related-work.tex    # Section 2: Related Work
│   ├── 03-methodology.tex     # Section 3: Methodology
│   ├── 04-results.tex         # Section 4: Experimental Results
│   └── 05-conclusion.tex      # Section 5: Conclusion & Future Work
├── IEEEtran.bst               # Official IEEE bibliography style file
├── IEEEtran.cls               # Official IEEE template class file
├── main.tex                   # Core compiler entry point
└── .gitignore                 # Standard LaTeX git ignore rules

```

---

## 🚀 Getting Started with Overleaf

Overleaf is the easiest way to write your paper collaboratively online without installing any local LaTeX distribution.

### Step 1: Create a Zip Archive

1. Download this repository as a `.zip` file from GitHub (`Code` -> `Download ZIP`).
2. Alternatively, if you have cloned it locally, compress the root directory files into a standard `.zip` folder.

### Step 2: Upload to Overleaf

1. Go to [Overleaf](https://www.overleaf.com/) and log into your account.
2. Click on **New Project** -> **Upload Project**.
3. Drag and drop your downloaded `.zip` file. Overleaf will automatically unpack the folder structure.

### Step 3: Configure Settings

1. Open the project in Overleaf.
2. Ensure that **`main.tex`** is set as the **Main document** (look for the file icon with a tiny arrow or verify via the Overleaf Menu on the top-left).
3. Ensure the Compiler is set to **pdfLaTeX** (Default) or **TeX Live 2023/2024+** inside the Menu settings.
4. Click **Recompile** to view the rendered template.

---

## 💻 Local Compilation Setup

If you prefer to work offline using an IDE (e.g., VS Code, TeXstudio, Vim) and a local LaTeX environment, follow these steps:

### Prerequisites

You need a TeX distribution and a bibliography processor installed on your machine:

* **Windows:** [MiKTeX](https://miktex.org/) or [TeX Live](https://www.tug.org/texlive/)
* **macOS:** [MacTeX](https://www.tug.org/mactex/)
* **Linux:** `texlive-full` package (e.g., `sudo apt install texlive-full`)

### Method A: Using a LaTeX IDE (Recommended for Beginners)

1. Open the folder in an IDE like **TeXstudio** or **VS Code** (with the *LaTeX Workshop* extension).
2. Set the entry point to `main.tex`.
3. Run the Build tool or use the shortcut (`Ctrl+Alt+B` in VS Code) to compile. The workspace will run `pdflatex` and `bibtex` in the correct order.

### Method B: Using Command Line (CLI)

Navigate to the root directory of the cloned repository and execute the standard compilation sequence to resolve citations and cross-references properly:

```bash
# 1. Compile the main document to generate auxiliary files
pdflatex main.tex

# 2. Process the bibliography references
bibtex main

# 3. Re-compile to map citations
pdflatex main.tex

# 4. Final compilation to fix all cross-references and page numbers
pdflatex main.tex

```

*Note: If you have `latexmk` installed, you can simply run:*

```bash
latexmk -pdf main.tex

```

---

## ✍️ How to Write & Organize Content

To keep your workspace clean, do **not** modify `main.tex` for drafting paragraphs. Instead, utilize the specialized sub-folders:

### 1. Editing Metadata & Macros

* **`meta/authors.tex`**: Modify author names, department names, organization affiliations, and email addresses.
* **`meta/macros.tex`**: Include additional LaTeX packages here (e.g., `\usepackage{amsmath}`) and define any custom macros or mathematical shorthand notations.
* **`meta/references.bib`**: Paste your BibTeX citations here. Reference them in your sections using standard tags: `\cite{citation_key}`.

### 2. Writing Paper Sections

* Open the **`sections/`** directory.
* Write your text inside the designated `.tex` files (`01-introduction.tex`, etc.).
* If you need to add a new section or change the order, modify **`sections/_index.tex`** where the `\input{...}` directives are structured.

### 3. Adding Figures

* Place your image files (PDF, PNG, JPEG) inside the `figures/` directory.
* Include them in your text files using relative paths:
```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=\linewidth]{figures/figure.pdf}
    \caption{Your Figure Caption Here.}
    \label{fig:my_figure}
\end{figure}

```



---

## 🤖 Continuous Integration (GitHub Actions)

This repository includes a `.github/workflows/build_latex.yaml` file. Whenever you push a commit or open a Pull Request on GitHub:

1. An automated virtual workflow triggers.
2. It compiles your modular LaTeX source files using a secure TeX Live environment.
3. It ensures there are no critical syntax errors or failing compilation dependencies, guaranteeing your paper is always in a buildable state.

