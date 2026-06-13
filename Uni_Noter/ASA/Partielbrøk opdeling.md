
Når man arbejder med brøker i Laplace-domænet, kan det være svært at se, hvordan de direkte kan omskrives.  
Derfor opdeler man en stor brøk i flere mindre brøker dette kaldes **partielbrøkopdeling**.

Formålet er at gøre udtrykket nemmere at arbejde med, især når man skal tage inverse Laplace-transformationer.

---

## Eksempel

Vi starter med en brøk:

$$
\frac{5}{s^2+3s+2}
$$

---

## Trin 1: Find rødderne

Vi kan sætte nævneren lig 0 og finde røderne.

$$
{s^2+3s+2} = 0 = [-1,-2]
$$

---

## Trin 2: Gør fællesnævner

Vi kan nu opdele brøkken med vores rødder. her er det vigtigt at se røderne er konjugered.
$$
\frac{5}{(s+1)(s+2)} = \frac{A}{s+1} + \frac{B}{s+2}
$$

---

## Trin 3: Isoler A og B

Ved at gange $(s+1)(s+2)$ på alle brøkker i funktionen isolere du til en simpler version

$$
5 = A*(s+2)+B*(s+1)
$$

For at finde A og B kan vi definere S. vis vi definere S til at være lig rod 1 fjernes B side og vi kan finde A og definere vi S til at være lig rod 2 fjernes A side. 
$$
S = -1
$$
$$
5 = A*(s+2) \approx A=5
$$
$$
s=-2
$$
$$
5 = B*(s+1) \approx B=-5
$$


---
## Trin 4: Endelig formel

Vi have vores fundet funktion til at være
$$
\frac{5}{(s+1)(s+2)} = \frac{A}{s+1} + \frac{B}{s+2}
$$

Indsætter vi Nu A og B for vi en funktion der er simple and konvertere i laplace

$$
\frac{5}{s+1} + \frac{-5}{s+2}
$$