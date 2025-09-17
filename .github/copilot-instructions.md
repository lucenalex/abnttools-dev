# AI Coding Agent Instructions for ABNT Tools

This document guides AI agents working with the ABNT Tools LaTeX package project. ABNT Tools provides LaTeX functionality for formatting documents according to ABNT (Brazilian Association of Technical Standards) guidelines.

## Project Architecture

The project follows a modular architecture with clear separation of concerns:

- `src/abnttools.sty`: Main package entry point that orchestrates other modules
- `src/abnt-core.sty`: Core functionality for basic ABNT formatting
- `src/abnt-biblatex.sty`: Bibliography and citation handling
- `src/abnt-floats.sty`: Float handling (figures, tables, etc.)
- `src/abnt-structure.sty`: Document structure elements

### Key Design Patterns

1. **Preset System**
   - Documents types are configured via presets (e.g., `academic`, `article`)
   - Presets are loaded from `abnt-preset-{name}.cfg` files
   - Example from `abnttools.sty`:
   ```latex
   \DeclareStringOption[academic]{preset}
   \ProcessKeyvalOptions*
   ```

2. **Option Processing**
   - Uses `kvoptions` package for key-value option handling
   - Options are processed in `abnttools.sty` before loading modules
   - Core setup is handled via `\abntsetup` macro

## Development Workflows

### Testing Changes
1. Create a test document in `examples/` demonstrating the feature
2. Compile with:
   ```powershell
   pdflatex -interaction=nonstopmode test-document.tex
   ```
3. Check both PDF output and `.log` file for errors

### Package Structure Conventions
- All package files use `.sty` extension
- Configuration files use `.cfg` extension
- Maintain clear section comments:
  ```latex
  %-------------------------------------------------------------------------------
  % Section Name
  %-------------------------------------------------------------------------------
  ```

## Integration Points

1. **LaTeX Package Dependencies**
   - Core dependency: `kvoptions` for option processing
   - Document dependencies in package headers using `\RequirePackage`

2. **User Configuration**
   - Via package options: `\usepackage[preset=article]{abnttools}`
   - Via setup macro: `\abntsetup{...}`
   - Custom presets: Create `abnt-preset-{name}.cfg`

## Common Tasks

1. **Adding New Features**
   - Place core functionality in appropriate module file
   - Update main package if new options needed
   - Document in `doc/abnttools-manual.tex`

2. **Error Handling**
   - Use `\PackageError` for critical issues
   - Use `\PackageWarning` for non-critical issues
   - Use `\PackageInfo` for debugging information
