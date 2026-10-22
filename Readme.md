## O que faz
Monitora uma área da tela e dispara alarme sonoro quando:
- o valor numérico sai da faixa configurada (acima do máximo ou abaixo do mínimo);
- o valor fica parado por mais tempo que o limite configurado;
- não consegue ler nenhum número por mais tempo que o limite configurado;
- o texto da área muda em relação ao texto de referência;
- a cor da área muda em relação à cor de referência.

O programa suporta quatro modos:
- Número: monitora apenas o valor numérico;
- Texto: monitora se o texto da área mudou;
- Cor: monitora se a cor da área saiu da referência;
- Ambos: combina leitura numérica + texto + cor.

Tem botão de reconhecer alarme e rearma automaticamente quando a condição volta ao normal.

## Como usar
1. Baixe a versão estável do executável na seção Releases do repositório.
2. Abra o programa e clique em "1) Selecionar área".
3. Selecione a região da tela onde está o número, texto ou a cor a monitorar.
4. Ajuste o modo, os limites, as confirmações e os tempos de parado/ilegível.
5. Clique em "INICIAR" para começar o monitoramento.
6. Se quiser, use "Ler agora" para executar uma leitura imediata.

Dicas:
- Para números, configure os valores de máximo e mínimo e o limite de "Parado(s)".
- Para texto, primeiro capture o texto de referência e depois o app monitora mudanças.
- Para cor, capture a cor de referência e o app avisa quando a aparência da área divergir.
- O botão "|abs|" faz a comparação usar o valor absoluto.

Não precisa instalar Python nem Tesseract, porque o executável já embute isso.

## Build
Gerado com PyInstaller 6.22.3 em Python 3.14, no Windows 11, com Tesseract 5 embutido (somente o idioma `eng`):

    python -m PyInstaller --onefile --windowed --name MonitorValor --add-data "Tesseract-OCR;Tesseract-OCR" Testezap.py

Se quiser gerar o executável manualmente, mantenha a pasta `Tesseract-OCR` junto ao projeto e use a mesma configuração acima.

## Observações
- Somente Windows.
- Na primeira abertura pode demorar alguns segundos, porque o Tesseract é extraído em tempo de execução.
- Alguns antivírus podem marcar o executável como suspeito (falso positivo comum em programas feitos com PyInstaller).
- A janela do app fica acima das demais (`topmost`) para facilitar o monitoramento em tela.
