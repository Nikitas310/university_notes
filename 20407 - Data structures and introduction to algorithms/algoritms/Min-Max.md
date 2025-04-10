# מציאת ערך מינימום במערך

**קלט** - מערך לא ממוין $A$ בן $n$ איברים.
**פלט** - ערך האיבר המינימלי של $A$.

**סיבוכיות** - $O(n)$. בפועל נדרשות $n-1$ השוואות.

**אופן עבודה** - אלגוריתם מגדיר משתנה `min` להיות המינימום הנוכחי, ושומר בפנים את האיבר הראשון במערך. לאחר מכן בעזרת לולאה משוואה כל שאר איברי המערך עם ערך המינימום הנוכחי ושומר מתוכו את הקטן מבינהם. 

**שמורת לולאה** - לפני כל איטרציה ה-$i$ ($1 \le i \lt n$) , משתנה $min$ מכיל את הערך הקטן בתת-מערך $A[1, i]$.
- לפני האיטרציה הראשונה תת-צערך $A[1,1]$ מכיל רק איבר אחד והוא שמור במשתנה $min$.
- בכל צעד גוף הלולאה $for$ משוואה את איבר המינימלי הנוכחי עם איבר ה-$i+1$ במערך. אם הוא קטן מהמינימום הנוכחי, אזי הוא קטן מכל האיברים שקדמו לו במערך.
- כאשר $i == n$ משתנה $min$ מכיל את האיבר המינימלי בתת-מערך $A[1,n]$ שזה מערך כולו. 

```pseudocode
Minimun(A)
min <- A[1]
for i <- 2 to length[A]
	do if min > A[i]
		then min <- A[i]
return min
```

```python
def minimum(a):
	min_num = a[0]
	for el in a[1:]:
		min_num = el if (el < min_num) else min_num
return min_num
```


# מציאת ערך מקסימום במערך

אלגוריתם זהה למציאת ערך מינימום במערך, רק שבודקים אם הערך החדש גדול מערך המקסימום הנוכחי.



# מציאת ערך מינימום ומקסימום בו זמנית

**קלט** - מערך לא ממוין $A$ בן $n$ איברים.
**פלט** - ערך האיבר המינימלי וערך האיבר המקסימלי של $A$.

**סיבוכיות** - $\Theta(n)$. בפועל עבור $n$ זוגי נדרשות $3n /2 - 2$ השוואות, עבור $n$ אי-זוגי נדרשות $3\lfloor n/2 \rfloor$ השוואות.

**אופן עבודה** - בשלב הראשון האלגוריתם בוחר ערכים ל-$min$ ו-$max$ נוכחים. אם $n$ אי-זיגי אזי האיבר הראשון יהיה גם המינימום וגם המקסימום. אחרת נעשה השוואה בין שני האיברים הראשונים במערך, ושומר אותם במשתנה המתאים. בשבל בשני נעשה השוואה בין גל זוג עוקב של איברים ולאחר מכן נשוואה את הגדול מבינהם למקסימום הנוכחי ואת הקטן למינימום.

```pseudocode
Min-Max(A)
if length[A] % 2 = 0
	minimum, maximum <- Min-Max-Even(A)
else
	minimum, maximum <- Min-Max-Odd(A)

return minimum, maximum
	 


Min-Max-Odd(A)
minimum <- A[1]
maximum <- A[1]

i <- 2
while i < length[A]
	do if A[i] < A[i+1]
		if A[i] < minimum
			then minimum <- A[i]
		if A[i+1] > maximum
			then maximum <- A[i+1]
	else
		if A[i+1] < minimum
			then minimum <- A[i+1]
		if A[i] > maximum
			then maximum <- A[i]
	i <- i + 2
return minimum, maximum


Min-Max-Even(A)
if A[1] < A[2]
	minimum <- A[1]
	maximum <- A[2]
else
	minimum <- A[2]
	maximum <- A[1]

i <- 3
while i < length[A]
	do if A[i] < A[i+1]
		if A[i] < minimum
			then minimum <- A[i]
		if A[i+1] > maximum
			then maximum <- A[i+1]
	else
		if A[i+1] < minimum
			then minimum <- A[i+1]
		if A[i] > maximum
			then maximum <- A[i]
	i <- i + 2
return minimum, maximum
```

```python
def min_max(a):
minimum, maximum = None, None
	if len(a) % 2:
		if a[0] < a[1]:
			minimum, maximum = a[0], a[1]
		else:
			minimum, maximum = a[1], a[0]
		i = 2
	else:
		minimum, maximum = a[0], a[0]
		i = 1

	while i < len(a) - 1:
		if a[i] < a[i+1]:
			minimum = a[i] if a[i] < minimum else minimum
			maximum = a[i+1] if a[i+1] < maximum else maximum
		else
			minimum = a[i+1] if a[i+1] < minimum else minimum
			maximum = a[i] if a[i] < maximum else maximum

		i += 2
	return minimum, maximum
```
