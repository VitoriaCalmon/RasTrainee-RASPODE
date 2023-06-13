#define alarme 4
#define led 2
#define bomba 9
#define infra 6      
#define bot200 10
#define bot500 11
#define bot800 12

int leiturabot200, leiturabot500, leiturabot800;
bool copo=0;       //distância inadequada
int tempoAnterior =0, tempo_vol =0;
double deftempoAnterior;


void setup()
{

  pinMode(alarme, OUTPUT);
  pinMode(bomba, OUTPUT);
  pinMode(led, OUTPUT);
  pinMode(infra, INPUT);
  pinMode(bot200, INPUT_PULLUP);
  pinMode(bot500, INPUT_PULLUP);
  pinMode(bot800, INPUT_PULLUP);
  
  Serial.begin(9600);
}

void loop()
{
  Serial.print("leitura200: ");
  Serial.println(leiturabot200);
  Serial.print("leitura500: ");
  Serial.println(leiturabot500);
  Serial.print("leitura800: ");
  Serial.println(leiturabot800);
  Serial.print("INFRA: ");
  Serial.println(infra);

  copo= digitalRead(infra);

  leiturabot200 = digitalRead(bot200);
  leiturabot500 = digitalRead(bot500);
  leiturabot800 = digitalRead(bot800);
  
  if(copo == 1){
  
    if(leiturabot200==1){
    tempo_vol=2500;
    }
      if(millis()- deftempoAnterior >= tempo_vol){ 
          deftempoAnterior = millis();
          digitalWrite(bomba, HIGH);
          digitalWrite(led, HIGH);
      }
      else{
          digitalWrite(bomba, LOW);
          digitalWrite(led, LOW);
          tone(alarme, 261,500);
          delay(2000);
          noTone(alarme);
          copo=0;
    }
    if(leiturabot500==1){
    tempo_vol=5300;
      if(millis()- deftempoAnterior >= tempo_vol){ 
          deftempoAnterior = millis();
          digitalWrite(bomba, HIGH);
          digitalWrite(led, HIGH);
      }
      else{
          digitalWrite(bomba, LOW);
          digitalWrite(led, LOW);
          tone(alarme, 261,500);
          delay(2000);
          noTone(alarme);
          copo=0;
      }
  }
   if(leiturabot800==1){
    tempo_vol=8000;
      if(millis()- deftempoAnterior >= tempo_vol){ 
          deftempoAnterior = millis();
          digitalWrite(bomba, HIGH);
          digitalWrite(led, HIGH);
      }
      else{
          digitalWrite(bomba, LOW);
          digitalWrite(led, LOW);
          tone(alarme, 261,500);
          delay(2000);
          noTone(alarme);
          copo=0;
      }
   }
}
}
