//# ArduinoNSCAD
//DSGN final project

//https://youtu.be/wTPVTj7_vtQ

/*
 * Library Example for L298N Module to control DC motors
 * 
 * This code is to control single motor. For two motor control, please open L298N_DC_2_Motors
 * this code is ready for ESP32
 * 
 * Written by Ahmad Shamshiri on Dec 24, 2019 
 * in Ajax, Ontario, Canada. www.robojax.com

 *  * This code is "AS IS" without warranty or liability. Free to be used as long as you keep this note intact.* 
 * This code has been download from Robojax.com

 */

#include <Robojax_L298N_DC_motor.h>
#include <Ps3Controller.h>

 
// motor 1 settings
#define CHA 0
#define ENA 19 // this pin must be PWM enabled pin if Arduino board is used
#define IN1 18
#define IN2 5

// motor 2 settings
#define IN3 22
#define IN4 23
#define ENB 21// this pin must be PWM enabled pin if Arduino board is used
#define CHB 1

const int CCW = 2; // do not change
const int CW  = 1; // do not change

#define motor1 1 // do not change
#define motor2 2 // do not change

// for single motor
//Robojax_L298N_DC_motor robot(IN1, IN2, ENA, CHA, true);  

// for two motors without debug information // Watch video instruciton for this line: https://youtu.be/2JTMqURJTwg
//Robojax_L298N_DC_motor robot(IN1, IN2, ENA, CHA,  IN3, IN4, ENB, CHB);

Robojax_L298N_DC_motor robot(IN1, IN2, ENA, CHA, IN3, IN4, ENB, CHB, true);

void setup() {
  Serial.begin(115200);
  robot.begin();
  //L298N DC Motor by Robojax.com

  Ps3.begin("cc:50:e3:96:32:f6");
  Serial.println("Ready.");

}

void loop() {
  
  if (Ps3.isConnected()){
    Serial.println("Connected!");
  }

   if ( Ps3.event.button_down.triangle ){
   Serial.print("Pressing the triangle button: ");
   // robot.demo(1);
   robot.rotate(motor1, 80, CW);//run motor1 at 60% speed in CW direction
   //robot.rotate(motor2, 70, CCW);//run motor1 at 60% speed in CW direction
   } else if ( Ps3.event.button_up.triangle ){
   Serial.println("Released the triangle button");
   robot.brake(1);
   //robot.brake(2);  
   } 

   if ( Ps3.event.button_down.cross ){
   Serial.print("Pressing the cross button: ");
   // robot.demo(1);
   robot.rotate(motor1, 80, CCW);//run motor1 at 60% speed in CW direction
   //robot.rotate(motor2, 70, CCW);//run motor1 at 60% speed in CW direction
   } else if ( Ps3.event.button_up.cross ){
   Serial.println("Released the cross button");
   robot.brake(1);
   //robot.brake(2);  
   } 
   
   if ( Ps3.event.button_down.up ){
   Serial.print("Pressing the up button: ");
   // robot.demo(2);
   robot.rotate(motor2, 70, CCW);//run motor1 at 70% speed in CCW direction
   } else if ( Ps3.event.button_up.up ){
   Serial.println("Released the up button");
   robot.brake(2);
   } 

   if ( Ps3.event.button_down.down ){
   Serial.print("Pressing the down button: ");
   // robot.demo(2);
   robot.rotate(motor2, 70, CW);//run motor1 at 70% speed in CW direction
   } else if ( Ps3.event.button_up.down ){
   Serial.println("Released the down button");
   robot.brake(2); 
   } 

/*
  robot.rotate(motor1, 100, CW);//run motor1 at 60% speed in CW direction
  delay(500);
  
  //robot.rotate(motor2, 100, CCW);//run motor1 at 60% speed in CW direction
  
  robot.brake(1);
  //robot.brake(2);   
  delay(500);  

  for(int i=0; i<=100; i++)
  {
    robot.rotate(motor1, i, CW);// turn motor1 with i% speed in CW direction (whatever is i) 
    delay(100);
  }
  delay(500);
  
  robot.brake(1);
  delay(1000);  
  
 for(int i=0; i<=100; i++)
  {
    robot.rotate(motor2, i, CW);// turn motor1 with i% speed in CW direction (whatever is i) 
    delay(100);
  }
  delay(2000);
  
  robot.brake(2);
  delay(2000);    
  // Robojax L298N Library. Watch video instruciton https://youtu.be/2JTMqURJTwg
  */
}
