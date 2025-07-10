; Macros for MMC1 projects

; Memory-mapped register addresses

MMC1_CTRL_REG  =$8000
MMC1_CHR0_REG  =$A000
MMC1_CHR1_REG  =$C000
MMC1_PRG_REG   =$E000

; Inject the MMC1 reset stub in every PRG bank
; https://wiki.nesdev.com/w/index.php/Programming_MMC1#PRG_banks
.macro mmc1_inject_resetstub segname
  .segment segname
    .scope
      mmc1_resetstub_codeblock:
        sei
        ldx #$FF
        txs
        stx MMC1_CTRL_REG
        jmp start
        .addr nmi, mmc1_resetstub_codeblock, $0000
    .endscope
.endmacro

; Macro to stream to the (serial) MMC1 register
.macro mmc1_register_write addr
  .repeat 4
    sta addr
    lsr
  .endrepeat
  sta addr
.endmacro
