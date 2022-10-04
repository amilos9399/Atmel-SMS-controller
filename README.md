# Atmel-SMS-controller with Arduino board and cheap chinesse modem
asm file
Created: 4.10.2022
Author : Milos
restart LCDa posle svakog ciklusa ispisa
ispis error i PB ready povezan na mrezu
	EE prom write on all S commands not on P commands
	
	On Arduino board with CH340 it is used TxRx0 so must be removed resistors 59 ohm R12 i R13 and chip CH340 to cut the PS, then programm the atmel 2560.	
	turn on the fuses "OCDEN", "JTAGEN", and "BOOTRST" even with warnings with ISP  6 pin connector
	then programm the board with Jtag or ISP connector.		

Status Fuses	
BODLEVEL = 4V3
OCDEN = [ ]
JTAGEN = [X]
SPIEN = [X]
WDTON = [X]
EESAVE = [ ]
BOOTSZ = 4096W_1F000
BOOTRST = [ ]
CKDIV8 = [ ]
CKOUT = [ ]
SUT_CKSEL = EXTXOSC_8MHZ_XX_16KCK_65MS

EXTENDED = 0xFC (valid)
HIGH = 0x80 (valid)
LOW = 0xFF (valid)

SMS COMMANDS - possible to send to controller with modem
SR-Time of work without reset or Power black out
S?? Status of outputs
T?? Temperature
P1x is a command for temporary switch on the first out, x is char ASCII from 1 (hex 31) to H (hex 48) multiplied by 10 minutes, means result will be the time that output No 1 will be ON.
The same is for P2x for second output, P3x and P4x third and forth output
S11 Turn on 1. out and write it to EEPROM, in case of PS failure return previous state
S10 Turn off 1. out,  and write it to EEPROM, in case of PS failure return previous state, Same for S21, S20, S31, S30, S41, S40
D? Delete all messages
UAM1=3816280xxxxx Write to EE  1 of 4 possible telephone numbers who are allowed to command to the device
UAM2=3816418xxxxx ....
	smanjeno brisanje memorije 
	povecano vreme za start up modema
	ubacen prekid napajanja radi reseta modema
	Za vreme inicijaliyacije modema prikayuje samo poruke
128radi timer 2 16 bitni 100mS
prebacivanje temp por promenjeno						
nisu isti bitovi za sbrc i sbrs ide 0-7, bst od 1-2       
Upis brojeva u EE komanda UAM1=3816280xxxxxx

Answers:
SR
Vreme rada $A(novi red) 000Dan00Sat00Min
S??
1OFF2OFF3OFF4OFF
T??


                   
