---
title: 测试字体显示和语法高亮
weight: 18
pre: "<b>4. </b>"
chapter: true
mathjax: true
---

> To be, or not to be, Ay there's the point, To Die, to sleep, is that all? Aye all: No, to sleep, to dream, aye marry there it goes, For in that dream of death, when we awake, And borne before an everlasting Judge, From whence no passenger ever returned, The undiscovered country, at whose sight The happy smile, and the accursed damn'd.  But for this, the joyful hope of this, Who'd bear the scorns and flattery of the world, Scorned by the right rich, the rich cursed of the poor?  The widow being oppressed, the orphan wrong'd, The taste of hunger, or a tyrants reign, And thousand more calamities besides, To grunt and sweat under this weary life, When that he may his full Quietus make, With a bare bodkin, who would this endure, But for a hope of something after death?  Which puzzles the brain, and doth confound the sense, Which makes us rather bear those evils we have, Than fly to others that we know not of.  Aye that, O this conscience makes cowards of us all, Lady in thy orizons, be all my sins remembered.

**"To be, or not to be"** is one of the most widely known and quoted lines in modern English, and the soliloquy has been referenced in innumerable works of theatre, literature and music.

> 春眠不觉晓，处处闻啼鸟。
> 夜来风雨声，花落知多少。

春眠不觉晓，处处闻啼鸟。
夜来风雨声，花落知多少。

# 移舟泊烟渚#

## 日暮客愁新##

### 野旷天低树###

#### 江清月近人####

##### 江清月近人#####


1. 独上高楼望尽天涯路。
2. 衣带渐宽终不悔，为伊消得人憔悴。
3. 众里寻他千百度，暮然回首，那人正在灯火阑珊处。

* 昔我往矣，杨柳依依。今我来思，雨雪霏霏。 
* 蒹葭（jiān jiā）苍苍，白露为霜。 所谓伊人，在水一方。
* 彼采葛兮，一日不见，如三月兮。彼采萧兮，一日不见，如三秋兮。彼采艾兮，一日不见，如三岁兮。

# Test for headline h1 

The quick brown fox jumps over the lazy dog

## Test for headline h2

The quick brown fox jumps over the lazy dog

### Test for headline h3

The quick brown fox jumps over the lazy dog

#### Test for headline h4 

The quick brown fox jumps over the lazy dog

##### Test for headline h5 

The quick brown fox jumps over the lazy dog

## Test for Text highlight

Note: github don't support `==hightlight==` markdown. we need to use a html 5 `<mark>`

* 彼采葛兮，一日不见，如三月兮。
* <mark>彼采萧兮，一日不见，如三秋兮。</mark>
* 彼采艾兮，一日不见，如三岁兮。

## Test for picture

1. open `Keynote` or `Pages` (instructions same after this point)
2. Select a template. The background does not matter but white shows your work better
3. Drag or paste in your screenshot. Note: Using control+⌘+shift+4 you can send your screenshot directly to the clipboard.
4. Apply a drop shadow to your image
5. Select and copy just the image and paste it into your email or desired location.

![My helpful screenshot](/images/showcase/tat.png)

[ Stackexchange Question : Screenshot of selected area with shadow](http://apple.stackexchange.com/a/199248)

### Add Shadow by using script 

```bash
#!/bin/bash

convert "$1" -trim \( +clone -background grey25 -shadow 80x40+5+30 \) +swap -background transparent -layers merge +repage "$1-shadow.png"
```
The best thing is transparent drop shadow around the window without the white border.

The script from [here](https://github.com/StefanScherer/dotfiles/blob/master/bin/add-shadow)

You might need to `brew install imagemagick` before using it.

![Before add shadow](/images/showcase/tat.png)
*fig.1 - Before adding the shadow*


![After add shadow](/images/showcase/tat.png)
*fig.2 - 阴影效果添加之后*

### Create favicon.ico

```
convert favicon.png -define icon:auto-resize=64,48,32,16 favicon.ico

```

The code form [here](https://gist.github.com/pfig/1808188#gistcomment-1667360)

## Test syntax highlighting

### go

```go
pckage main

import (
    "fmt"
    "time"
)

func readword(ch chan string) {
    fmt.Println("Type a word, then hit Enter.")
    var word string
    fmt.Scanf("%s", &word)
    ch <- word
}

func timeout(t chan bool) {
    time.Sleep(5 * time.Second)
    t <- true
}

func main() {
    t := make(chan bool)
    go timeout(t)

    ch := make(chan string)
    go readword(ch)

    select {
    case word := <-ch:
        fmt.Println("Received", word)
    case <-t:
        fmt.Println("Timeout.")
    }
}
```
### Bash

```bash
[ -r ~/.profile ] && . ~/.profile             # set up environment, once, Bourne-sh syntax only
if [ -n "$PS1" ] ; then                       # are we interactive?
   [ -r ~/.bashrc     ] && . ~/.bashrc        # tty/prompt/function setup for interactive shells
   [ -r ~/.bash_login ] && . ~/.bash_login    # any at-login tasks for login shell only
fi                                            # End of "if" block
```

### JavaScript

```js
var counter = (function () {
    var i = 0; // private property

    return {   // public methods
        get: function () {
            alert(i);
        },
        set: function (value) {
            i = value;
        },
        increment: function () {
            alert(++i);
        }
    };
})(); // module

counter.get();       // shows 0
counter.set(6);
counter.increment(); // shows 7
counter.increment(); // shows 8
```

### HTML 

```html
<!DOCTYPE html>
<html>
<head>
<title>MathJax TeX Test Page</title>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
</script>
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_CHTML">
</script>
</head>
<body>
When $a \ne 0$, there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
</body>
</html>

```
### Scala

```scala
var correct = 0
var questions = 0
var heads = 0
var trials = 10000

// Let's run some trials
(1 to trials).foreach { trial =>
  // toss a fair coin
  scala.util.Random.nextBoolean() match {
    case true =>  // Heads was tossed. Wake on Monday.
      // Sleeping Beauty always bet Heads was tossed;
      // ... in this case, only once.
      questions += 1
      correct += 1
      heads += 1
    case _ =>     // Tails was tossed. Wake on Monday and Tuesday.
      // Sleeping Beauty always bet Heads was tossed;
      // ... in this case, it will bet both on Monday
      // and Tuesday. But it will fail!
      questions += 2
  }
}

println("Probability of SB being correct: " + correct.toDouble/questions)
println("Probability of Heads being tossed: " + heads.toDouble/trials)
```

Here's a sample run:

```
Probability of SB being correct: 0.33636242148870776
Probability of Heads being tossed: 0.5034
```

## Test for Tables

| Lex noation      | Set Theory Symbols    | 概念 |
| ---              | ---                   | ---                |
| `\mid`           | $$ \mid            $$ | |
| `\lbrace`        | $$ \lbrace \rbrace $$ | 也能用`\{\}` |
| `\in`            | $$ a \in A         $$ | a属于A element of|
| `\notin`         | $$ a \notin A      $$ | 不属于  |
| `\ni`            | $$ \ni             $$ | 也能用`\owns`|
| `\varnothing`    | $$ \varnothing     $$ | 空集 |
| `\subset`        | $$ A \subset B     $$ | A是B的子集        |
| `\subseteq`      | $$ A \subseteq B   $$ | A是B的子集（一般用这个）|
| `\subsetneq`     | $$ A \subsetneq B  $$ | A是B的真子集 proper subset |
| `\supset`        | $$ B \supset A     $$ | B包含A  | 
| `\supseteq`      | $$ B \supseteq A   $$ | B包含A（一般用这个）include|
| `\supsetneq`     | $$ B \supsetneq A  $$ | B真包含A |
| `\cap`           | $$ A \cap B        $$ | A与B的交集，A交B Intersection |
| `\cup`           | $$ A \cup B        $$ | A与B的并集，A并B Union|


## Test for MathJax (Tex/LaTeX) 

$$ \lbrace x \in X \mid x > \frac{1}{2} \rbrace $$ 

When $$a \ne 0$$ there are two solutions to $$ax^2 + bx + c = 0$$ and they are $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$


### A note for MathJax when using single $

When [using the single-dollar][1] delimiters, ”... the cost is $2.50 for the first one, and $2.00 for each additional one ...” would cause the phrase “2.50 for the first one, and” to be treated as mathematics since it falls between dollar signs. For this reason, if you want to use single-dollars for in-line math mode, you must enable that explicitly in your configuration:

```html
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
  });
</script>
<script type="text/javascript" async
  src="path-to-mathjax/MathJax.js?config=TeX-AMS_CHTML"></script>
```

[1]:http://docs.mathjax.org/en/latest/start.html#putting-mathematics-in-a-web-page

There has been an extensive discussion on this topic, see more details [in this page](http://docs.mathjax.org/en/latest/).



