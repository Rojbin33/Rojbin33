#pgzero
import random
 
WIDTH = 1000         
HEIGHT = 600
 
TITLE = "balık"
FPS = 30
 
arka= Actor("arkaplan")
fish=Actor("fish",(50,900))
son=Actor("son")
akvaryum=Actor("menu")
start=Actor("start3",(450,500))
puan=1                                    
kaplumbagalar=[]
baliklar=[]
baliklar2=[]
kopekler=[]
mod= "menu"
for i in range(5):
    x = random.randint(1200, 1400)
    y = random.randint(0,1000)
    kaplumbaga=Actor("kaplumbaga",(x,y))
    kaplumbaga.speed = random.randint(2, 8)
    kaplumbagalar.append(kaplumbaga)
for i in range(7):
    x = random.randint(1200, 1400)
    y = random.randint(0,1000)
    balik=Actor("balik",(x,y))
    balik.speed = random.randint(1,6)
    baliklar.append(balik)
for i in range(2):
    x = random.randint(1200, 1400)
    y = random.randint(0,1000)
    balik2=Actor("balik2",(x,y))
    balik2.speed = random.randint(30,45)
    baliklar2.append(balik2)
for i in range(1):
    x = random.randint(1200, 1400)
    y = random.randint(0,1000)
    kopek=Actor("kopek",(x,y))
    kopek.speed = random.randint(5,10)
    kopekler.append(kopek)


def draw():
   
    if mod=="oyun":
        arka.draw()
        fish.draw()
       
        for i in range(len(baliklar)):
            baliklar[i].draw()
            
        for i in range(len(kaplumbagalar)):
            kaplumbagalar[i].draw()
        
        for i in range(len(baliklar2)):
            baliklar2[i].draw()
       
        for i in range(len(kopekler)):
            kopekler[i].draw()
        screen.draw.text(puan, center=(100,100), color="black",fontsize=80)
    elif mod=="menu":
        akvaryum.draw()
        start.draw()     
        screen.draw.text("START TIKLAYIN", center = (450,300), color = "black", fontsize = 70)
    elif mod == "son":
        son.draw()
        screen.draw.text("Kaybettin tekrar dene", center = (400,300), color = "black", fontsize = 70)

def on_mouse_move(pos):
    fish.pos = pos

def yeni_kaplumbaga():
    x = random.randint(1200, 1400)
    y = random.randint(0,600)
    kaplumbaga=Actor("kaplumbaga",(x,y))
    kaplumbaga.speed = random.randint(2, 8)
    kaplumbagalar.append(kaplumbaga)    

def deniz_kaplumbagasi():
    for i in range(len(kaplumbagalar)):
        if kaplumbagalar[i].x > -20:
            kaplumbagalar[i].x = kaplumbagalar[i].x - kaplumbagalar[i].speed
        else:
            kaplumbagalar.pop(i)
            yeni_kaplumbaga()
def yeni_balik():
    x = random.randint(1200, 1400)
    y = random.randint(0,600)
    balik=Actor("balik",(x,y))
    balik.speed = random.randint(2, 6)
    baliklar.append(balik)   
    
def mor_balik():
    for i in range(len(baliklar)):
        if baliklar[i].x>-10:
            baliklar[i].x=baliklar[i].x-baliklar[i].speed
        else:
            baliklar.pop(i)
            yeni_balik()
def yeni_balik2():
    x = random.randint(1200, 1400)
    y = random.randint(0,600)
    balik2=Actor("balik2",(x,y))
    balik2.speed = random.randint(35, 45)
    baliklar2.append(balik2)   
    
def turuncu_balik():
    for i in range(len(baliklar2)):
        if baliklar2[i].x>-10:
            baliklar2[i].x=baliklar2[i].x-baliklar2[i].speed
        else:
            baliklar2.pop(i)
            yeni_balik2()

def yeni_kopek():
    x = random.randint(1200, 1400)
    y = random.randint(0,600)
    kopek=Actor("kopek",(x,y))
    kopek.speed = random.randint(5, 10)
    kopekler.append(kopek)   
def mavi_kopek():
    for i in range(len(kopekler)):
        if kopekler[i].x>-10:
            kopekler[i].x=kopekler[i].x-kopekler[i].speed
        else:
            kopekler.pop(i)
            yeni_kopek()
               
def carpismalar():
    global mod,puan
    for i in range(len(kaplumbagalar)):
        if fish.colliderect(kaplumbagalar[i]):
            mod="son"
    for j in range(len(baliklar)):
        if fish.colliderect(baliklar[j]):
            puan=puan+1
            baliklar.pop(j)
            yeni_balik()
            break
    for j in range(len(baliklar2)):
        if fish.colliderect(baliklar2[j]):
            puan=puan+2
            baliklar2.pop(j)
            yeni_balik2()
    for i in range(len(kopekler)):
        if fish.colliderect(kopekler[i]):
            mod="son"
            break
def update(dt):
    global mod,puan
    if mod =="oyun":
        deniz_kaplumbagasi()
        mor_balik()
        turuncu_balik()
        if puan >= 100:
            mavi_kopek()
        carpismalar()
        if puan >=40 and puan <=99:
            fish.image = "megafish"
        elif puan>=100 and puan<=299:
            fish.image="balık"
        else:
            fish.image = "fish"
        #if fish.x<0:
            #arkaplan.images = ""
        #elif fish.x>800:
            #arkaplan.image = ""
        
def on_mouse_down(button,pos):
    global mod, puan
    if button == mouse.left and mod == "menu":
        if start.collidepoint(pos):
        
            mod='oyun'
           
            
            
            
            

 
