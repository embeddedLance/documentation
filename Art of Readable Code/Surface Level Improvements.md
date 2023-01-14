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
✅

```C
for (Node* node = list->head; node != NULL; node = node->next)
    Print(node->data);
```

```C++
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

```C++
✅
if (exponent >= 0) {
    return mantissa * (1 << exponent);
} else {
    return mantissa / (1 << -exponent);
}
```
```C++
❌
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
```C++
❌
class BinaryTree {
    int Size();
    ...
};
```


```C++
✅
class BinaryTree {
    int Height();     // NumNodes or MemoryBytes 
...
};
```

---
Choose Specific Words

```C++
❌
class Thread {
    int Stop();
...
};
```

```C++
✅
class Thread {
    int Kill();     // Or Pause
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
❌
var euclidean_norm = function (v) {
    var retval = 0.0;
    for (var i = 0; i < v.length; i += 1)
        retval += v[i] * v[i];
    return Math.sqrt(retval);
};
```
For instance, imagine if the inside of the loop were accidentally:
```❌retval += v[i];```
This bug would be more obvious if the name were sum_squares:
```C++
sum_squares += v[i]; // Where's the "square" that we're summing? Bug!
```
---
Loop Iterators

```C++
❌
for (int i = 0; i < clubs.size(); i++)
    for (int j = 0; j < clubs[i].members.size(); j++)
        for (int k = 0; k < users.size(); k++)
            if (clubs[i].members[k] == users[j])
                cout << "user[" << j << "] is in club[" << i << "]" << endl;
```
In the if statement, members[] and users[] are using the wrong index

```C++
✅
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
❌ ServerCanStart()
✅ CanListenOnPort()

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

```C++ 
❌
string id; // Example: "af84ef845cd8"```
```
```C++
✅
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
❌ DoServerLoop(), ConvertToString()
✅ ServerLoop(), ToString()

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
❌
# Cuts off the end of the text, and appends "..."
def Clip(text, length):
...
```
Behavior?
• It removes length from the end
• It truncates to a maximum length

---
```C++
✅
# Cuts off the end of the text, and appends "..."
def Truncate(text, length):
...
```
Rename length to max_length or better yet, max_chars.

---
```C++
❌
print integer_range(start=2, stop=4)
# Does this print [2,3] or [2,3,4] (or something else)?
```
```C++
✅
print integer_range(first=2, last=4)
# Does this print [2,3] or [2,3,4] (or something else)?
```

---
```PrintEventsInRange("OCT 16 12:00am", "OCT 17 12:00am")```
```PrintEventsInRange("OCT 16 12:00am", "OCT 16 11:59:59.9999pm")```

Unfortunately, English doesn’t have a succinct word for “just past the last value.” Your best bet here is **begin**, **end**

---
Booleans
❌ ```read_password```
✅```user_is_authenticated```


❌ ```disable_ssl = false```
✅```use_ssl = true```

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
```C++
❌
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
```C++
✅
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
```C++
❌
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
```C++
✅
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
```C++
✅
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

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/manuals.png?raw=true "Manuals :(")

---
**KEY IDEA**
The purpose of commenting is to help the reader know as much as the writer did.

---
# What not to Comment

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/liberty.png?raw=true "What not to Comment :(")

---
```C++
❌
// The class definition for Account
class Account {
    public:
        // Constructor
        Account();
        // Set the profit member to a new value
        void SetProfit(double profit);
        // Return the profit from this Account
        double GetProfit();
};
```

---
Don't Comment for the sake of commenting
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/pelted.png?raw=true "What not to Comment :(")

---
```C++
❌
// Find the Node in the given subtree, with the given name, using the given depth.
Node* FindNodeInSubtree(Node* subtree, string name, int depth);
```
```C++
✅
// Find a Node with the given 'name' or return NULL.
// If depth <= 0, only 'subtree' is inspected.
// If depth == N, only 'subtree' and N levels below are inspected.
Node* FindNodeInSubtree(Node* subtree, string name, int depth);
```

---
Don’t Comment Bad Names—Fix the Names Instead
```C++
❌
// Enforce limits on the Reply as stated in the Request,
// such as the number of items returned, or total byte size, etc.
void CleanReply(Request request, Reply reply);
```
```C++
✅
// Make sure 'reply' meets the count/byte/etc. limits from the 'request'
void EnforceLimitsFromRequest(Request request, Reply reply);
```

---
Don’t Comment Bad Names—Fix the Names Instead
```C++
❌
// Releases the handle for this key. This doesn't modify the actual registry.
void DeleteRegistry(RegistryKey* key);
```
```C++
✅
void ReleaseRegistryHandle(RegistryKey* key);
```
---
# Include "Director Commentary"
```C++
// Surprisingly, a binary tree was 40% faster than a hash table for this data.
// The cost of computing a hash was more than the left/right comparisons.

....

// This heuristic might miss a few words. That's OK; solving this 100% is hard.

....

// This class is getting messy. Maybe we should create a 'ResourceNode' subclass to
// help organize things.
```
---
# Comment on Flaws in Your Code

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/flaws_in_code.png?raw=true "Comment on Flaws :)")

---
# Advertising Likely Pitfalls

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/pitfalls.png?raw=true "Advertising Likely Pitfalls")

---
```C++
❌ 
void SendEmail(string to, string subject, string body);
```
```C++
✅
// Calls an external service to deliver email. (Times out after 1 minute.)
void SendEmail(string to, string subject, string body);
```
```C++
❌ 
def FixBrokenHtml(html): ...
```

```C++
✅
// Runtime is O(number_tags * average_tag_depth), so watch out for badly nested inputs.
def FixBrokenHtml(html): ...
```
---
# "BIG PICTURE" Comments
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/big_picture.png?raw=true "Big Picture Comments")

---
# SHOULD YOU COMMENT THE WHAT, THE WHY, OR THE HOW?
You may have heard advice like, “Comment the why, not the what (or the how).” Although catchy, we feel these statements are too simplistic and mean different things to different people.

Do whatever helps the reader understand the code more easily. This may involve commenting the what, the how, or the why (or all three).

---
Getting over the Writer's Block

```C++
// Oh crap, this stuff will get tricky if there are ever duplicates in this list.
```
to 
```C++
// Careful: this code doesn't handle duplicates in the list (because that's hard to do)
```

---
# Precise & Compact Comments

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/concise_commenting.png?raw=true "Concise Comments")

---
**KEY IDEA**
Comments should have a high information-to-space ratio.

```C++
// Call connect with 10 as timeout and encryption set to false
Connect(10, false);

Connect(/* timeout_ms = */ 10, /* use_encryption = */ false);
```

```C++
// Iterate through the list in reverse order
for (list<Product>::reverse_iterator it = products.rbegin(); it != products.rend();++it)

// Display each price, from highest to lowest
for (list<Product>::reverse_iterator it = products.rbegin(); ... )
```

---
# Making Control Flow Easy to Read

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/control_flow.png?raw=true "Control Flow")

---
The order of arguments in conditionals

LHS: expression being interrogated, more in flux
RHS: expression being compared against, more constant
```C++
while (bytes_received < bytes_expected)
```
---
# Order of if/else 

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/gorilla.png?raw=true "Address the Gorilla in the room")

---
• Prefer dealing with the positive case first instead of the negative—e.g., if (debug) instead
of if (!debug).
• Prefer dealing with the simpler case first to get it out of the way. This approach might also
allow both the if and the else to be visible on the screen at the same time, which is nice.
• Prefer dealing with the more interesting or conspicuous case first.

---

“Don’t think of a pink elephant.” You can’t help but think about it—the “don’t” is drowned out by the more unusual “pink elephant.”

```C++
if (url.HasQueryParameter("expand_all")) {
    for (int i = 0; i < items.size(); i++) {
        items[i].Expand();
}
...
} else {
response.Render(items);
...
}
```
---
# Avoid do/while Loops

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/do_while.png?raw=true "Avoid Do While :(")

---
In my experience, the do-statement is a source of errors and confusion. … I prefer the condition “up front where I can see it.” Consequently, I tend to avoid do-statements.

Bjarne Stroustrup

---
Return Early from a function

```C++
public boolean Contains(String str, String substr) {
    if (str == null || substr == null) 
        return false;
    if (substr.equals("")) 
        return true;
}
```
---
# Can you follow the flow of Execution?
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/three_card.png?raw=true "Variable manipulated many times")

---
**KEY IDEA**
The more places a variable is manipulated, the harder it is to reason about its current value.

* Shrink the Scope of your variables
* Very hard to understand programs with many variables


---
Microsoft’s Eric Brechner has talked about how a great interview question should involve at least three variables.* It’s probably because dealing with three variables at the same time forces you to think hard! This makes sense for an interview, where you’re trying to push a candidate to the limit. But do you want your coworkers to feel like they’re in an interview while they’re reading your code?

---
# One Task at a Time

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/1task.png?raw=true "Multi-Tasking :(")

---
# Refactoring your code

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/tasking.png?raw=true "Refactoring your code")

---
# Turning thoughts into Code
You do not really understand something unless you can explain it to your grandmother.
    — **Albert Einstein**

1. Describe what code needs to do, in plain English, as you would to a colleague.
2. Pay attention to the key words and phrases used in this description.
3. Write your code to match this description.

---
# Write Less Code

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/less_code.png?raw=true "Write Less Code")

---
**KEY IDEA**
The most readable code is no code at all.

* Use libraries
* Unix/OS tools instead of coding
* Remove unused code

---
# Error Message Readability
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/readable_error.png?raw=true "Errors and Readability")

---
# Testing and Readability
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
![h:500 center](img/cat_temp.png?raw=true "Testing and Readability")

---
# Testing and Redability
* Prefer clean and simple test values that still get the job done.
* But the complete code should still be exercised.
* Name the test to clarify:
    • The class being tested (if any)
    • The function being tested
    • The situation or bug being tested
