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
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:200 center](img/encoded_names1.png?raw=true "Encoded Names")

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:400 center](img/attributed_names.png?raw=true "Attributed Names")

---
Length of Names

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/long_names.png?raw=true "Long Names")

---
:x: DoServerLoop(), ConvertToString()
:heavy_check_mark: ServerLoop(), ToString()

Use Acronyms and declare them in your Coding Standard/README etc


---
# Names That Can’t Be Misconstrued

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:400 center](img/left_wire.png?raw=true "Cut the left wire")

---
**KEY IDEA**
Actively scrutinize your names by asking yourself, “What other meanings could someone interpret from this name?”

e.g 
```C++
# Cuts off the end of the text, and appends "..."
def Clip(text, length):
...
```
Behavior?
• It removes length from the end
• It truncates to a maximum length

---
```C++
# Cuts off the end of the text, and appends "..."
def Truncate(text, length):
...
```
Rename length to max_length or better yet, max_chars.

---
:x:
```C++
print integer_range(start=2, stop=4)
# Does this print [2,3] or [2,3,4] (or something else)?
```
:heavy_check_mark:
```C++
print integer_range(first=2, last=4)
# Does this print [2,3] or [2,3,4] (or something else)?
```

---
```PrintEventsInRange("OCT 16 12:00am", "OCT 17 12:00am")```
```PrintEventsInRange("OCT 16 12:00am", "OCT 16 11:59:59.9999pm")```

Unfortunately, English doesn’t have a succinct word for “just past the last value.” Your best bet here is **begin**, **end**

---
Booleans
:x: ```read_password```
:heavy_check_mark: ```user_is_authenticated```


:x: ```disable_ssl = false```
:heavy_check_mark: ```use_ssl = true```

---
**WHO’S THE WIZARD?**

A while ago, one of the authors was installing the OpenBSD operating system. During the disk formatting step, a complicated menu appeared, asking for disk parameters.  One of the options was to go to “Wizard mode.” He was relieved to find this user-friendly option and selected it. To his dismay, it dropped the installer into a low-level prompt waiting for manual disk formatting commands, with no clear way to get out of it. Evidently “wizard” meant you were the wizard!

---
# Aesthetics

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/records.png?raw=true "Piles :(")

---
**Simple Principles**
• Use consistent layout, with patterns the reader can get used to.
• Make similar code look similar.
• Group related lines of code into blocks.

---
# Why Do Aesthetics Matter?
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/interview_candidate.png?raw=true "Candidates :(")

---
:x:
```C++
class StatsKeeper {
public:
// A class for keeping track of a series of doubles
void Add(double d); // and methods for quick statistics about them
private: int count; /* how many so far
*/ public:
double Average();
private: double minimum;
list<double>
past_items
;double maximum;
};
```


---
:heavy_check_mark:
```C++
// A class for keeping track of a series of doubles
// and methods for quick statistics about them.
class StatsKeeper {
    public:
        void Add(double d);
        double Average();

    private:
        list<double> past_items;
        int count; // how many so far

        double minimum;
        double maximum;
};
```

---
:x:
```C++
public class PerformanceTester {
public static final TcpConnectionSimulator wifi = new TcpConnectionSimulator(
    500, /* Kbps */
    80, /* millisecs latency */
    200, /* jitter */
    1 /* packet loss % */);
public static final TcpConnectionSimulator t3_fiber =
new TcpConnectionSimulator(
    45000, /* Kbps */
    10, /* millisecs latency */
    0, /* jitter */
    0 /* packet loss % */);
public static final TcpConnectionSimulator cell = new TcpConnectionSimulator(
    100, /* Kbps */
    400, /* millisecs latency */
    250, /* jitter */
    5 /* packet loss % */);
}
```

---
:heavy_check_mark:
```C++
public class PerformanceTester {
    public static final TcpConnectionSimulator wifi =
        new TcpConnectionSimulator(
            500,    /* Kbps */
            80,     /* millisecs latency */
            200,    /* jitter */
            1       /* packet loss % */);
    public static final TcpConnectionSimulator t3_fiber =
        new TcpConnectionSimulator(
            45000,  /* Kbps */
            10,     /* millisecs latency */
            0,      /* jitter */
            0       /* packet loss % */);
    public static final TcpConnectionSimulator cell =
        new TcpConnectionSimulator(
            100,    /* Kbps */
            400,    /* millisecs latency */
            250,    /* jitter */
            5       /* packet loss % */);
}
```

---
:heavy_check_mark:
```C++
public class PerformanceTester {
// TcpConnectionSimulator(throughput, latency, jitter, packet_loss)
//                             [Kbps]   [ms]    [ms]    [percent]
public static final TcpConnectionSimulator wifi =
    new TcpConnectionSimulator(500,      80,    200,       1);
public static final TcpConnectionSimulator t3_fiber =
    new TcpConnectionSimulator(45000,    10,    0,         0);
public static final TcpConnectionSimulator cell =
    new TcpConnectionSimulator(100,      400,   250,       5);
}
```
---
* Use Column Alignment When Helpful
* Pick a Meaningful Order, and Use It Consistently
* Organize Declarations into Blocks
* Break Code into **Paragraphs**

**KEY IDEA**
Consistent style is more important than the “right” style.

---
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:600 center](img/pig-sty.png?raw=true "Pig Sty :(")

---

# Commenting

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
