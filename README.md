Python: asosiy tushunchalar va algoritmlar
1. Funksiya

Funksiya bu bir marta yoziladigan va kerak bo'lganda qayta-qayta chaqiriladigan kod bloki.

python
def qosh(a, b):
    return a + b

print(qosh(3, 5))  # 8

# Default qiymat
def salom(ism="Mehmon"):
    print("Salom,", ism)

salom()          # Salom, Mehmon
salom("Ali")     # Salom, Ali

# Bir nechta qiymat qaytarish
def min_max(arr):
    return min(arr), max(arr)

a, b = min_max([4, 1, 9])
print(a, b)  # 1 9

# Lambda (qisqa funksiya)
kvadrat = lambda x: x * x
print(kvadrat(6))  # 36

Rekursiv funksiya o'zini o'zi chaqiradi:

python
def faktorial(n):
    if n <= 1:          # to'xtash sharti
        return 1
    return n * faktorial(n - 1)

print(faktorial(5))  # 120
2. List (ro'yxat)

O'zgartirish mumkin bo'lgan, tartibli to'plam.

python
a = [5, 2, 8, 1]

a.append(10)        # oxiriga qo'shish -> [5,2,8,1,10]
a.insert(1, 99)     # indeksga qo'shish
a.remove(8)         # qiymat bo'yicha o'chirish
x = a.pop()         # oxirgisini olib o'chiradi
a.sort()            # o'sish tartibida
a.sort(reverse=True)  # kamayish tartibida
a.reverse()

print(len(a))       # uzunlik
print(a[0], a[-1])  # birinchi va oxirgi
print(a[1:3])       # slice
print(3 in a)       # borligini tekshirish

# List comprehension
kvadratlar = [i * i for i in range(1, 6)]   # [1,4,9,16,25]
juft = [i for i in range(20) if i % 2 == 0]

# Sikl bilan o'tish
for i in range(len(a)):
    print(i, a[i])
for qiymat in a:
    print(qiymat)
for i, q in enumerate(a):
    print(i, q)

2D list (matritsa):

python
n, m = 3, 4
mat = [[0] * m for _ in range(n)]   # to'g'ri usul
mat[1][2] = 7
# XATO: [[0]*m]*n  -> barcha qatorlar bitta obyekt bo'lib qoladi
3. Massiv (array)

Pythonda "massiv" odatda list bilan ishlatiladi. Qo'shimcha ikki variant bor:

python
# 1) array moduli: faqat bir xil turdagi sonlar (xotirani tejaydi)
from array import array
arr = array('i', [1, 2, 3])   # 'i' = int
arr.append(4)

# 2) NumPy: tez hisoblash va ilmiy ishlar uchun (pip install numpy)
import numpy as np
b = np.array([1, 2, 3, 4])
print(b * 2)       # [2 4 6 8]
print(b.sum(), b.mean())

Olimpiada va oddiy masalalarda list yetarli.

4. Dictionary (lug'at)

Kalit → qiymat juftliklari. Qidirish juda tez (O(1)).

python
d = {"ali": 20, "vali": 25}

d["sami"] = 30          # qo'shish
d["ali"] = 21           # o'zgartirish
del d["vali"]           # o'chirish

print(d["ali"])
print(d.get("yo'q", 0))   # kalit bo'lmasa 0 qaytaradi (xato bermaydi)
print("ali" in d)         # kalit borligini tekshirish

for k, v in d.items():
    print(k, v)
for k in d.keys(): ...
for v in d.values(): ...

Sanash (juda ko'p ishlatiladi):

python
s = "abracadabra"
sanoq = {}
for h in s:
    sanoq[h] = sanoq.get(h, 0) + 1
print(sanoq)  # {'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1}

# Qisqa usul
from collections import Counter
print(Counter(s))

# Kalit yo'q bo'lsa avtomatik 0 yoki [] yaratadi
from collections import defaultdict
g = defaultdict(list)
g[1].append(2)   # graf uchun qulay
5. Set (to'plam)

Takrorlanmas, tartibsiz elementlar. Qidirish tez (O(1)).

python
s = {1, 2, 3, 3, 2}
print(s)            # {1, 2, 3}

s.add(10)
s.remove(2)         # yo'q bo'lsa xato beradi
s.discard(99)       # yo'q bo'lsa xato bermaydi

a = {1, 2, 3, 4}
b = {3, 4, 5}
print(a | b)   # birlashma  {1,2,3,4,5}
print(a & b)   # kesishma   {3,4}
print(a - b)   # ayirma     {1,2}
print(a ^ b)   # simmetrik ayirma {1,2,5}

# Takrorlarni olib tashlash
royxat = [1, 2, 2, 3, 3, 3]
unik = list(set(royxat))
6. Tuple va String
python
t = (1, 2, 3)      # o'zgarmas ro'yxat
x, y, z = t        # ochish (unpacking)

s = "Salom Dunyo"
print(s.upper(), s.lower())
print(s.split())            # ['Salom', 'Dunyo']
print(s[::-1])              # teskari
print(" ".join(["a", "b"])) # "a b"
7. Prefix sum (prefiks yig'indi)

G'oya: pref[i] = massivning dastlabki i ta elementi yig'indisi. Shundan keyin [l, r] oraliq yig'indisi O(1) da topiladi. Oddiy usulda har so'rov O(n) bo'lardi.

python
a = [3, 1, 4, 1, 5, 9, 2]
n = len(a)

pref = [0] * (n + 1)
for i in range(n):
    pref[i + 1] = pref[i] + a[i]
# pref = [0, 3, 4, 8, 9, 14, 23, 25]

def yigindi(l, r):          # l dan r gacha (0-indeks, ikkalasi ham kiradi)
    return pref[r + 1] - pref[l]

print(yigindi(2, 4))   # 4+1+5 = 10
print(yigindi(0, 6))   # 25

Tayyor funksiya bilan:

python
from itertools import accumulate
pref = [0] + list(accumulate(a))

2D prefix sum (matritsa uchun):

python
mat = [[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]]
n, m = len(mat), len(mat[0])
P = [[0] * (m + 1) for _ in range(n + 1)]
for i in range(n):
    for j in range(m):
        P[i+1][j+1] = mat[i][j] + P[i][j+1] + P[i+1][j] - P[i][j]

def kv_yigindi(r1, c1, r2, c2):
    return P[r2+1][c2+1] - P[r1][c2+1] - P[r2+1][c1] + P[r1][c1]

print(kv_yigindi(1, 1, 2, 2))  # 5+6+8+9 = 28
8. Eratosfen g'alviri (Sieve of Eratosthenes)

G'oya: 1 dan n gacha barcha tub sonlarni topish. Tub sonning karralilarini ketma-ket o'chirib boramiz. Murakkabligi O(n log log n).

python
def galvir(n):
    tub = [True] * (n + 1)
    tub[0] = tub[1] = False
    i = 2
    while i * i <= n:
        if tub[i]:
            for j in range(i * i, n + 1, i):   # i*i dan boshlaymiz
                tub[j] = False
        i += 1
    return [i for i in range(2, n + 1) if tub[i]]

print(galvir(30))
# [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]

Ishlatilishi: tub[x] orqali istalgan sonning tub yoki tub emasligini O(1) da bilish mumkin. Bu ko'p so'rovli masalalarda juda foydali.

9. Binary search (ikkilik qidiruv)

Shart: massiv saralangan bo'lishi kerak. Har qadamda qidiruv oralig'i yarmiga qisqaradi, murakkabligi O(log n).

python
def binary_search(a, x):
    l, r = 0, len(a) - 1
    while l <= r:
        m = (l + r) // 2
        if a[m] == x:
            return m          # topildi
        elif a[m] < x:
            l = m + 1
        else:
            r = m - 1
    return -1                 # topilmadi

a = [1, 3, 5, 7, 9, 11]
print(binary_search(a, 7))    # 3
print(binary_search(a, 4))    # -1

Tayyor modul bisect:

python
from bisect import bisect_left, bisect_right

a = [1, 2, 2, 2, 5, 8]
print(bisect_left(a, 2))    # 1  (2 ning birinchi o'rni)
print(bisect_right(a, 2))   # 4  (2 dan keyingi o'rin)
print(bisect_right(a, 2) - bisect_left(a, 2))  # 2 soni nechta: 3

Javob ustida binary search (olimpiadalarda ko'p uchraydi):

python
# Masala: x*x >= 50 bo'ladigan eng kichik butun x
l, r = 0, 10**9
while l < r:
    m = (l + r) // 2
    if m * m >= 50:
        r = m
    else:
        l = m + 1
print(l)  # 8
10. DP (Dynamic Programming, dinamik dasturlash)

G'oya: Katta masalani kichik qismlarga bo'lib, har bir qism javobini bir marta hisoblab saqlash (takroriy hisoblashni oldini olish).

a) Fibonachchi
python
# Oddiy rekursiya: sekin, O(2^n)
def fib_sekin(n):
    return n if n < 2 else fib_sekin(n-1) + fib_sekin(n-2)

# Memoizatsiya (yuqoridan pastga)
from functools import lru_cache
@lru_cache(maxsize=None)
def fib(n):
    return n if n < 2 else fib(n-1) + fib(n-2)

# Tabulyatsiya (pastdan yuqoriga), O(n)
def fib_dp(n):
    dp = [0] * (n + 2)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

print(fib_dp(50))  # 12586269025
b) Pul almashtirish (eng kam tanga)
python
def kam_tanga(tangalar, summa):
    INF = float('inf')
    dp = [0] + [INF] * summa
    for s in range(1, summa + 1):
        for t in tangalar:
            if s >= t:
                dp[s] = min(dp[s], dp[s - t] + 1)
    return dp[summa] if dp[summa] != INF else -1

print(kam_tanga([1, 5, 6], 11))  # 2  (5+6)
c) Ryukzak masalasi (0/1 knapsack)
python
def ryukzak(og, qiy, sigim):
    dp = [0] * (sigim + 1)
    for i in range(len(og)):
        for w in range(sigim, og[i] - 1, -1):   # teskari yo'nalish muhim
            dp[w] = max(dp[w], dp[w - og[i]] + qiy[i])
    return dp[sigim]

print(ryukzak([1, 3, 4, 5], [1, 4, 5, 7], 7))  # 9
d) Eng uzun o'suvchi ketma-ketlik (LIS)
python
from bisect import bisect_left

def lis(a):
    t = []
    for x in a:
        i = bisect_left(t, x)
        if i == len(t):
            t.append(x)
        else:
            t[i] = x
    return len(t)

print(lis([10, 9, 2, 5, 3, 7, 101, 18]))  # 4
e) Eng katta qism yig'indi (Kadane)
python
def kadane(a):
    joriy = eng = a[0]
    for x in a[1:]:
        joriy = max(x, joriy + x)
        eng = max(eng, joriy)
    return eng

print(kadane([-2, 1, -3, 4, -1, 2, 1, -5, 4]))  # 6

DP yechish tartibi:

dp[i] nimani anglatishini aniqlang.
Boshlang'ich qiymatlarni yozing.
Formulani (qayta bog'lanish) toping.
Javob qaysi katakda ekanini aniqlang.
11. Boshqa muhim narsalar
Kirish/chiqish
python
n = int(input())
a = list(map(int, input().split()))   # "1 2 3" -> [1,2,3]
x, y = map(int, input().split())

# Tezkor kiritish (katta ma'lumotlar uchun)
import sys
input = sys.stdin.readline

print(*a)              # ro'yxatni bo'sh joy bilan chiqaradi
print(f"Javob: {n}")   # f-string
Shartlar va sikllar
python
if x > 0:
    print("musbat")
elif x == 0:
    print("nol")
else:
    print("manfiy")

for i in range(5): ...          # 0..4
for i in range(1, 10, 2): ...   # 1,3,5,7,9
while n > 0:
    n //= 2
# break - siklni to'xtatadi, continue - keyingi qadamga o'tadi
Saralash
python
a = [5, 2, 8]
a.sort()                              # joyida
b = sorted(a, reverse=True)           # yangi list
juftlar = [("ali", 20), ("vali", 18)]
juftlar.sort(key=lambda p: p[1])      # ikkinchi element bo'yicha
Ikki ko'rsatkich (two pointers)
python
# Saralangan massivda yig'indisi target bo'lgan juftlik
def juftlik(a, target):
    l, r = 0, len(a) - 1
    while l < r:
        s = a[l] + a[r]
        if s == target:
            return l, r
        elif s < target:
            l += 1
        else:
            r -= 1
    return None
collections va heapq
python
from collections import deque, Counter
q = deque([1, 2, 3])
q.append(4)
q.popleft()       # navbat (BFS uchun)

import heapq
h = []
heapq.heappush(h, 5)
heapq.heappush(h, 1)
print(heapq.heappop(h))   # 1 (eng kichigi)
Matematika
python
import math
print(math.gcd(12, 18))    # 6 (EKUB)
print(math.sqrt(49))       # 7.0
print(math.isqrt(50))      # 7 (butun ildiz)
print(pow(2, 10, 1000))    # 2^10 mod 1000 = 24
print(10 // 3, 10 % 3)     # 3 1
Fayl bilan ishlash va xatolar
python
try:
    with open("data.txt") as f:
        matn = f.read()
except FileNotFoundError:
    print("Fayl topilmadi")
Sinf (class)
python
class Talaba:
    def __init__(self, ism, yosh):
        self.ism = ism
        self.yosh = yosh

    def salom(self):
        print(f"Men {self.ism}, {self.yosh} yoshdaman")

t = Talaba("Ali", 20)
t.salom()
12. Hammasini bitta dasturda birlashtirish

Masala: massiv berilgan, ko'p so'rov keladi. Har so'rovda [l, r] oraliqdagi tub sonlarning yig'indisi so'ralsin.

python
import sys
input = sys.stdin.readline

def galvir(n):
    tub = [True] * (n + 1)
    tub[0] = tub[1] = False
    for i in range(2, int(n**0.5) + 1):
        if tub[i]:
            for j in range(i*i, n + 1, i):
                tub[j] = False
    return tub

def main():
    n = int(input())
    a = list(map(int, input().split()))
    q = int(input())

    tub = galvir(max(a))

    # tub sonlar uchun prefix sum
    pref = [0] * (n + 1)
    for i in range(n):
        pref[i + 1] = pref[i] + (a[i] if tub[a[i]] else 0)

    for _ in range(q):
        l, r = map(int, input().split())      # 1-indeksli
        print(pref[r] - pref[l - 1])

main()

Kirish:

5
2 4 7 9 11
2
1 3
2 5

Chiqish:

9
18
Qaysi masalada nimani ishlatish
Vaziyat	Vosita
Oraliq yig'indisi ko'p so'raladi	Prefix sum
Tub sonlar, bo'luvchilar	Eratosfen g'alviri
Saralangan massivda qidirish	Binary search / bisect
Qismlarga bo'linadigan, takrorlanuvchi masala	DP
Tez qidirish, sanash	dict, set, Counter
Takrorlarni olib tashlash	set
Navbat / BFS	deque
Eng kichik/katta elementni tez olish	heapq

Istasangiz, istalgan mavzuni (masalan DP ning yanada murakkab turlari, graf algoritmlari yoki OOP) alohida, ko'proq mashq va masalalar bilan chuqurroq tushuntirib beraman.

tushuncha sal kam yanayam aniqroq tushuntirib ber

Chuqurroq tushuntirish

Har mavzuni "nima o'zi", "nega ishlaydi" va "qadamma-qadam ishlashi" tartibida yozdim.

1. Funksiya

Funksiya kirish (parametr) qabul qiladi, ish bajaradi va natija qaytaradi. U matematikadagi f(x) ga o'xshaydi.

python
def kvadrat(x):        # x - parametr
    return x * x       # return - natijani qaytaradi

y = kvadrat(5)         # 5 - argument
print(y)               # 25

return va print farqi (boshlovchilar ko'p adashadi):

python
def a(x):
    print(x * 2)       # faqat ekranga chiqaradi, qiymat qaytarmaydi

def b(x):
    return x * 2       # qiymatni qaytaradi, uni saqlash mumkin

p = a(3)   # ekranda 6 chiqadi, lekin p = None
q = b(3)   # q = 6

O'zgaruvchi ko'rinish doirasi (scope):

python
def f():
    t = 10             # lokal: faqat f ichida mavjud
    print(t)

f()
# print(t)  -> XATO, t funksiya tashqarisida yo'q

List funksiyaga "o'zi" beriladi, nusxasi emas:

python
def qosh(arr):
    arr.append(100)    # asl listni o'zgartiradi

x = [1, 2]
qosh(x)
print(x)               # [1, 2, 100]

Rekursiya qanday ishlaydi, faktorial(3) misolida:

faktorial(3) = 3 * faktorial(2)
                   faktorial(2) = 2 * faktorial(1)
                                      faktorial(1) = 1   <- to'xtash sharti

Keyin natija orqaga qaytadi: 1 → 2*1=2 → 3*2=6. To'xtash sharti bo'lmasa, funksiya cheksiz chaqiriladi va xato beradi.

2. List, Dictionary, Set: qaysi biri nega kerak

Asosiy farq qidirish tezligida:

	List	Dict	Set
Tartib bor	ha (indeks bilan)	ha (qo'shilish tartibida)	yo'q
Takror	mumkin	kalit takrorlanmaydi	takrorlanmaydi
x in ... tezligi	O(n), hammasini ko'radi	O(1)	O(1)

Nega dict va set tez? Ular ichida hash ishlatiladi. Kalit sonli "manzil"ga aylantiriladi va element shu manzildan to'g'ridan-to'g'ri olinadi. List esa boshidan oxirigacha birma-bir tekshiradi.

python
import time

n = 10**5
royxat = list(range(n))
tolam = set(range(n))

# 1000 marta "n-1 bormi?" deb so'raymiz
t = time.time()
for _ in range(1000):
    (n - 1) in royxat
print("list:", time.time() - t)    # sekin

t = time.time()
for _ in range(1000):
    (n - 1) in tolam
print("set:", time.time() - t)     # deyarli bir zumda

Qoida: "Bu element avval uchraganmi?" deb ko'p so'rasangiz, set yoki dict ishlating.

Misol: massivda yig'indisi target bo'lgan ikki son bormi? (Two Sum)

python
def ikki_son(a, target):
    korilgan = set()
    for x in a:
        kerak = target - x          # x ga juft bo'ladigan son
        if kerak in korilgan:       # O(1)
            return True
        korilgan.add(x)
    return False

print(ikki_son([2, 7, 11, 15], 9))   # True (2+7)

List bilan bu masala ikki sikl, ya'ni O(n²) bo'lardi. Set bilan O(n).

List nusxalash tuzog'i:

python
a = [1, 2, 3]
b = a            # b - alohida list emas, xuddi shu list
b.append(4)
print(a)         # [1, 2, 3, 4], a ham o'zgardi!

c = a.copy()     # haqiqiy nusxa (yoki a[:])
c.append(5)
print(a)         # o'zgarmadi

Dict kaliti faqat o'zgarmas tur bo'ladi: son, string, tuple mumkin. List mumkin emas.

3. Prefix sum
Muammo

Massiv a va 100 000 ta so'rov bor, har birida [l, r] oraliq yig'indisi kerak.

Oddiy usul: sum(a[l:r+1]). Bu har so'rovda O(n), jami 100 000 × 100 000 = 10¹⁰ amal. Juda sekin.

G'oya

Avval bir marta "to'plangan yig'indilar"ni hisoblab qo'yamiz. Keyin har so'rov bitta ayirish.

pref[i] = massivning dastlabki i ta elementi yig'indisi.

a    = [3, 1, 4, 1, 5, 9, 2]
indeks: 0  1  2  3  4  5  6

pref[0] = 0                   (hech narsa yo'q)
pref[1] = 3                   (a[0])
pref[2] = 3+1 = 4             (a[0..1])
pref[3] = 4+4 = 8             (a[0..2])
pref[4] = 8+1 = 9
pref[5] = 9+5 = 14
pref[6] = 14+9 = 23
pref[7] = 23+2 = 25

Formula: pref[i+1] = pref[i] + a[i]

Nega ayirish ishlaydi?

a[2..4] yig'indisi kerak (ya'ni 4+1+5):

pref[5] = a[0]+a[1]+a[2]+a[3]+a[4]     = 14
pref[2] = a[0]+a[1]                    = 4
                  ayirma = a[2]+a[3]+a[4] = 10  ✓

Umumiy formula: yig'indi(l, r) = pref[r+1] - pref[l]

pref[0] = 0 nega kerak? l = 0 bo'lganda pref[0] ni ayirish kerak bo'ladi va uning 0 bo'lishi yig'indiga ta'sir qilmaydi.

python
a = [3, 1, 4, 1, 5, 9, 2]
pref = [0] * (len(a) + 1)
for i in range(len(a)):
    pref[i + 1] = pref[i] + a[i]

def yigindi(l, r):
    return pref[r + 1] - pref[l]

print(yigindi(2, 4))   # 10

Murakkablik: tayyorlash O(n), har so'rov O(1).

2D prefix sum

P[i][j] = chap-yuqori burchakdan (i-1, j-1) katakkacha to'g'ri to'rtburchak yig'indisi.

Hisoblash qo'shish-ayirish (inclusion-exclusion) bilan: yuqoridagini va chapdagini qo'shamiz. Ikkalasi ham ichki qismni hisoblagani uchun, ichkaridagini bir marta ayiramiz.

P[i+1][j+1] = mat[i][j] + P[i][j+1] + P[i+1][j] - P[i][j]

So'rovda ham xuddi shunday. Kerakli to'rtburchakdan tashqaridagi ikki "chiziq"ni ayiramiz, ikki marta ayrilgan burchakni bir marta qaytarib qo'shamiz.

4. Eratosfen g'alviri
Muammo

1 dan n gacha hamma tub sonlarni topish. Har sonni alohida tekshirish sekin.

G'oya

Tub son kattaroq sonlarning "bo'luvchisi" bo'la oladi. Demak, tub sonni topgach, uning karralilarini (2p, 3p, 4p, ...) tub emas deb belgilaymiz.

n = 30 uchun jarayon:

Boshida: 2 dan 30 gacha hammasi "tub" deb belgilangan.

i=2: tub. Karralilarini o'chiramiz: 4,6,8,10,12,...,30
i=3: tub. Karralilarini o'chiramiz: 9,12,15,18,21,24,27,30
i=4: allaqachon o'chirilgan, o'tkazib yuboramiz
i=5: tub. O'chiramiz: 25,30
i=6: 6*6=36 > 30, to'xtaymiz.

Qolganlari: 2,3,5,7,11,13,17,19,23,29
Ikkita muhim optimizatsiya

1) Nega i*i dan boshlaymiz?
i ning i*k ko'rinishidagi karralisida k < i bo'lsa, u son k ning bo'luvchilari orqali allaqachon o'chirilgan bo'ladi. Masalan i=5 uchun 5*2=10 ni 2 o'chirgan, 5*3=15 ni 3 o'chirgan. Yangi narsa 25 dan boshlanadi.

2) Nega i*i <= n gacha yuramiz?
Murakkab sonning albatta √n dan kichik yoki teng bo'luvchisi bo'ladi. Masalan 30 ning bo'luvchisi 2 (√30 ≈ 5.4 dan kichik). Shuning uchun √n gacha tublarning karralilarini o'chirish yetarli.

python
def galvir(n):
    tub = [True] * (n + 1)      # tub[i] = i tub sonmi?
    tub[0] = tub[1] = False     # 0 va 1 tub emas
    i = 2
    while i * i <= n:
        if tub[i]:
            for j in range(i * i, n + 1, i):
                tub[j] = False
        i += 1
    return tub                  # ro'yxat emas, tekshirish massivi

tub = galvir(100)
print(tub[97])    # True
print(tub[91])    # False (91 = 7*13)

tublar = [i for i in range(len(tub)) if tub[i]]

Qachon ishlatiladi: n ≤ 10⁷ gacha va "bu son tubmi?" degan ko'p so'rov bo'lsa. Bitta katta sonni tekshirish uchun esa √x gacha bo'luvchi qidirish yetadi.

5. Binary search
G'oya

Massiv saralangan. Telefon kitobida ism qidirgandek: o'rtasini ochamiz va kerakli qism qaysi yarmida ekanini bilamiz, qolgan yarmini tashlab yuboramiz. Har qadamda ish ikki baravar kamayadi.

1 000 000 element uchun ko'pi bilan ~20 qadam. Oddiy qidiruvda 1 000 000 qadam bo'lardi.

Qadamma-qadam, a = [1, 3, 5, 7, 9, 11], x = 9
l=0, r=5 → m=2, a[2]=5  < 9 → javob o'ngda → l = m+1 = 3
l=3, r=5 → m=4, a[4]=9  == 9 → topildi, indeks 4

x = 4 (yo'q element) bo'lsa:

l=0, r=5 → m=2, a[2]=5 > 4 → r = m-1 = 1
l=0, r=1 → m=0, a[0]=1 < 4 → l = m+1 = 1
l=1, r=1 → m=1, a[1]=3 < 4 → l = m+1 = 2
l=2, r=1 → l > r, oraliq bo'sh → topilmadi
python
def binary_search(a, x):
    l, r = 0, len(a) - 1
    while l <= r:               # oraliqda hech bo'lmasa 1 element bor
        m = (l + r) // 2
        if a[m] == x:
            return m
        elif a[m] < x:
            l = m + 1           # m allaqachon tekshirilgan, shuning uchun +1
        else:
            r = m - 1           # shuning uchun -1
    return -1

Eng ko'p uchraydigan xatolar:

l = m yoki r = m yozish → ba'zan cheksiz sikl bo'ladi.
while l < r va while l <= r ni adashtirish. Shablonni bir xil saqlang.
Massiv saralanmagan holda ishlatish.
Javob ustida binary search (eng kuchli qo'llanish)

Massiv shart emas. Muhimi, savolga javob "yo'q, yo'q, yo'q, ha, ha, ha" ko'rinishida monoton bo'lsin.

Misol: "x² ≥ 50 bo'ladigan eng kichik butun x?"

x:       0   1   2   3   4   5   6   7   8   9 ...
x²>=50:  F   F   F   F   F   F   F   F   T   T ...
                                         ↑ shu kerak
python
l, r = 0, 10**9          # javob shu oraliqda
while l < r:
    m = (l + r) // 2
    if m * m >= 50:      # shart bajarilyapti → javob m yoki chaproqda
        r = m
    else:                # bajarilmayapti → javob m dan o'ngda
        l = m + 1
print(l)                 # 8

Bu shablonni yodlab oling: "shart bajarilsa r = m, bajarilmasa l = m + 1". Olimpiadada "eng kichik / eng katta ... topish" masalalari ko'pincha shu bilan yechiladi.

6. DP (dinamik dasturlash)
Asosiy fikr

DP ikkita xususiyat bo'lganda ishlaydi:

Kichik masalalar takrorlanadi (bir xil narsani qayta-qayta hisoblaymiz).
Katta masala javobi kichik masalalar javobidan tuziladi.
Fibonachchi misolida nega kerak

fib(5) oddiy rekursiyada:

                fib(5)
              /        \
          fib(4)        fib(3)
         /     \        /    \
     fib(3)  fib(2)  fib(2) fib(1)
     /   \
 fib(2) fib(1)

fib(3) ikki marta, fib(2) uch marta hisoblandi. n kattalashganda bu portlaydi (O(2ⁿ)). DP: har qiymatni bir marta hisoblab saqlaymiz.

DP yechish usuli (4 qadam)
Holat: dp[i] nimani bildiradi? (Eng muhim qadam.)
Boshlang'ich qiymat: eng kichik holat javobi.
O'tish (formula): dp[i] ni oldingilardan qanday hosil qilamiz?
Javob: qaysi katakda.
Misol 1: Pul almashtirish

Masala: tangalar [1, 5, 6], summa 11. Eng kam nechta tanga kerak?

Nega oddiy "eng kattasidan boshlash" (greedy) ishlamaydi? Tangalar [1, 3, 4], summa 6: greedy 4+1+1 = 3 ta tanga beradi, lekin to'g'ri javob 3+3 = 2 ta.

DP:

dp[s] = s so'mni yig'ish uchun eng kam tanga soni.
dp[0] = 0.
dp[s] = min(dp[s - t] + 1) har tanga t uchun. Ya'ni oxirgi tanga t bo'lsa, qolgan s - t ni eng kam tanga bilan yig'ib, 1 ni qo'shamiz.
Javob dp[summa].

Jadval to'ldirilishi (tangalar 1, 5, 6):

s:     0  1  2  3  4  5  6  7  8  9  10 11
dp[s]: 0  1  2  3  4  1  1  2  3  4  2  2

Masalan dp[11]: 1 tanga tashlasak dp[10]+1 = 3; 5 tanga tashlasak dp[6]+1 = 2; 6 tanga tashlasak dp[5]+1 = 2. Eng kichigi 2.

python
def kam_tanga(tangalar, summa):
    INF = float('inf')            # "yetib bo'lmaydi" belgisi
    dp = [INF] * (summa + 1)
    dp[0] = 0
    for s in range(1, summa + 1):
        for t in tangalar:
            if s >= t:
                dp[s] = min(dp[s], dp[s - t] + 1)
    return dp[summa] if dp[summa] != INF else -1
Misol 2: Ryukzak (0/1 knapsack)

Narsalar bor, har birining og'irligi va qiymati bor. Ryukzak sig'imi cheklangan. Har narsani bir marta olish mumkin. Maksimal qiymat?

dp[w] = sig'imi w bo'lganda olish mumkin bo'lgan maksimal qiymat.

Har narsa uchun: "olmayman" (dp[w] o'zgarmaydi) yoki "olaman" (dp[w - og'irlik] + qiymat), kattasini tanlaymiz.

Nega sikl teskari (sigim dan pastga)?
Misol: bitta narsa, og'irligi 2, qiymati 3, sig'im 4.

To'g'ri yo'nalishda (w = 2, 3, 4): dp[2] = 3, keyin dp[4] = dp[2] + 3 = 6. Narsa ikki marta olingan bo'ldi. Bu noto'g'ri.
Teskari yo'nalishda (w = 4, 3, 2): dp[4] = dp[2] + 3 = 0 + 3 = 3 (dp[2] hali yangilanmagan), keyin dp[2] = 3. To'g'ri.
python
def ryukzak(og, qiy, sigim):
    dp = [0] * (sigim + 1)
    for i in range(len(og)):                      # har narsa uchun
        for w in range(sigim, og[i] - 1, -1):     # TESKARI
            dp[w] = max(dp[w], dp[w - og[i]] + qiy[i])
    return dp[sigim]
Misol 3: Kadane, eng katta qism yig'indi

Uzluksiz qism massivning eng katta yig'indisi. [-2, 1, -3, 4, -1, 2, 1, -5, 4] → javob 6 (4, -1, 2, 1).

joriy = aynan shu elementda tugaydigan eng yaxshi yig'indi. Har elementda ikki tanlov bor: oldingi qismni davom ettirish (joriy + x) yoki yangidan boshlash (x). Oldingi yig'indi manfiy bo'lsa, u bizga zarar, shuning uchun yangidan boshlaymiz.

x:      -2  1  -3  4  -1  2  1  -5  4
joriy:  -2  1  -2  4   3  5  6   1  5
eng:    -2  1   1  4   4  5  6   6  6   → javob 6
python
def kadane(a):
    joriy = eng = a[0]
    for x in a[1:]:
        joriy = max(x, joriy + x)
        eng = max(eng, joriy)
    return eng
Misol 4: LIS (eng uzun o'suvchi qism ketma-ketlik)

Oddiy O(n²) variant (tushunish uchun):

dp[i] = a[i] bilan tugaydigan eng uzun o'suvchi ketma-ketlik uzunligi. Har i uchun undan oldingi j larni ko'ramiz. a[j] < a[i] bo'lsa, dp[i] = max(dp[i], dp[j] + 1).

python
def lis(a):
    n = len(a)
    dp = [1] * n               # har element o'zi bilan 1 uzunlik
    for i in range(n):
        for j in range(i):
            if a[j] < a[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)

print(lis([10, 9, 2, 5, 3, 7, 101, 18]))   # 4  (2,3,7,101)

n katta bo'lsa (10⁵), oldingi javobdagi bisect li O(n log n) variantdan foydalaning.
Kodni tezlashtirish va DP ni oddiy kodga qo'shish
1. Avval: kod qancha vaqt ishlaydi?

Python taxminan 1 sekundda 10⁷ ta oddiy amal bajaradi. Masala cheklovlariga qarab oldindan baholash mumkin:

n	Ruxsat etilgan murakkablik
n ≤ 10	O(n!)
n ≤ 20	O(2ⁿ)
n ≤ 1 000	O(n²)
n ≤ 10⁵	O(n log n)
n ≤ 10⁶ – 10⁷	O(n)
n ≤ 10¹⁸	O(log n)

Ichma-ich ikki sikl va n = 10⁵ bo'lsa, bu 10¹⁰ amal, ya'ni sekin. Shu paytda kodni o'zgartirish kerak.

Vaqtni o'lchash:

python
import time

t = time.perf_counter()
# ... tekshirilayotgan kod ...
print("Vaqt:", time.perf_counter() - t)
2. "Sekin kod → tez kod" almashtirish retseptlari

Har retsept: sekin kod, tez kod va nima o'zgargani.

Retsept 1: takroriy yig'indi → Prefix sum
python
# SEKIN: har so'rovda butun oraliqni qayta sanaydi. O(n * q)
for l, r in sorovlar:
    print(sum(a[l:r+1]))
python
# TEZ: bir marta tayyorlaymiz, har so'rov O(1). Jami O(n + q)
pref = [0] * (len(a) + 1)
for i in range(len(a)):
    pref[i + 1] = pref[i] + a[i]

for l, r in sorovlar:
    print(pref[r + 1] - pref[l])

Qachon almashtiriladi: bitta massiv ustida oraliq so'rovlari ko'p bo'lsa.

Retsept 2: list ichida qidirish → set / dict
python
# SEKIN: "x in list" har safar boshidan oxirigacha ko'radi. O(n * q)
ruxsat = [3, 8, 12, 45, 99]       # katta ro'yxat deb tasavvur qiling
for x in sorovlar:
    if x in ruxsat:
        print("bor")
python
# TEZ: set da qidirish O(1)
ruxsat = set([3, 8, 12, 45, 99])
for x in sorovlar:
    if x in ruxsat:
        print("bor")

Ikki sikl bilan "juftlik topish" masalasi ham shunday tezlashadi. Ichki siklni set/dict qidiruviga almashtiring (oldingi javobdagi Two Sum).

Retsept 3: chiziqli qidiruv → Binary search
python
# SEKIN: saralangan massivda boshidan qidirish. O(n) har so'rov
def bor_mi(a, x):
    for v in a:
        if v == x:
            return True
    return False
python
# TEZ: O(log n)
from bisect import bisect_left

def bor_mi(a, x):
    i = bisect_left(a, x)
    return i < len(a) and a[i] == x

Shart: massiv saralangan bo'lishi kerak. Saralash bir marta O(n log n) turadi, keyin har qidiruv tez.

Retsept 4: tub sonni qayta-qayta tekshirish → Eratosfen
python
# SEKIN: har son uchun alohida tekshirish. O(sqrt(x)) har son
def tubmi(x):
    if x < 2: return False
    i = 2
    while i * i <= x:
        if x % i == 0: return False
        i += 1
    return True

for x in sonlar:            # 10^5 ta son, har biri 10^6 gacha
    print(tubmi(x))
python
# TEZ: bir marta g'alvir, keyin har javob O(1)
M = 10**6
tub = [True] * (M + 1)
tub[0] = tub[1] = False
for i in range(2, int(M**0.5) + 1):
    if tub[i]:
        for j in range(i*i, M + 1, i):
            tub[j] = False

for x in sonlar:
    print(tub[x])
Retsept 5: rekursiya → Memoizatsiya (DP)
python
# SEKIN: bir xil holat qayta-qayta hisoblanadi. O(2^n)
def f(n):
    if n < 2: return n
    return f(n-1) + f(n-2)
python
# TEZ: bitta qator qo'shish kifoya. O(n)
from functools import lru_cache

@lru_cache(maxsize=None)
def f(n):
    if n < 2: return n
    return f(n-1) + f(n-2)
Retsept 6: kirish/chiqish va string
python
# SEKIN
n = int(input())
for _ in range(n):
    x = int(input())          # input() sekin
    print(x * 2)              # har print alohida chiqadi
python
# TEZ
import sys
input = sys.stdin.readline

n = int(input())
natija = []
for _ in range(n):
    x = int(input())
    natija.append(x * 2)
print("\n".join(map(str, natija)))   # bir yo'la chiqarish

Stringlarni s += "..." bilan sikl ichida qo'shish ham sekin. Ro'yxatga yig'ib, oxirida "".join(...) qiling.

Retsept 7: Python'ga xos kichik tezlatmalar
python
# SEKIN                         # TEZ
for i in range(n):              # list comprehension
    r.append(i * i)             r = [i * i for i in range(n)]

yig = 0                         # tayyor funksiya (C tilida yozilgan)
for v in a: yig += v            yig = sum(a)

if len(a) == 0:                 if not a:

a.pop(0)  # O(n)!              deque.popleft()  # O(1)
a.insert(0, x)  # O(n)!
3. DP ni kodga qanday qo'shiladi

DP bu yangi til konstruksiyasi emas. Bu fikrlash usuli. Jarayon 4 bosqichda bo'ladi, har bosqichda kod oldingisidan oz farq qiladi.

Misol masala

Jadval n × m. . bo'sh katak, # to'siq. Chap-yuqoridan o'ng-pastga faqat o'ngga yoki pastga yurish mumkin. Nechta turli yo'l bor?

. . .
. # .
. . .

Javob: 2.

1-bosqich: Oddiy rekursiya (to'g'ri, lekin sekin)

Avval masalani oddiy rekursiya bilan yozing. "(i, j) katakdan oxirgi katakka nechta yo'l bor?"

python
def yol(i, j):
    if i >= n or j >= m or g[i][j] == '#':
        return 0                      # chegaradan chiqdi yoki to'siq
    if i == n - 1 and j == m - 1:
        return 1                      # manzilga yetdik
    return yol(i + 1, j) + yol(i, j + 1)   # pastga + o'ngga

Muammo: (2,2) katagiga turli yo'llar bilan kelinadi va har safar uning davomi qaytadan hisoblanadi. n = m = 20 da ham ancha sekin.

2-bosqich: Memoizatsiya (1 qator qo'shamiz)
python
import sys
from functools import lru_cache
sys.setrecursionlimit(10**6)          # chuqur rekursiya uchun

@lru_cache(maxsize=None)              # <- shu qatorning o'zi DP ga aylantirdi
def yol(i, j):
    if i >= n or j >= m or g[i][j] == '#':
        return 0
    if i == n - 1 and j == m - 1:
        return 1
    return yol(i + 1, j) + yol(i, j + 1)

print(yol(0, 0))

lru_cache har (i, j) uchun javobni eslab qoladi. Bir xil holat ikkinchi marta so'ralsa, hisoblamasdan tayyor javob beradi. Jami holatlar n * m ta, demak O(n·m).

Dastur ichiga ulanishi: n, g ni funksiyadan tashqarida o'qib, keyin yol(0, 0) ni chaqirasiz. Hammasi shu.

3-bosqich: Tabulyatsiya (rekursiyasiz, tezroq va xavfsizroq)

Rekursiya chuqur bo'lsa (n, m ~ 1000+) Python "recursion error" beradi. Shuning uchun jadvalni sikl bilan to'ldiramiz. Buning uchun 4 qadam:

Holat: dp[i][j] = (0,0) dan (i,j) ga nechta yo'l.
Boshlang'ich: dp[0][0] = 1.
O'tish: (i,j) ga faqat tepadan yoki chapdan kelinadi, demak dp[i][j] = dp[i-1][j] + dp[i][j-1]. To'siq bo'lsa 0.
Javob: dp[n-1][m-1].
python
n, m = 3, 3
g = ["...",
     ".#.",
     "..."]

dp = [[0] * m for _ in range(n)]
dp[0][0] = 1 if g[0][0] == '.' else 0

for i in range(n):
    for j in range(m):
        if g[i][j] == '#':
            dp[i][j] = 0
            continue
        if i == 0 and j == 0:
            continue
        yuqori = dp[i-1][j] if i > 0 else 0
        chap   = dp[i][j-1] if j > 0 else 0
        dp[i][j] = yuqori + chap

print(dp[n-1][m-1])    # 2

Jadval to'lib borishi:

1 1 1
1 0 1
1 2 3?  -> aslida: dp[2][1]=dp[1][1]+dp[2][0]=0+1=1, dp[2][2]=dp[1][2]+dp[2][1]=1+1=2

To'g'ri jadval:

1 1 1
1 0 1
1 1 2      javob = 2
4-bosqich: Xotirani tejash (ixtiyoriy)

dp[i] qatori faqat dp[i-1] qatoriga bog'liq, shuning uchun bitta qator yetadi:

python
dp = [0] * m
dp[0] = 1
for i in range(n):
    for j in range(m):
        if g[i][j] == '#':
            dp[j] = 0
        elif j > 0:
            dp[j] += dp[j - 1]      # dp[j] = tepadan (eski), dp[j-1] = chapdan (yangi)
print(dp[m - 1])

Xotira O(n·m) dan O(m) ga tushdi.

DP ni topish uchun "belgilar"

Masalada quyidagilar bo'lsa, DP ni o'ylang:

"Eng kam / eng ko'p / nechta usul bilan" so'ralsa
Har qadamda tanlov bor (olaman / olmayman, o'ngga / pastga)
Oddiy rekursiya bir xil holatni takrorlasa
Greedy (ochko'zlik) ba'zi misolda xato bersa

Tez yo'l: avval brute force rekursiya yozing. Keyin "funksiya parametrlari nechta xil qiymat oladi?" deb sanang. Shu son yetarlicha kichik bo'lsa, @lru_cache qo'shing. Kerak bo'lsa tabulyatsiyaga o'tkazing.

4. Bir nechta usulni birlashtirish: to'liq misol

Masala: n ta musbat son va q ta so'rov berilgan. Har so'rovda (l, S): l pozitsiyadan boshlab yig'indisi kamida S bo'ladigan eng qisqa qism massiv qayerda tugaydi (r ni toping)?

Sekin yechim: har so'rovda l dan boshlab sonlarni qo'shib borish, O(n·q).

Tez yechim: Prefix sum + Binary search. Sonlar musbat, demak pref o'sib boradi (saralangan), shuning uchun binary search qo'llash mumkin.

python
import sys
from bisect import bisect_left
input = sys.stdin.readline

def main():
    n = int(input())
    a = list(map(int, input().split()))
    q = int(input())

    # 1) Prefix sum
    pref = [0] * (n + 1)
    for i in range(n):
        pref[i + 1] = pref[i] + a[i]

    natija = []
    for _ in range(q):
        l, S = map(int, input().split())      # l: 0-indeks
        kerak = pref[l] + S                   # pref[r+1] >= kerak bo'lishi kerak

        # 2) Binary search: kerak dan kichik bo'lmagan birinchi o'rin
        k = bisect_left(pref, kerak)
        if k > n:
            natija.append(-1)                 # yetarli yig'indi yo'q
        else:
            natija.append(k - 1)              # r = k - 1

    print("\n".join(map(str, natija)))          # 3) Tez chiqarish

main()

Misol:

Kirish:          Chiqish:
5                2
1 2 3 4 5        3
3                -1
0 6
1 7
3 20

Tekshiramiz, birinchi so'rov l=0, S=6: 1+2+3 = 6, r = 2. ✓

Bu dasturda ishlatilgan texnikalar:

Prefix sum: yig'indini O(1) da olish
Binary search (bisect): r ni O(log n) da topish
Tez I/O: sys.stdin.readline va join
main() funksiya ichida yozish: global o'zgaruvchilarga qaraganda lokal o'zgaruvchilar Pythonda tezroq

Jami murakkablik: O(n + q log n).

5. Natijani tekshirish usuli (stress test)

Tez kod ba'zan xato ishlaydi. Shuning uchun sekin lekin to'g'ri brute force yozib, tasodifiy testlarda solishtiring:

python
import random

def sekin(a, l, S):                    # oddiy, ishonchli
    yig = 0
    for r in range(l, len(a)):
        yig += a[r]
        if yig >= S:
            return r
    return -1

def tez(a, l, S):                      # tezlashtirilgan
    pref = [0]
    for v in a: pref.append(pref[-1] + v)
    k = bisect_left(pref, pref[l] + S)
    return -1 if k > len(a) else k - 1

from bisect import bisect_left
for _ in range(1000):
    a = [random.randint(1, 10) for _ in range(random.randint(1, 10))]
    l = random.randint(0, len(a) - 1)
    S = random.randint(1, 50)
    assert sekin(a, l, S) == tez(a, l, S), (a, l, S)
print("Hammasi to'g'ri")

Xato topilsa, assert aynan qaysi test xato ekanini ko'rsatadi.
