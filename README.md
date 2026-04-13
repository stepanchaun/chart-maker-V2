
from PIL import Image
 
# Vstup súradníc dvoch bodov
x1 = int(input("Zadaj x1: "))
y1 = int(input("Zadaj y1: "))
x2 = int(input("Zadaj x2: "))
y2 = int(input("Zadaj y2: "))

# Veľkosť obrázka
sirka, vyska = 100, 100
 
# Vytvorenie obrázka
img = Image.new("RGB", (sirka, vyska), color=(255, 255, 255))
pix = img.load()

# Farba čiary
cierna = (0, 0, 0)

# Vypočítanie bodov na čiare pomocou lineárnej interpolácie
def nakresli_ciaru(x1, y1, x2, y2):
    body = []
    
    # Počet krokov
    kroky = max(abs(x2 - x1), abs(y2 - y1)) + 1
    
    for i in range(kroky):
        # Interpolácia
        t = i / kroky if kroky > 0 else 0
        x = int(x1 + (x2 - x1) * t)
        y = int(y1 + (y2 - y1) * t)
        
        # Kontrola hraníc
        if 0 <= x < sirka and 0 <= y < vyska:
            pix[x, y] = cierna
            body.append((x, y))
    
    return body

# Nakreslenie čiary
vypocitane_body = nakresli_ciaru(x1, y1, x2, y2)

print(f"Bod 1: ({x1}, {y1})")
print(f"Bod 2: ({x2}, {y2})")
print(f"Vypočítaných bodov na čiare: {len(vypocitane_body)}")
print(f"Prvých 10 bodov: {vypocitane_body[:10]}")

 # Zobrazenie obrázka
img.show()
