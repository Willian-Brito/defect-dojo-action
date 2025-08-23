# 🚀 DefectDojo Integration GitHub Action

Esta GitHub Action integra-se com o [DefectDojo](https://www.defectdojo.org/) para criar produtos, engajamentos e importar relatórios de vulnerabilidades automaticamente.

O DefectDojo é uma ferramenta [open-source](https://github.com/DefectDojo/django-DefectDojo) para **gestão centralizada de vulnerabilidades**. Como uma plataforma que integra resultados de múltiplos scanners (SAST, DAST, SCA) e organiza esses achados para facilitar a gestão e priorização dos riscos.

## 📌 **Recursos**
- Cria um produto no DefectDojo (caso não exista)
- Gera um engajamento no produto
- Importa relatórios de segurança automaticamente
- Suporta ferramentas de análise como **Horusec**, **SARIF**, entre outras

---

## 📦 **Como Usar**
Você pode usar esta Action no seu workflow do GitHub adicionando o seguinte YAML ao arquivo `.github/workflows/defectdojo.yml`:

```yaml
name: DefectDojo Scan

on:
  push:
    branches:
      - main

jobs:
  defectdojo:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout do código
        uses: actions/checkout@v4

      - name: Executar DefectDojo Integration
        uses: Willian-Brito/defect-dojo-action@main
        with:
          url_base: "http://seu-defectdojo.com/api/v2/"
          username: "seu-usuario"
          source_url: "https://github.com/seu-usuario/seu-repositorio"
          tool: "Horusec"
          file: "horusec_report.sarif"
          scan_type: "SARIF"
          product_name: "Meu Projeto"
          description: "Projeto de teste no DefectDojo"
          origin: "third-party"
          token: ${{ secrets.DEFECTDOJO_TOKEN }}
