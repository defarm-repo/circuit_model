# Markdown Conversion Guide

This guide explains how to convert Markdown files (`.md`) to other formats, with a special focus on creating PDF files using `pandoc` and a LaTeX distribution like MacTeX.

## Converting Markdown to PDF

The most powerful and flexible way to convert Markdown to PDF is by using `pandoc`, a universal document converter. `pandoc` uses a LaTeX engine in the background to produce high-quality, professional-looking PDFs.

### 1. Installation

You'll need to install two main components: `pandoc` and a LaTeX distribution.

#### Install Pandoc

If you're on macOS and use [Homebrew](https://brew.sh/), you can install `pandoc` with the following command:

```bash
brew install pandoc
```

#### Install a LaTeX Distribution (MacTeX/BasicTeX)

You have a few options for a LaTeX distribution.

*   **MacTeX:** This is a full-featured LaTeX distribution, including a graphical interface and many packages. It's a large download (several gigabytes).
*   **BasicTeX:** This is a much smaller, minimal LaTeX distribution that is often sufficient for use with `pandoc`. You can install additional packages as needed.

For most users, **BasicTeX** is the recommended starting point. You can install it with Homebrew:

```bash
brew install --cask basictex
```

After installing BasicTeX, you may need to install some additional packages using the TeX Live Manager (`tlmgr`). Open a new terminal window and run the following commands to update the manager and install essential collections:

```bash
sudo tlmgr update --self
sudo tlmgr install collection-basic collection-latex collection-latexrecommended collection-fontsrecommended
```

### 2. Conversion Command

Once you have `pandoc` and your LaTeX distribution installed, you can convert a Markdown file to PDF with a simple command.

Navigate to the directory containing your Markdown file and run:

```bash
pandoc your_file.md -o your_file.pdf
```

Replace `your_file.md` with the name of your Markdown file and `your_file.pdf` with the desired output name.

For better results, especially with fonts and Unicode characters, it's recommended to specify the `xelatex` engine:

```bash
pandoc your_file.md -o your_file.pdf --pdf-engine=xelatex
```

### 3. Converting to Other Formats

`pandoc` can convert Markdown to many other formats as well. Here are a few examples:

*   **HTML:**

    ```bash
    pandoc your_file.md -o your_file.html
    ```

*   **Microsoft Word (`.docx`):**

    ```bash
    pandoc your_file.md -o your_file.docx
    ```

*   **LaTeX (`.tex`):**

    ```bash
    pandoc your_file.md -o your_file.tex
    ```

## Advanced Usage and Tips

*   **Templates:** You can use custom LaTeX templates to control the appearance of your PDF files. Use the `--template` flag with `pandoc`.
*   **Metadata:** You can include metadata (like title, author, and date) at the beginning of your Markdown file in a YAML block:

    ```yaml
    ---
    title: My Document
    author: John Doe
    date: October 26, 2025
    ---

    Your Markdown content starts here...
    ```
*   **Table of Contents:** To automatically generate a table of contents, use the `--toc` flag:

    ```bash
    pandoc --toc your_file.md -o your_file.pdf
    ```

This guide provides the basic steps to get you started with converting Markdown files. For more detailed information and advanced options, refer to the official [pandoc documentation](https://pandoc.org/).
