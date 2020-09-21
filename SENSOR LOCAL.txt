
import RPi.GPIO as GPIO
import datetime
import paho.mqtt.client as mqtt 
import time
GPIO.setmode(GPIO.BOARD)
GPIO.setup (11, GPIO.IN)
GPIO.setup (7, GPIO.IN)
GPIO.setup (12, GPIO.OUT)
GPIO.setup (13, GPIO.OUT)
f=open("Registro.txt","w")
named_tuple = time.localtime() # get struct_time

horaActual=datetime.datetime.now().strftime("%m/%d/%Y, %H : %M : %S")


c=0
def ejecutar():
        if GPIO.input(7):
          GPIO.output(12, True)
          print("Sensor 1 activado: Led 1 Encendido")
          time.sleep(1)
          m=("Sensor 1 activado: Led 1 Encendido")
          #rc = mqttc.loop()
          mqttc.publish("654hector1@gmail.com/test", m)
          #=i+1
          #c=c++1;
          f.write(str("Sensor 1 activado: Led 1 Encendido  ")+horaActual +str("      Estado:   Boton 1 Aplastado") +"\n")         
          time.sleep(1)
        
        else:
          GPIO.output(12, False)
          print("Sensor 1 desactivado: Led 1  Apagado")
          des=("Sensor 1 desactivado: Led 1  Apagado")
          f.write(str(" Sensor 1 desactivado: Led 1  Apagado") +"\n")
          mqttc.publish("654hector1@gmail.com/test",des )
	 
          time.sleep(1)
        if GPIO.input(11):
          GPIO.output(13, True)
          print("boton activado")
          time.sleep(1)
          m1=("Sensor 2 activado: Led 2 Encendido")
          mqttc.publish("654hector1@gmail.com/test", m1)
          #rc = mqttc.loop()
          #mqttc.publish("ruberchiles@hotmail.es/test","Sensor="+"Valor:"+str(i)+"                 Fecha y Hora:"+str(horaActual))
          i#=i+1
          #c=c++1;
          f.write(str("Sensor 2 activado: Led 2 Encendido  ")+horaActual +str("      Estado:   Boton 2 Aplastado") +"\n")         
          time.sleep(1)
        
        else:
          GPIO.output(13, False)
          print("boton desactivado")
          des2=("Sensor 2 desactivado: Led 2 apagado")
          mqttc.publish("654hector1@gmail.com/test", des2)
          f.write(str(" Sensor 2 desactivado: Led 2  Apagado") +"\n")
	 
          time.sleep(1)   

def on_message(client, obj, msg):    
	accion=(msg.payload.decode("utf-8"))
	clave="1234"
	print(accion)
	if accion==clave:
	    ejecutar()
	
	
mqttc = mqtt.Client()
mqttc.on_message = on_message
mqttc.username_pw_set("654hector1@gmail.com", "naruto798199429")
mqttc.connect("maqiatto.com",1883)
mqttc.subscribe("654hector1@gmail.com/kop", 0)
rc=0
print("Conectado...")
i=0

while rc == 0:
	time.sleep(2)
	rc = mqttc.loop()
	es=ejecutar()
	horaActual=datetime.datetime.now().strftime("%m/%d/%Y, %H : %M : %S")
	#mqttc.publish("654hector1@gmail.com/test", "sensor  "+str(i))
	i=i+1
      
      

def main ():

    print("fin")
    while(1):
     f.close()
     pass
#main()
