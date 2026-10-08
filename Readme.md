
## O que faz
Lê um número de uma área da tela via OCR e toca alarme sonoro quando:
- o valor sai da faixa (acima do máximo ou abaixo do mínimo);
- o valor fica parado por mais tempo que o configurado;
- não consegue ler nenhum número por mais tempo que o configurado.

Tem botão de reconhecer alarme e rearma sozinho quando o valor volta para a faixa.

## Como usar
1. Baixe `MonitorValor.exe` abaixo.
2. Abra, selecione a área do número, ajuste os limites e inicie o monitoramento.

Não precisa instalar Python nem Tesseract, porque ele já vai embutido.

## Build
Gerado com PyInstaller 6.22.3 em Python 3.14, no Windows 11, com o Tesseract 5 embutido (somente o idioma `eng`):

    python -m PyInstaller --onefile --windowed --name MonitorValor --add-data "Tesseract-OCR;Tesseract-OCR" Testezap.py

Para gerar você mesmo, veja a seção "Gerando o executável" do README.

## Observações
- Somente Windows.
- Na primeira abertura pode demorar alguns segundos, porque desempacota o Tesseract.
- Alguns antivírus podem marcar o executável como suspeito (falso positivo comum em programas feitos com PyInstaller).
