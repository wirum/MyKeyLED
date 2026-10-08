# LCDWiki MSP1803 — símbolo do módulo completo

Símbolo: `MyKeyLED_Local:LCDWiki_MSP1803_Module`.
Arquivo modificado: `C:/Users/Lukazz/Desktop/Half-Life/Week-01-PCB/hardware/MyKeyLed/libraries/MyKeyLED_Local.kicad_sym`.
Documento criado junto à biblioteca: `libraries/LCDWiki_MSP1803_README.md`.

## Fontes exclusivamente oficiais

- [Página MSP1803](https://www.lcdwiki.com/1.8inch_SPI_Module_ST7735S_SKU:MSP1803).
- [Esquema do módulo MSP1803](https://www.lcdwiki.com/res/MSP1803/MSP1803-1.8-SPI.pdf), folha única, 15/10/2014: conectores externos J2 e J4.
- [Manual MSP1803 Rev1.0](https://www.lcdwiki.com/res/MSP1803/1.8inch_SPI_Module_MSP1803_User_Manual_EN.pdf), tabela de interface na página 3 e descrição SPI na página 5.
- [Desenho dimensional oficial](https://www.lcdwiki.com/images/8/87/MSP1803-005.png).

Não foi utilizado o símbolo do painel cru QD1801/QDTFT1801 de 14 pinos. O conector J3 CON14 do esquema oficial é interno; seus pinos não são pinos externos deste símbolo. O símbolo inclui somente J2 CON8 e J4 CON4.

## Mapeamento dos 12 terminais

A qualificação por conector foi autorizada pelo usuário para tornar todos os terminais eletricamente únicos. `J4.1` significa o pino físico **1 de J4**, não um pino físico 9. Os nomes permanecem inalterados. Uma propriedade oculta `Physical_pin_mapping` também armazena esse mapeamento dentro do símbolo.

| Número no símbolo | Conector/pino físico | Nome | Função e tipo elétrico no símbolo |
|---|---|---|---|
| J2.1 | J2 / 1 | VCC | Entrada de alimentação 3,3–5 V; power_in |
| J2.2 | J2 / 2 | GND | Terra; power_in |
| J2.3 | J2 / 3 | CS | Seleção do TFT ativa em nível baixo; input |
| J2.4 | J2 / 4 | RESET | Reset do TFT ativo em nível baixo; input |
| J2.5 | J2 / 5 | A0 | Seleção de registro/dados; input; divergência de polaridade registrada abaixo |
| J2.6 | J2 / 6 | SDA | Dados SPI enviados ao TFT; input |
| J2.7 | J2 / 7 | SCK | Clock SPI do TFT; input |
| J2.8 | J2 / 8 | LED | Alimentação/controle do backlight; passive |
| J4.1 | J4 / 1 | SD_CS | Seleção do microSD, ligada a CS do slot via R1; input |
| J4.2 | J4 / 2 | SD_MOSI | Dados enviados ao microSD, ligada a DIN via R2; input |
| J4.3 | J4 / 3 | SD_MISO | Dados recebidos do microSD, ligada a DOUT; output |
| J4.4 | J4 / 4 | SD_SCK | Clock do microSD, ligado a CLK via R3; input |

Os tipos elétricos são a representação KiCad das funções documentadas, vistos pelo módulo. LED foi mantido passivo porque o esquema mostra ligação por R4 de 7,5 ohms ao LED+ do painel; não foi tratado como entrada lógica de um circuito buffer. A documentação diz que nível alto acende e cita 3,3 V para iluminação contínua. A tensão de IO indicada na página é 3,3 V. Isso não define conexões para o projeto.

J4 não possui VCC ou GND externos adicionais no esquema: o slot usa a alimentação de 3 V e terra internos do módulo. Os pinos do slot SD1 não foram confundidos com os quatro pinos do header J4. Os sinais TFT e microSD permanecem separados no símbolo; não foram unidos internamente por suposição.

## Divergências documentais preservadas

A página oficial descreve A0 como alto=registro e baixo=dados. O manual Rev1.0, página 5, descreve DCX baixo=comando e alto=dados. Não escolhi uma polaridade para a descrição do símbolo: ele mantém exatamente `A0`, como entrada de seleção, e registra o conflito na propriedade Description. O esquema usa o nome interno REST para RESET, mas o nome externo adotado é RESET, conforme tabela de interface e desenho mecânico.

A tabela Arduino do manual enumera sua lista de conexões em ordem inversa. A numeração física foi retirada de J2 no esquema e conferida com a tabela Interface Definition da página e com o marcador quadrado do primeiro pino no desenho, em vez de usar os números da lista Arduino.

## Dimensões e ausência de footprint

O desenho oficial informa PCB **34,50 × 58,00 mm**, centros dos furos de fixação separados por **28,50 × 52,00 mm**, margem de **3,00 mm** dos centros às bordas, furos de fixação **Ø3,20 mm**, passo indicado no header J2 de **2,54 mm** e distância indicada da linha de J2 à borda inferior de **2,50 mm**.

O desenho não fornece uma cadeia de cotas completa para a posição horizontal do J2, posição do J4, passo explicitamente cotado do J4 e diâmetro dos furos de conexão dos headers. A aparência gráfica não foi medida para preencher essas lacunas. Por isso **não foi criado footprint**, nem atribuído um footprint parcial. O campo Footprint está vazio; a biblioteca `.pretty` permanece vazia. As dimensões citadas são apenas documentais e não foram convertidas em geometria de PCB.

O retângulo do símbolo é uma apresentação lógica, sem escala mecânica. Não é uma representação dimensional do módulo.

## Verificação

O arquivo foi lido e exportado para SVG pelo KiCad 10 e a apresentação foi inspecionada. Foram conferidos 12 números únicos e o mapeamento de cada conector. A biblioteca local já estava registrada; não foi necessário modificar tabelas, bibliotecas globais, esquemático, PCB ou arquivo `.kicad_pro`. O ESP32-C3 Super Mini não foi alterado. Não foram escolhidos GPIOs ou efetuadas conexões/roteamento.
