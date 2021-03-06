Para todas as questões, utilize os LEDs e/ou os botões da placa Launchpad do MSP430.

1. Escreva um código em C que pisca os LEDs ininterruptamente.
```C
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED2|LED1)

#define SetOut(pin)	 (P1DIR |= pin)
#define SetHigh(pin)	 (P1OUT |= pin)
#define SetLow(pin)	 (P1OUT &= ~pin)
#define SwitchValue(pin) (P1OUT ^= pin)
int main()
{
	WDTCTL = WDTHOLD | WDTPW;
	SetOut(LEDS); //P1DIR |= LEDS;
	SetHigh(LED2); //P1OUT |= LED2;				// Liga LED2
	SetLow(LED1); //P1OUT &= ~LED1;				// Desliga LED1
	for (;;)
	{
		SwitchValue(LED2 | LED1); // P1OUT ^= (LED2 | LED1);
	}
	return 0;
}
```
2. Escreva um código em C que pisca os LEDs ininterruptamente. No ciclo que pisca os LEDs, o tempo que os LEDs ficam ligados deve ser duas vezes maior do que o tempo que eles ficam desligados.
```C
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED2|LED1)

#define SetOut(pin)	 (P1DIR |= pin)
#define SetHigh(pin)	 (P1OUT |= pin)
#define SetLow(pin)	 (P1OUT &= ~pin)
#define SwitchValue(pin) (P1OUT ^= pin)
int main()
{
	WDTCTL = WDTHOLD | WDTPW;	// Desabilita WDT
	SetOut(LEDS); //P1DIR |= LEDS;
	for (;;)
	{
		SetHigh(LED2);
		SetLow(LED1);
		
		SetHigh(LED2);
		SetLow(LED1);

		SetHigh(LED1);
		SetLow(LED2);

		SetHigh(LED1);
		SetLow(LED2);
	}
	return 0;
}
```
3. Escreva um código em C que acende os LEDs quando o botão é pressionado.
```C
#include <msp430g2533.h>
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED2|LED1)
#define BTN BIT2

#define SetOut(pin)		 (P1DIR |= pin)
#define SetIn(pin)		 (P1DIR &= ~pin)
#define SetPullUp(pin)	 (P1REN |= pin)
#define SetPullDown(pin) (P1REN &= ~pin)
#define SetHigh(pin)	 (P1OUT |= pin)
#define SetLow(pin)		 (P1OUT &= ~pin)
#define SwitchValue(pin) (P1OUT ^= pin)

int main()
{
	WDTCTL = WDTHOLD | WDTPW;	
	SetOut(LEDS); //P1DIR |= LEDS;
	SetIn(BTN);
	SetPullUp(BTN);
	for (;;)
	{
		if (P1IN & BTN == 0)
			SetHigh(LEDS);
		else
			SetLow(LEDS);
	}
	return 0;
}
```
4. Escreva um código em C que pisca os LEDs ininterruptamente somente se o botão for pressionado.
```C
#include <msp430g2533.h>
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED2|LED1)
#define BTN BIT2

#define SetOut(pin)		 (P1DIR |= pin)
#define SetIn(pin)		 (P1DIR &= ~pin)
#define SetPullUp(pin)	 (P1REN |= pin)
#define SetPullDown(pin) (P1REN &= ~pin)
#define SetHigh(pin)	 (P1OUT |= pin)
#define SetLow(pin)		 (P1OUT &= ~pin)
#define SwitchValue(pin) (P1OUT ^= pin)

int main()
{
	WDTCTL = WDTHOLD | WDTPW;	// Desabilita WDT
	SetOut(LEDS); //P1DIR |= LEDS;
	SetHigh(LED1);
	SetLow(LED2);
	SetIn(BTN);
	SetPullUp(BTN);
	for (;;)
	{
		if (P1IN & BTN == 0)
			SwitchValue(LEDS);
		else
			SetLow(LEDS);
	}
	return 0;
}
```
5. Escreva um código em C que acende os LEDs quando o botão é pressionado. Deixe o MSP430 em modo de baixo consumo, e habilite a interrupção do botão.

```C

#include <msp430g2533.h>
#include <legacymsp430.h>
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED2|LED1)
#define BTN BIT2

#define SetOut(pin)		 (P1DIR |= pin)
#define SetIn(pin)		 (P1DIR &= ~pin)
#define SetPullUp(pin)	 (P1REN |= pin)
#define SetPullDown(pin) (P1REN &= ~pin)
#define SetHigh(pin)	 (P1OUT |= pin)
#define SetLow(pin)		 (P1OUT &= ~pin)
#define SwitchValue(pin) (P1OUT ^= pin)

int main()
{
	WDTCTL = WDTHOLD | WDTPW;	// Desabilita WDT
	SetOut(LEDS); //P1DIR |= LEDS;
	SetIn(BTN);
	SetPullUp(BTN);

	P1IE |= BTN; 
	P1IES |= BTN; 
	_BIS_SR(LPM0 + GIE);
	return 0;
}

interrupt(PORT1_VECTOR) Interrupcao_P1()
{
	SetHigh(LEDS);
	while (P1IN&BTN == 0);	
	SetLow(LEDS);
	P1IFG &= ~BTN;	
}
```
