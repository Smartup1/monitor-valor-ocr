# Monitor de Valor (OCR)

Programa para Windows que monitora um valor numérico exibido na tela, por exemplo num supervisório. Você seleciona a área, define a faixa aceitável e o programa lê o número a cada poucos segundos com Tesseract OCR, tocando um alarme sonoro quando algo sai do normal.

## Quando o alarme dispara

- **Valor fora da faixa:** acima do máximo ou abaixo do mínimo, confirmado por leituras seguidas.
- **Valor parado:** o número não muda por mais tempo que o configurado.
- **Sem leitura:** o programa não consegue ler nenhum número por mais tempo que o configurado. Serve para avisar que o próprio sistema perdeu a leitura.

O alarme tem botão **RECONHECER** e rearma sozinho quando o valor volta para a faixa.

## Download

Baixe o executável pronto na aba **Releases** deste repositório. Não precisa instalar Python nem Tesseract, porque ele já vai embutido.

## Como usar

1. Abra o programa e clique em **1) Selecionar área**. Arraste sobre o número na tela e confirme com ENTER.
2. Ajuste os campos:

| Campo | Padrão | O que faz |
|---|---|---|
| Alarme se MAIS de | 210 | Limite máximo (vazio = sem limite) |
| Alarme se MENOS de | 190 | Limite mínimo (vazio = sem limite) |
| Ler a cada (segundos) | 5 | Intervalo entre leituras |
| Confirmar alarme / volta (leituras) | 3 / 1 | Leituras seguidas fora da faixa para alarmar, e dentro da faixa para rearmar |
| Alarme se parado há (s) | 30 | Alarma se o valor não mudar nesse tempo (0 = desligado) |
| Alarme se sem ler há (s) | 30 | Alarma se não conseguir ler número nesse tempo (0 = desligado) |
| Ignorar sinal | ligado | Compara pelo valor absoluto |

3. Clique em **2) INICIAR MONITORAMENTO**.
4. Quando o alarme tocar, clique em **RECONHECER ALARME** para silenciar. Ele rearma quando o valor voltar para a faixa.

O botão **Ler agora** faz uma leitura única, útil para testar a área selecionada.

**Dica:** não deixe a janela do programa em cima da área lida. Ele avisa quando isso acontece.

## Estados do alarme

| Estado | Significado |
|---|---|
| ARMADO | Pronto para disparar |
| ALARMANDO | Sirene tocando, esperando reconhecer |
| RECONHECIDO | Silenciado, aguardando o valor voltar para a faixa |

## Rodando pelo código-fonte

Requisitos: Windows e Python 3.12 ou 3.13 (versões muito novas podem não ter suporte em todas as bibliotecas).

```
pip install -r requirements.txt
python Testezap.py
```

`requirements.txt`:
```
numpy
opencv-python
pytesseract
pillow
mss
```

### Tesseract

O Tesseract não está neste repositório. Baixe o Tesseract 5 para Windows e copie `tesseract.exe`, as DLLs e a pasta `tessdata` para uma pasta chamada `Tesseract-OCR` ao lado do script:

```
Tesseract-OCR/
  tesseract.exe
  *.dll
  tessdata/
    eng.traineddata
```

Só o idioma `eng` é necessário, porque o programa lê apenas dígitos.

## Gerando o executável

```
pip install pyinstaller
python -m PyInstaller --onefile --windowed --name MonitorValor --add-data "Tesseract-OCR;Tesseract-OCR" Testezap.py
```

O arquivo fica em `dist/MonitorValor.exe`. Na primeira abertura ele pode levar alguns segundos, porque desempacota o Tesseract numa pasta temporária. Se der erro ao abrir, gere uma vez sem `--windowed` para ver a mensagem no console.

## Observações

- O OCR depende de uma boa seleção da área: pegue só o número, com bom contraste.
- Antivírus às vezes marcam executáveis do PyInstaller como suspeitos (falso positivo). Se acontecer, adicione uma exceção.
