#models.py
from peewee import *
db = SqliteDatabase("database.db")

class Mashinalar(Model):
    mashina= CharField()
    firma = CharField()
    yil = IntegerField()
    yigil= CharField()

    class Meta:
        database = db

db.connect()
db.create_tables([Mashinalar])



#main.py
from models import Mashinalar
while True:
    def add_car():
        mashina = input("Qanaqa mashinani kiritasiz?: ")
        firma = input("Mashinani qaysi firma chiqargan?: ")
        yil= input("Qaysi yilda chiqarilga?: ")
        yigil= input("Qayerda yig'ilgan?: ")

        new_car = Mashinalar(
            mashina=mashina,
            firma=firma,
            yil=yil,
            yigil=yigil
        )
        new_car.save()


    def list_car():
        all_cars = Mashinalar.select()
        count = 0
        for car in all_cars:
            count +=1
            print(f"[{count}] - {car.mashina} {car.firma}/{car.yil} {car.yigil}")


    tanla = input("[1] Mashina qo'shish\n [2] Mashinalar ro'yxati\n\n Qaysi birini tanlaysiz?: ")    
    if tanla == "1":
      add_car()
    elif tanla == "2":
        list_car()
        
        
#Find.py        
from models import Mashinalar

qidir = input("Nima qidirmoqchisiz?: ")
alldata = Mashinalar().select()
for data in alldata:
    id = data.id
    mashina = data.mashina
    firma= data.firma
    yil = data.yil
    yigil= data.yigil

    if qidir in mashina or qidir in firma or qidir in str(yil) or qidir in yigil:
        print(f"ID: {id}")
        print(f"FIRMASI: {firma}")
        print(f"CHIQARILGAN YIL: {yil}")
        print(f"YIG'ILGAN JOYI: {yigil}")
    else:
        pass
        print("Topilmadi")       
        

