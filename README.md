# C-digo_de_Conduta_Uso_Respons-vel_da_Inteligente_Artificial.py
Esse projeto fala de consultas de como usar a Inteligência Artificial 

#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
codigo_de_conduta_ia.py

Versão em Python do "Código de Conduta — Uso Responsável de Inteligência Artificial".
Fornece o texto do código de conduta em formatos plaintext e Markdown, funções utilitárias
para exibir e salvar em arquivo, e uma interface de linha de comando simples.

Uso:
    python codigo_de_conduta_ia.py --print            # Imprime o texto em plain text no console
    python codigo_de_conduta_ia.py --format md --output codigo.md
    python codigo_de_conduta_ia.py --format txt --output codigo.txt
"""

from __future__ import annotations
import argparse
import sys
from pathlib import Path
from typing import Optional

# ---------------------------------------------------------------------------
# Conteúdo do Código de Conduta (em português)
# ---------------------------------------------------------------------------

_TITLE = "Código de Conduta — Uso Responsável de Inteligência Artificial"

_MARKDOWN = f"""# {_TITLE}

**Objetivo**  
Promover o uso seguro, ético e transparente de sistemas de inteligência artificial (IA), protegendo a dignidade, privacidade e direitos das pessoas afetadas.

## Princípios fundamentais
- Respeito à dignidade humana
- Não causar dano
- Transparência e honestidade
- Responsabilidade humana
- Justiça e não discriminação

## Regras essenciais (resumo)
1. **Identificação:** Sempre deixe claro quando algo foi gerado ou decidido por IA.  
2. **Consentimento:** Colete e use dados pessoais somente com objetivo legítimo e consentimento informado.  
3. **Privacidade:** Minimize dados, proteja-os e cumpra leis de proteção de dados.  
4. **Não discriminar:** Teste e mitigue vieses; não use IA para decisões que perpetuem desigualdades.  
5. **Supervisão:** Mantenha supervisão humana para decisões que afetem direitos, segurança ou bem‑estar.  
6. **Explicabilidade:** Forneça explicações compreensíveis quando a IA produzir decisões que impactem pessoas.  
7. **Segurança:** Teste sistemas para evitar falhas e ataques; atualize e corrija vulnerabilidades.  
8. **Proibição de uso malicioso:** Não criar ou distribuir deepfakes, desinformação, manipulação eleitoral ou qualquer uso enganoso.  
9. **Propriedade intelectual:** Respeite direitos autorais e atribua fontes quando aplicável.  
10. **Impacto e sustentabilidade:** Considere consequências sociais e ambientais; minimize impacto negativo.  

## Procedimento ao identificar dano ou risco
- Pausar o sistema afetado quando possível.  
- Registrar evidências e comunicar imediatamente aos responsáveis.  
- Oferecer apoio às pessoas prejudicadas e executar correções e mitigação.  
- Revisar processos para evitar recorrência.

## Responsabilidades dos usuários e desenvolvedores
- **Usuários:** Usar ferramentas de IA conforme indicado, reportar problemas e respeitar limites de privacidade.  
- **Desenvolvedores/Operadores:** Garantir testes, mitigação de vieses, controles de acesso, monitoramento contínuo e documentação das decisões do sistema.

## Mecanismo de denúncia e recurso
- Disponibilizar canal claro para reclamações e solicitações de revisão humana de decisões automatizadas.  
- Garantir prazo e procedimento para resposta e correção.

## Cumprimento e sanções
- Violações serão investigadas; ações podem incluir correção técnica, suspensão de acesso ou medidas disciplinares, conforme gravidade.

## Revisão
- Este código deve ser revisado periodicamente para incorporar novidades legais, técnicas e feedback dos afetados.
"""

_PLAINTEXT = f"""{_TITLE}

Objetivo
Promover o uso seguro, ético e transparente de sistemas de inteligência artificial (IA), protegendo a dignidade, privacidade e direitos das pessoas afetadas.

Princípios fundamentais
- Respeito à dignidade humana
- Não causar dano
- Transparência e honestidade
- Responsabilidade humana
- Justiça e não discriminação

Regras essenciais (resumo)
1. Identificação: Sempre deixe claro quando algo foi gerado ou decidido por IA.
2. Consentimento: Colete e use dados pessoais somente com objetivo legítimo e consentimento informado.
3. Privacidade: Minimize dados, proteja-os e cumpra leis de proteção de dados.
4. Não discriminar: Teste e mitigue vieses; não use IA para decisões que perpetuem desigualdades.
5. Supervisão: Mantenha supervisão humana para decisões que afetem direitos, segurança ou bem‑estar.
6. Explicabilidade: Forneça explicações compreensíveis quando a IA produzir decisões que impactem pessoas.
7. Segurança: Teste sistemas para evitar falhas e ataques; atualize e corrija vulnerabilidades.
8. Proibição de uso malicioso: Não criar ou distribuir deepfakes, desinformação, manipulação eleitoral ou qualquer uso enganoso.
9. Propriedade intelectual: Respeite direitos autorais e atribua fontes quando aplicável.
10. Impacto e sustentabilidade: Considere consequências sociais e ambientais; minimize impacto negativo.

Procedimento ao identificar dano ou risco
- Pausar o sistema afetado quando possível.
- Registrar evidências e comunicar imediatamente aos responsáveis.
- Oferecer apoio às pessoas prejudicadas e executar correções e mitigação.
- Revisar processos para evitar recorrência.

Responsabilidades dos usuários e desenvolvedores
- Usuários: Usar ferramentas de IA conforme indicado, reportar problemas e respeitar limites de privacidade.
- Desenvolvedores/Operadores: Garantir testes, mitigação de vieses, controles de acesso, monitoramento contínuo e documentação das decisões do sistema.

Mecanismo de denúncia e recurso
- Disponibilizar canal claro para reclamações e solicitações de revisão humana de decisões automatizadas.
- Garantir prazo e procedimento para resposta e correção.

Cumprimento e sanções
- Violações serão investigadas; ações podem incluir correção técnica, suspensão de acesso ou medidas disciplinares, conforme gravidade.

Revisão
- Este código deve ser revisado periodicamente para incorporar novidades legais, técnicas e feedback dos afetados.
"""

# ---------------------------------------------------------------------------
# Funções utilitárias
# ---------------------------------------------------------------------------

def get_markdown() -> str:
    """Retorna o texto do código de conduta em Markdown."""
    return _MARKDOWN

def get_plaintext() -> str:
    """Retorna o texto do código de conduta em plain text."""
    return _PLAINTEXT

def print_to_console(fmt: str = "txt") -> None:
    """Imprime o texto no console.
    fmt: 'txt' ou 'md' (default 'txt')
    """
    if fmt == "md":
        sys.stdout.write(get_markdown())
    else:
        sys.stdout.write(get_plaintext())

def save(path: Path, fmt: str = "txt", overwrite: bool = False) -> Path:
    """Salva o código de conduta em arquivo.
    path: caminho do arquivo de saída (Path ou str)
    fmt: 'txt' ou 'md'
    overwrite: sobrescrever se arquivo existir
    Retorna o Path salvo.
    """
    p = Path(path)
    if p.exists() and not overwrite:
        raise FileExistsError(f"O arquivo já existe: {p!s}. Use overwrite=True para sobrescrever.")
    text = get_markdown() if fmt == "md" else get_plaintext()
    p.write_text(text, encoding="utf-8")
    return p

def try_export_pdf(path: Path, fmt: str = "md") -> Optional[Path]:
    """
    Tenta exportar o conteúdo como PDF usando fpdf (simples) se disponível.
    Não é obrigatório; se a biblioteca não existir, informa ao usuário como instalar.
    Retorna o caminho do PDF criado, ou None se a exportação falhar.
    """
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
        # FPDF não lida bem com linhas muito longas — quebra manual simples:
        pdf.multi_cell(0, 7, line)
    pdf_path = path.with_suffix(".pdf")
    pdf.output(str(pdf_path))
    return pdf_path

# ---------------------------------------------------------------------------
# Interface de linha de comando
# ---------------------------------------------------------------------------

def _build_parser() -> argparse.ArgumentParser:
    p = argparse.ArgumentParser(
        description="Gera/Imprime o Código de Conduta — Uso Responsável de Inteligência Artificial"
    )
    p.add_argument(
        "--format", "-f",
        choices=("txt", "md"),
        default="txt",
        help="Formato de saída: 'txt' (plain text) ou 'md' (Markdown). Padrão: txt."
    )
    p.add_argument(
        "--output", "-o",
        help="Caminho para salvar o arquivo (opcional). Ex: codigo.md"
    )
    p.add_argument(
        "--print", "-p",
        action="store_true",
        help="Imprime o conteúdo no console."
    )
    p.add_argument(
        "--pdf",
        action="store_true",
        help="Tenta também exportar como PDF (requer 'fpdf' instalado)."
    )
    p.add_argument(
        "--overwrite",
        action="store_true",
        help="Sobrescrever arquivo de saída se já existir."
    )
    return p

def main(argv=None) -> int:
    parser = _build_parser()
    args = parser.parse_args(argv)

    if args.print or not args.output:
        # Se o usuário não especificou output, imprimimos por padrão para facilitar uso.
        print_to_console(fmt=args.format)
        if not args.output:
            return 0

    if args.output:
        out_path = Path(args.output)
        try:
            saved = save(out_path, fmt=args.format, overwrite=args.overwrite)
            print(f"\nArquivo salvo em: {saved}")
        except FileExistsError as e:
            print(f"Erro: {e}", file=sys.stderr)
            return 2
        except Exception as e:
            print(f"Falha ao salvar arquivo: {e}", file=sys.stderr)
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
