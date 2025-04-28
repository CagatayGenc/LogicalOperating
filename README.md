```python
def alt_alta_topla(sayi1, sayi2):
    sayi1 = sayi1[::-1]
    sayi2 = sayi2[::-1]
    toplam = []
    elde = 0
    for i in range(max(len(sayi1), len(sayi2))):
        rakam1 = int(sayi1[i]) if i < len(sayi1) else 0
        rakam2 = int(sayi2[i]) if i < len(sayi2) else 0
        toplam_rakam = rakam1 + rakam2 + elde
        toplam.append(str(toplam_rakam % 10))
        elde = toplam_rakam // 10
    if elde:
        toplam.append(str(elde))
    return ''.join(toplam[::-1])

def alt_alta_cikar(sayi1, sayi2):
    sayi1 = sayi1[::-1]
    sayi2 = sayi2[::-1]
    fark = []
    odunc = 0
    for i in range(len(sayi1)):
        rakam1 = int(sayi1[i])
        rakam2 = int(sayi2[i]) if i < len(sayi2) else 0
        rakam1 -= odunc
        odunc = 0
        if rakam1 < rakam2:
            rakam1 += 10
            odunc = 1
        fark.append(str(rakam1 - rakam2))
    return ''.join(fark[::-1]).lstrip('0') or '0'

def alt_alta_carp(sayi1, sayi2):
    toplamlar = []
    for i, rakam2 in enumerate(sayi2[::-1]):
        carpim = []
        elde = 0
        for rakam1 in sayi1[::-1]:
            carpim_rakam = int(rakam1) * int(rakam2) + elde
            carpim.append(str(carpim_rakam % 10))
            elde = carpim_rakam // 10
        if elde:
            carpim.append(str(elde))
        carpim = ''.join(carpim[::-1]) + '0' * i
        toplamlar.append(carpim)
    sonuc = '0'
    for num in toplamlar:
        sonuc = alt_alta_topla(sonuc, num)
    return sonuc

def alt_alta_bol(sayi1, sayi2):
    if sayi2 == '0':
        return "Hata: Sıfıra bölme"
    bolum = 0
    kalan = sayi1
    while int(kalan) >= int(sayi2):
        kalan = alt_alta_cikar(kalan, sayi2)
        bolum += 1
    return str(bolum)

print("1: Toplama")
print("2: Çıkarma")
print("3: Çarpma")
print("4: Bölme")
secim = input("İşlem seçin (1/2/3/4): ")

sayi1 = input("Birinci sayı: ")
sayi2 = input("İkinci sayı: ")

if secim == '1':
    sonuc = alt_alta_topla(sayi1, sayi2)
    print(f"{sayi1} + {sayi2} = {sonuc}")
elif secim == '2':
    sonuc = alt_alta_cikar(sayi1, sayi2)
    print(f"{sayi1} - {sayi2} = {sonuc}")
elif secim == '3':
    sonuc = alt_alta_carp(sayi1, sayi2)
    print(f"{sayi1} * {sayi2} = {sonuc}")
elif secim == '4':
    sonuc = alt_alta_bol(sayi1, sayi2)
    print(f"{sayi1} / {sayi2} = {sonuc}")
else:
    print("Geçersiz seçim!")
```
