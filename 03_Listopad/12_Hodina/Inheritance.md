# Dědičnost

![](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fbe780pnhc1i6ybjluhfh.png)

- Jaké společné vlastnosti mají pes a kočka?

---

### Definice

Dědičnost je vlastnost OOP (objektově orientovaného programování), která umožňuje vytvořit **novou třídu** (tzv. *potomka*) na základě existující třídy (*rodiče*).  
Nová třída tak **přebírá vlastnosti a chování** rodičovské třídy a může je dále rozšiřovat nebo upravovat.

> Rodič v angličtině = Parent/Superclass  
> Potomek v angličtině = Child/Subclass

![Obrázek dědičnosti](https://cdn-images-1.medium.com/max/1080/1*gRily1Y6mlrOETJeKRgvgw.png)

---

### Jak napsat v kódu?

- Třída může dědit od jiné třídy pomocí znaku **`:`**.

```csharp
class Rodic
{
    // metody a atributy
}

class Potomek : Rodic
{
    // další metody a atributy
}
```

- Ve třídě `Potomek` můžeme použít přístupné atributy a metody třídy `Rodic`.
- Třída `Potomek` může mít své atributy a metody, které nebudou ve třídě `Rodic`.
- Třída `Potomek` může přepsat metodu rodiče, pokud je v rodiči označena jako `virtual` nebo `abstract`.
    - Jedná se o `Method Overriding` a používá se klíčové slovo `override`.
- Nedoporučuje se, ale lze vytvořit i atributy ve třídě `Potomek` se stejným názvem jako má třída `Rodic`.
    - Atribut v rodiči se tímto způsobem „schová“ (nedělejte to).

> Třída může mít maximálně jednoho přímého rodiče (můžeme dědit jen od jedné třídy).

### Příklady

Reprezentace kočky a psa v kódu bez použití dědičnosti:

#### Bez dědičnosti

```csharp
using System;

class Dog
{
    public string name = "";
    public int energy;

    public void Eat()
    {
        energy++;
    }

    public void Bark()
    {
        Console.WriteLine("Haf haf");
    }
}

class Cat
{
    public string name = "";
    public int energy;

    public void Eat()
    {
        energy++;
    }

    public void Meow()
    {
        Console.WriteLine("Mňau");
    }
}

class Program
{
    public static void Main(string[] args)
    {
        Dog d = new Dog();
        d.Eat();
        d.Bark();

        Cat c = new Cat();
        c.Eat();
        c.Meow();
    }
}
```

#### S dědičností

```csharp
using System;

class Animal
{
    public string name = "";
    public int energy;

    public void Eat()
    {
        energy++;
    }

    public virtual void MakeNoise()
    {
        Console.WriteLine("Make some noise");
    }
}

class Dog : Animal
{
    public string breed = "";
}

class Cat : Animal
{
}

class Program
{
    public static void Main(string[] args)
    {
        Cat c = new Cat();
        c.Eat();
        c.name = "Betsy";

        Dog d = new Dog();
        d.name = "Arnold";
        d.breed = "Zlatý retriever";
        d.Eat();
    }
}
```

---

### Přepisování metod

- V dědičnosti máme možnost přepsat metodu rodiče.
- Metoda v rodiči musí být označena jako `virtual` nebo `abstract` (případně už sama přepisovat jinou metodu).
- V potomkovi vytvoříme metodu se stejnou hlavičkou jako má rodič a použijeme klíčové slovo **`override`**.
    - Klíčové slovo `override` se píše přímo do hlavičky metody.
    - Pokud bychom napsali `override` u metody, kterou nelze přepsat, program by vyhodil chybu.
    - To nám může pomoct odhalit překlepy při přepisování metod či jiné chyby.

#### Příklad

```csharp
using System;

class Animal
{
    public virtual void MakeNoise()
    {
        Console.WriteLine("Make some noise");
    }
}

class Dog : Animal
{
    public override void MakeNoise()
    {
        Console.WriteLine("Haf haf");
    }
}

class Cat : Animal
{
    public override void MakeNoise()
    {
        Console.WriteLine("Mňau");
    }
}
```

> V C# každá třída automaticky dědí od třídy `object` (tedy `System.Object`), pokud neurčí jiného rodiče.  
> Všechny třídy mají několik metod již vytvořených a některé lze pomocí `override` přepsat.  
> Můžeme přepsat metodu `ToString()` a jednoduše tisknout vlastní objekty na konzoli.  
> Metoda `ToString()` vrátí řetězcovou reprezentaci objektu (ve výchozím nastavení obvykle vrací název jeho typu).

```csharp
class Dog
{
    public string name = "";
    public string breed = "";
    public int age;

    public override string ToString()
    {
        return name + ", plemeno: " + breed + ", věk: " + age;
    }
}
```

---

### Volání metod rodiče

- Pokud potomek přepíše metodu z rodiče, může se přesto rozhodnout zavolat i původní rodičovskou verzi.
- K tomu slouží klíčové slovo **`base`**.
- `base.NazevMetody()` zavolá metodu z rodiče, i když ji potomek přepsal.

#### Příklad:

```csharp
using System;

class Animal
{
    public virtual void MakeNoise()
    {
        Console.WriteLine("Dělá nějaký zvuk");
    }
}

class Dog : Animal
{
    public override void MakeNoise()
    {
        base.MakeNoise(); // Zavolá metodu z třídy Animal
        Console.WriteLine("Haf haf");
    }
}
```

**Výstup:**

```text
Dělá nějaký zvuk
Haf haf
```

---

### Modifikátor `protected`

- Modifikátor **`protected`** znamená, že:
- Atribut/metoda je **přístupná**:
    - ve **své vlastní třídě**,
    - a také ve **všech potomcích**, i když jsou v jiném jmenném prostoru (`namespace`).
- Používá se často při dědičnosti, když chceme, aby potomek měl přístup k proměnným nebo metodám rodiče,  
  ale zároveň je nechceme úplně „odhalit“ jako `public`.

> Na rozdíl od Javy samotné `protected` v C# **nezpřístupňuje** členy ostatním třídám ve stejném jmenném prostoru.  
> Kdybychom měli modifikátor `private` u atributů/metod rodiče, tak bychom je nemohli v potomkovi použít přímo.

#### Příklad:

```csharp
class Animal
{
    protected int energy;

    protected void Sleep()
    {
        energy += 10;
    }
}

class Cat : Animal
{
    public void Relax()
    {
        Sleep(); // metoda Sleep je přístupná díky protected, ale nelze ji zavolat z nesouvisející třídy
    }
}
```

---

### Otázky

1. **Jaký znak použiješ v C#, aby třída dědila z jiné třídy?**

2. **Jaký je rozdíl mezi atributem `public` a `protected` v kontextu dědičnosti?**

3. **Co znamená přepsání metody (method overriding) a k čemu slouží klíčová slova `virtual` a `override`?**

4. **Jaké jsou výhody použití dědičnosti oproti opakovanému kopírování kódu?**

5. **Co se stane, pokud vytvoříš v potomkovi atribut se stejným názvem jako má rodič?**

6. **Jak pomocí klíčového slova `base` zavoláš metodu z rodičovské třídy, která byla přepsána?**

7. **Jaká třída je implicitním (skrytým) rodičem všech tříd v C#? Jaké metody dědíme automaticky?**

8. **Jak můžeš pomocí metody `ToString()` upravit výpis objektu, aby dával smysl?**

9. **Může jedna třída v C# dědit od více tříd? Vysvětli proč.**

10. **Proč není vhodné označit atributy v rodiči jako `private`, pokud je chceme používat přímo i v potomkovi?**
