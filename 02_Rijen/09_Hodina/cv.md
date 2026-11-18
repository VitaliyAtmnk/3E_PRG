# Práce s polem

## Úloha 1 – Duplicitní prvky v poli

Je dáno pole celých čísel `nums`. Vrať `true`, pokud se některá hodnota v poli vyskytuje **alespoň dvakrát**. Pokud jsou všechny prvky navzájem různé, vrať `false`.

### Příklad 1

**Vstup:** `nums = [1,2,3,1]`  
**Výstup:** `true`

**Vysvětlení:** Prvek `1` se nachází na indexech `0` a `3`.

### Příklad 2

**Vstup:** `nums = [1,2,3,4]`  
**Výstup:** `false`

**Vysvětlení:** Všechny prvky jsou navzájem různé.

### Příklad 3

**Vstup:** `nums = [1,1,1,3,3,4,3,2,4,2]`  
**Výstup:** `true`

```csharp
public bool ContainsDuplicate(int[] nums) {

}
```

---

## Úloha 2 – Maximální zisk z nákupu a prodeje akcie

Je dáno pole `prices`, kde `prices[i]` představuje cenu určité akcie v `i`-tý den.

Chceš maximalizovat svůj zisk tak, že si vybereš **jeden den**, kdy koupíš jednu akcii, a **jiný, pozdější den**, kdy tuto akcii prodáš.

Vrať **maximální zisk, kterého lze touto transakcí dosáhnout**. Pokud nelze dosáhnout žádného zisku, vrať `0`.

### Příklad 1

**Vstup:** `prices = [7,1,5,3,6,4]`  
**Výstup:** `5`

**Vysvětlení:** Akcii koupíš 2. den (cena = 1) a prodáš 5. den (cena = 6). Zisk je `6 - 1 = 5`. Upozornění: Není dovoleno koupit akcii 2. den a prodat ji 1. den, protože nákup musí proběhnout před prodejem.

### Příklad 2

**Vstup:** `prices = [7,6,4,3,1]`  
**Výstup:** `0`

**Vysvětlení:** V tomto případě se neuskuteční žádná transakce a maximální zisk je `0`.

### Hlavička metody
```csharp
public int MaxProfit(int[] prices) {
        
}
```

---

## Úloha 3 – Jed na královském dvoře

> *Poznámka: Následující příběh je smyšlený a slouží pouze jako kulisa programátorské úlohy. Historické podezření, že Jiří z Poděbrad otrávil Ladislava Pohrobka, nebylo prokázáno.*

Představ si alternativní historii, ve které Jiří z Poděbrad opakovaně podává králi Ladislavu Pohrobkovi jed! Po každém podání působí jed přesně `duration` sekund. Přesněji řečeno, pokud Jiří podá jed v sekundě `t`, je Ladislav pod jeho účinkem během **časového intervalu včetně obou krajních hodnot** `[t, t + duration - 1]`. Pokud Jiří podá další dávku **dříve, než účinek předchozí dávky skončí**, doba působení jedu se **začne počítat znovu**. Účinek pak skončí až `duration` sekund po posledním podání.

Je dáno **neklesající** pole celých čísel `timeSeries`, kde `timeSeries[i]` označuje sekundu, ve které Jiří podá Ladislavovi jed, a celé číslo `duration`.

Vrať **celkový počet sekund, po které je Ladislav pod účinkem jedu**.

### Příklad 1

**Vstup:** `timeSeries = [1,4]`, `duration = 2`  
**Výstup:** `4`

**Vysvětlení:**
- V sekundě 1 Jiří podá jed a Ladislav je pod jeho účinkem během sekund 1 a 2.
- V sekundě 4 Jiří podá další dávku a Ladislav je pod účinkem jedu během sekund 4 a 5.

Ladislav je tedy pod účinkem jedu v sekundách 1, 2, 4 a 5, celkem **4 sekundy**.

### Příklad 2

**Vstup:** `timeSeries = [1,2]`, `duration = 2`  
**Výstup:** `3`

**Vysvětlení:**
- V sekundě 1 Jiří podá jed a Ladislav je pod jeho účinkem během sekund 1 a 2.
- V sekundě 2 Jiří podá další dávku a doba působení jedu se začne počítat od začátku. Ladislav je tak pod jeho účinkem během sekund 2 a 3.

Ladislav je tedy pod účinkem jedu v sekundách 1, 2 a 3, celkem **3 sekundy**.


### Hlavička metody

```csharp
public int FindPoisonedDuration(int[] timeSeries, int duration) {
        
}
```

Pokud si chcete zkontrolovat správnost svého řešení

#### Příklad 1
- https://leetcode.com/problems/contains-duplicate/?envType=problem-list-v2&envId=array

#### Příklad 2
- https://leetcode.com/problems/best-time-to-buy-and-sell-stock/?envType=problem-list-v2&envId=array

#### Příklad 3
- https://leetcode.com/problems/teemo-attacking/description/?envType=problem-list-v2&envId=array