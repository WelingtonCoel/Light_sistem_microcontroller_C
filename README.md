# Light_sistem_microcontroller_C
Solved a trouble in one electronic board, the microcontroller PIC16f was "dead".

----------------- Disclaimer: The lines below goes to the memory of the equipament and are actually working daily.-----------------

// # Software de controle de placa de luzes e  ventilação de ambulância, elaborado por Welington V. Coelho em 23/11/2021
// # conforme parte dos procedimentos de manutenção do citado sistema
// # welingtonc12@gmail.com Cel  
#include <Projeto - Placa Ambulância.h>

int x; // variável de controle para ligar/desligar EXAUST/ASP

void main()
{
   while (TRUE)
   {
      
      
      //--------------------------------- VENT ----------------------------------------------ok
      if (input (pin_a4) == 1) // Pressionado RA4 aciona saída RA6
      {
         output_toggle (pin_A6); // Aciona saída RA6 (pino 8)
         while (input (pin_a4) == 1);
         delay_ms (250);
      }

      
      //--------------------------------- LUZ ALTA ------------------------------------------ok
      if (input (pin_a2) == 1) // Pressionado RA2 (pino 1) aciona saída RB2 (pino 8)
      {
         output_toggle (pin_b2); // Aciona saída RB2 (pino 8)
         while (input (pin_a2) == 1);
         delay_ms (250);
      }

      //--------------------------------- LUZ BAIXA -----------------------------------------ok
      if (input (pin_a3) == 1) // Pressionado RA3 (pino 2) aciona saída RB3 (pino 9)
      {
         output_toggle (pin_b3); // Aciona saída Rb3 (pino 9)
         
         while (input (pin_a3) == 1);
         delay_ms (250);
      }

      //--------------------------------- LUZ DICRÓICA ---------------------------------------ok
      if (input (pin_a7) == 1) // Pressionado RA7 (pino 16) aciona saída RB1 (pino 7)
      {
         output_toggle (pin_b1); // Aciona saída RB1 (pino 7)
         
         while (input (pin_a7) == 1);
         delay_ms (250);
      }

      //---------------------------------LUZ DE EMBARQUE -------------------------------------ok
      if (input (pin_a1) == 1) // Pressionado RA1 (pino 18) aciona saída RB5 (pino 11)
      {
         output_toggle (pin_b5); // Aciona saída RB5 (pino 11)
         
         while (input (pin_a1) == 1);
         delay_ms (250);
      }

      //---------------------------------EXAUSTOR / ASPIRADOR ---------------------------------ok
      
      
      if (input (pin_A0) ==1) // RA0 aciona as saídas RB4 e RB0, liga/desliga exaust/asp
      {
         
         while (input (pin_A0) ==1);
         
         delay_ms (50);
         
         x = x + 1; //incrementa de 1 em 1 a, ligando ou desligando saidas
      
         
         if (x == 1)
         {
            
            output_low (pin_B4); // liga led EXAUST
            output_low (pin_B0); // liga saída EXAUST
            
            output_high (pin_B6); // desliga led ASPIRA
         }

         
         if (x == 2)
         {
            
            output_high (pin_B4); //desliga led EXAUST
            output_high (pin_B0); // desliga liga saída EXAUST
            
            output_high (pin_B6); // desliga led ASPIRA
         }

         
         if (x == 3)
         {
            
            output_high (pin_B4); //desliga led EXAUST
            output_low (pin_B0); // liga saída EXAUST
            
            output_low (pin_B6); // liga led ASPIRA
         }

         
         if (x == 4)
         {
            
            output_high (pin_B4); // desliga led EXAUST
            output_high (pin_B0); // desliga liga saída EXAUST
            
            output_high (pin_B6); // desliga led ASPIRA
            
         }

         if (x == 4)
         {
            
            x = 0;
         }
      }

      
