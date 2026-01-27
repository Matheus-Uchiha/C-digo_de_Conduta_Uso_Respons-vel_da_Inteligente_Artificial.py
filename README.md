# Code of Conduct for Responsible Use of Artificial Intelligence.py

This project discusses queries on how to use Artificial Intelligence.

#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
code_of_conduct_ia.py

Python version of the "Code of Conduct — Responsible Use of Artificial Intelligence".
Provides the code of conduct text in plaintext and Markdown formats, utility functions
to display and save to a file, and a simple command-line interface.

Usage:

python code_of_conduct_ia.py --print # Prints the text in plain text to the console
python code_of_conduct_ia.py --format md --output code.md

python code_of_conduct_ia.py --format txt --output code.txt
"""

from __future__ import annotations
import argparse
import sys
from pathlib import Path
from typing import Optional

# ---------------------------------------------------------------------------
# Code of Conduct Content (in Portuguese)
# ---------------------------------------------------------------------------

_TITLE = "Code of Conduct — Responsible Use of Artificial Intelligence"

_MARKDOWN = f"""# {_TITLE}

**Objective** 
To promote the safe, ethical, and transparent use of artificial intelligence (AI) systems, protecting the dignity, privacy, and rights of the people affected.

## Fundamental Principles
- Respect for human dignity
- Do no harm
- Transparency and honesty
- Human responsibility
- Justice and non-discrimination

## Essential Rules (summary)
1. **Identification:** Always make it clear when something was generated or decided by AI.

2. **Consent:** Collect and use personal data only for legitimate purposes and Informed consent.

3. **Privacy:** Minimize data, protect it, and comply with data protection laws.

4. **Non-discrimination:** Test for and mitigate biases; do not use AI for decisions that perpetuate inequalities.

5. **Oversight:** Maintain human oversight for decisions that affect rights, safety, or well-being.

6. **Explainability:** Provide understandable explanations when AI makes decisions that impact people.

7. **Security:** Test systems to prevent failures and attacks; update and fix vulnerabilities.

8. **Prohibition of malicious use:** Do not create or distribute deepfakes, disinformation, election manipulation, or any deceptive use.

9. **Intellectual property:** Respect copyright and attribute sources when applicable.

10. **Impact and sustainability:** Consider social and environmental consequences; minimize negative impact.

## Procedure when identifying harm or risk
- Pause the affected system when Possible.

- Record evidence and immediately report it to those responsible.

- Offer support to affected individuals and implement corrections and mitigation measures.

- Review processes to prevent recurrence.

## User and Developer Responsibilities
- **Users:** Use AI tools as directed, report issues, and respect privacy boundaries.

- **Developers/Operators:** Ensure testing, bias mitigation, access controls, continuous monitoring, and documentation of system decisions.

## Reporting and Appeal Mechanism
- Provide a clear channel for complaints and requests for human review of automated decisions.

- Ensure a timeframe and procedure for response and correction.

## Compliance and Sanctions
- Violations will be investigated; actions may include technical correction, suspension of access, or disciplinary measures, depending on severity.

## Review
- This code should be reviewed periodically to incorporate new legal and technical developments and feedback from those affected.

""

_PLAINTEXT = f"""{_TITLE}

Objective
To promote the safe, ethical, and transparent use of artificial intelligence (AI) systems, protecting the dignity, privacy, and rights of affected individuals.

Fundamental Principles
- Respect for human dignity
- Do no harm
- Transparency and honesty
- Human responsibility
- Justice and non-discrimination

Essential Rules (summary)
1. Identification: Always make it clear when something was generated or decided by AI.
2. Consent: Collect and use personal data only for legitimate purposes and with informed consent.
3. Privacy: Minimize data, protect it, and comply with data protection laws.
4. Non-discrimination: Test and mitigate biases; do not use AI for decisions that perpetuate inequalities.
5. Oversight: Maintain human oversight for decisions that affect rights, safety, or well-being.
6. Explainability: Provide understandable explanations when AI produces decisions that impact people.
7. Safety: Test systems to prevent failures and Attacks; update and fix vulnerabilities.
8. Prohibition of malicious use: Do not create or distribute deepfakes, disinformation, election manipulation, or any deceptive use.
9. Intellectual property: Respect copyright and attribute sources when applicable.
10. Impact and sustainability: Consider social and environmental consequences; minimize negative impact.

Procedure when identifying harm or risk 
- Pause the affected system when possible.

- Record evidence and immediately report it to those responsible.

- Offer support to affected individuals and implement corrections and mitigation measures.

- Review processes to prevent recurrence.

User and Developer Responsibilities
- Users: Use AI tools as directed, report issues, and respect privacy boundaries.

- Developers/Operators: Ensure testing, bias mitigation, access controls, continuous monitoring, and documentation of system decisions.

Reporting and Appeal Mechanism
- Provide a clear channel for complaints and requests for human review of automated decisions.

- Ensure a timeframe and procedure for response and correction.

Compliance and Sanctions
- Violations will be investigated; actions may include technical correction, suspension of access, or disciplinary measures, depending on severity.

Review
- This code should be reviewed periodically to incorporate new legal and technical developments and feedback from those affected.

""

# ---------------------------------------------------------------------------
# Utility Functions
 # ---------------------------------------------------------------------------

def get_markdown() -> str:

""Returns the code of conduct text in Markdown."""

return _MARKDOWN

def get_plaintext() -> str:

""Returns the code of conduct text in plain text."""

return _PLAINTEXT

def print_to_console(fmt: str = "txt") -> None:

""Prints the text to the console.
fmt: 'txt' or 'md' (default 'txt')

""

if fmt == "md":
sys.stdout.write(get_markdown())

else:

sys.stdout.write(get_plaintext())

def save(path: Path, fmt: str = "txt", overwrite: bool = False) -> Path:

""Saves the code of conduct to a file.
path: path to the output file (Path or str)

fmt: 'txt' or 'md'
overwrite: overwrite if file exists
Returns the saved Path.

""
p = Path(path)
if p.exists() and not overwrite:
raise FileExistsError(f"The file already exists: {p!s}. Use overwrite=True to overwrite.")

text = get_markdown() if fmt == "md" else get_plaintext()

p.write_text(text, encoding="utf-8")

return p

def try_export_pdf(path: Path, fmt: str = "md") -> Optional[Path]:

""
Attempts to export the content as a PDF using fpdf (plain) if available.

Not mandatory; if the library does not exist, informs the user how to install it.

Returns the path of the created PDF, or None if the export fails.

""
try:
from fpdf import FPDF
except Exception:
        return None

    text = get_markdown() if fmt == "md" else get_plaintext()
    pdf = FPDF()
    pdf.set_auto_page_break(auto=True, margin=15)
    pdf.add_page()
    pdf.set_font("Arial", size=12)
    for line in text.splitlines():
        # FPDF doesn't handle very long lines well — simple manual wrapping:
        pdf.multi_cell(0, 7, line)
     pdf_path = path.with_suffix(".pdf")
    pdf.output(str(pdf_path))
    return pdf_path

# ---------------------------------------------------------------------------

# Command-line interface
# ---------------------------------------------------------------------------

def _build_parser() -> argparse.ArgumentParser:

p = argparse.ArgumentParser(
description="Generates/Prints the Code of Conduct — Responsible Use of Artificial Intelligence"

)

p.add_argument(
"--format", "-f",
choices=("txt", "md"),
default="txt",
help="Output format: 'txt' (plain text) or 'md' (Markdown). Default: txt."

)

p.add_argument(
"--output", "-o",
help="Path to save the file (optional). Ex: code.md"

)

p.add_argument(
"--print", "-p",
action="store_true",
help="Prints the content in console."

)
p.add_argument(
"--pdf",
action="store_true",
help="Also try exporting as PDF (requires 'fpdf' installed)."

)
p.add_argument(
"--overwrite",
action="store_true",
help="Overwrite output file if it already exists."

)

return p

def main(argv=None) -> int:

parser = _build_parser()

args = parser.parse_args(argv)

if args.print or not args.output:

# If the user did not specify output, we print by default for ease of use.

print_to_console(fmt=args.format)
        if not args.output:
            return 0

    if args.output:
        out_path = Path(args.output)
        try:
            saved = save(out_path, fmt=args.format, overwrite=args.overwrite)
            print(f"\nFile saved in: {saved}")
        except FileExistsError as e:
            print(f"Error: {e}", file=sys.stderr)
            return 2
        except Exception as e:
            print(f"Failed to save file: {e}", file=sys.stderr)
            return 3
 
        if args.pdf:
            pdf_path = try_export_pdf(saved, fmt=args.format)
            if pdf_path:
                print(f"PDF exportado em: {pdf_path}")
            else:
                print("Exportação para PDF não disponível. Instale 'fpdf' (pip install fpdf) para habilitar.", file=sys.stderr)

    return 0

if __name__ == "__main__":
    raise SystemExit(main())
