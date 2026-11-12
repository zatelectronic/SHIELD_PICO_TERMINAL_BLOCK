# SHIELD PICO TERMINAL BLOCK — Revisão R01 (organização) — 2026-11-12
Zat Electronic · KiCad 10.0 · padrão Zat (doc 11) · componentes das bibliotecas ZAT

## O que mudou
- Esquema plano -> capa A2 + 2 folhas: 02 PICO (A3), 03 BORNES (A4). Referências mantidas (U1, J1, J2, H1-H4).
- U1: símbolo e footprint da biblioteca ZAT: ZAT_Board_RaspberryPi:RASPBERRY_PI_PICO_H (3D ${ZAT_RASPBERRY_PI_3D}/RASPBERRY_PI_PICO_H.step).
  Sai o footprint SnapEDA (pads com nome GPx, origem no centro); entra o ZAT (pads 1-40, origem no pino 1).
  Posição de todos os 40 furos conferida pad a pad: 0 µm de diferença. Pad 1,508 -> 1,6 mm, furo 1,0 mm igual.
  Campos SnapEDA removidos; Manufacturer / MPN / Datasheet iguais à biblioteca.
- J1 / J2: ZAT_Connector:Screw_Terminal_01x20 (cópia do KiCad com filtro que aceita ZAT_TerminalBlock) +
  ZAT_TerminalBlock:TerminalBlock_MaiXu_MX126-5.0-20P_1x20_P5.00mm_DG306_EdgeMount
  (3D ${ZAT_3D}/BORNE KRE VARIOS/DG306-5.0-20P-12-00AH.STEP; marca do pino 1 a 0,2 mm da borda).
- Nets com o nome do pino do Pico (GP0...GP22, GP26_A0, GP27_A1, GP28_A2, RUN, 3V3_EN, ADC_VREF, 3V3, VSYS, VBUS, GND): 33 nets, iguais ao original.
- GND como símbolo de alimentação; PWR_FLAG em GND, VSYS e VBUS (alimentação vem do Pico / USB). Nenhuma severidade em "ignore".
- Campos: Value, Descrição PT, Stock Code, Package Group; title block Zat.
- Fora do pacote: teste.txt (só "teste"), .history (VS Code), backups, fp-info-cache, DRC.rpt/ERC.rpt antigos, archive_3d_models.log.

## PCB (nada de cobre movido)
- Logos ZAT (5) e KiCad: courtyard real e "Not in schematic"; KiCad virou arte da placa.
- Os 4 logos pequenos ao lado dos furos M3 foram afastados 0,50-0,80 mm do furo (o courtyard encostava no do furo).
- Referências visíveis em F.SilkS 1,0 mm, fora do corpo e longe dos textos de pinos.
- .kicad_dru só com "(version 1)".

## Biblioteca global (já gravada no PC)
- symbols/ZAT_Connector: + Screw_Terminal_01x20
- footprints/ZAT_TerminalBlock: + TerminalBlock_MaiXu_MX126-5.0-20P_1x20_P5.00mm_DG306_EdgeMount
- Mantidos da biblioteca padrão: furos MountingHole_3.2mm_M3_ISO14580.

## Pontos de projeto
- IMPORTANTE: bornes ligados direto nos pinos do RP2040: lógica 3,3 V, não tolera 5 V, sem proteção.
- ATENÇÃO: VBUS = 5 V do USB. Alimentação externa pelo VSYS (1,8-5,5 V); não injetar em VBUS com o USB ligado (sem diodo).
- ATENÇÃO: AGND está no mesmo GND (como no original). RUN em nível baixo = reset; 3V3_EN baixo desliga o 3V3.
- MELHORIA: o 3D da ZAT mostra só o Pico H (sem as barras fêmea 1x20 que o modelo antigo tinha).

## Após abrir no KiCad
1. Reiniciar o KiCad (bibliotecas atualizadas).
2. ERC no esquema.
3. PCB: B (preencher zonas) -> F8 (deve vir sem alterações) -> DRC.
