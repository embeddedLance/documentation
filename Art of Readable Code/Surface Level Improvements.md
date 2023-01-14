---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
marp: true
---

# The Art of Readable Code

---
# Necessity


![bg right](img/late_night.png?raw=true "Late Night adventures")

---

# Code should be easy to understand
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![w:700 center](img/alien_tot.png?raw=true "ToT to other species")

---

Minimize the time it would take for someone else to understand it 
<style scoped>
pre {
   font-size: 0.8rem;
}
</style>
:heavy_check_mark:

```C
for (Node* node = list->head; node != NULL; node = node->next)
    Print(node->data);
```
:x:

```C
Node* node = list->head;
if (node == NULL) return;
while (node->next != NULL) {
    Print(node->data);
    node = node->next;
}
if (node != NULL) Print(node->data);
```
---
Is Smaller always better

:heavy_check_mark:

```C
if (exponent >= 0) {
    return mantissa * (1 << exponent);
} else {
    return mantissa / (1 << -exponent);
}
```
:x:

```C
return exponent >= 0 ? mantissa * (1 << exponent) : mantissa / (1 << -exponent);
```
---

# Surface Level Improvements 

---
# Packing Info into Names
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/man-eater.png?raw=true "man-eater plant")

---

Choose Specific Words
:x:

```C++
class BinaryTree {
    int Size();
    ...
};
```

:heavy_check_mark:

```C++
class BinaryTree {
    int Height();     // NumNodes or MemoryBytes 
...
};
```

---
Choose Specific Words

:x:

```C++
class Thread {
    int Stop();
...
};
```

:heavy_check_mark:

```C
class Thread {
    int Kill();     // Pause
...
};
```
---
# Find Colourful Names

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/stegosaurus.png?raw=true "Use a Thesaurus")


---

**Word** **Alternatives**


**send** deliver, dispatch, announce, distribute, route
**find** search, extract, locate, recover
**start** launch, create, begin, open
**make** create, set up, build, generate, compose, add, new


**KEY  IDEA**
It’s better to be clear and precise than to be cute.

---
Avoid Generic Names Like tmp and retval
```C
var euclidean_norm = function (v) {
    var retval = 0.0;
    for (var i = 0; i < v.length; i += 1)
    retval += v[i] * v[i];
    return Math.sqrt(retval);
};
```
For instance, imagine if the inside of the loop were accidentally:
```retval += v[i];```
This bug would be more obvious if the name were sum_squares:
```C++
sum_squares += v[i]; // Where's the "square" that we're summing? Bug!
```
---
Loop Iterators

```C++
for (int i = 0; i < clubs.size(); i++)
    for (int j = 0; j < clubs[i].members.size(); j++)
        for (int k = 0; k < users.size(); k++)
            if (clubs[i].members[k] == users[j])
                cout << "user[" << j << "] is in club[" << i << "]" << endl;
```
In the if statement, members[] and users[] are using the wrong index

```C++
if (clubs[ci].members[ui] == users[mi]) # Bug! First letters don't match up.
```

---
Prefer Concrete Names over Abstract Names
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/hammer.png?raw=true "Concrete Names")

---
:x: ServerCanStart()
:heavy_check_mark: CanListenOnPort()

At Google, to avoid default Copy Constructors and  assignment operators, the following macro is defined

```C++
#define DISALLOW_EVIL_CONSTRUCTORS(ClassName) \
ClassName(const ClassName&); \
void operator=(const ClassName&);
```

---
Attaching Extra Information to a Name

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/dangerous_animal.png?raw=true "Dangerous Animal")

---
:x: 
```C++ 
string id; // Example: "af84ef845cd8"```
```
:heavy_check_mark:
```C++
string hex_id;
```

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:200 center](img/detailed_info_params.png?raw=true "Param Details")
---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---


---
