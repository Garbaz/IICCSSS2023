---
marp: true
theme: dracula

math: mathjax

headingDivider: 2

paginate: true
header: Human Reading Time ~ LLM Surprisal
footer: Tobias Hoffmann, et al.

title: Human Reading Time ~ LLM Surprisal
author: Tobias Hoffmann
---

<style>
.outer {
    /* background:blue; */
    display:flex;
    flex-flow: row wrap;
    width:100%;
    height:90%;
}

.inner {
    /* background:green; */
    width:50%;
    display:flex;
    justify-content: center;
    align-items: center;  
}

.inner2 {
    /* background:red; */
    width: 70%;
}
</style>

<style>
.row {
  display: flex;
}

.column {
  flex: 50%;
}
</style>

<style>
.ref {
  font-size: 60%;
}
</style>


<style>
section {
    font-size: 30px;
}
</style>

# Human Reading Time ~ LLM Surprisal

<!-- _footer: Tobias Hoffmann, Lars Konieczny, Henrik Lorenzen, Mateo Cortés Lafourcade -->

<style scoped>
  section {
    /* align-items: stretch; */
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
  }
</style>


# Large Language Models

- Task: Given words so far, predict next word
  - e.g. prompt: *"The cat eats the* *"*, prediction: *"mouse"*
- State of the art: Attention mechanism<sup class="ref">*Vaswani et al. 2017*</sup>
  - Idea: Mix in *relevant* context tokens
  - Include large context without forgetfulness 

<div style="margin-left: 50px">
  <img src="gpt2-self-attention-example-2.png" height="200"></img>
</div>


# LLM Surprisal

- Normally: Most likely next word?
- Instead: How likely is *this* next word?
  - I.e. $P(t_n | t_{n-1}, ..., {t_0})$
- *Surprisal* $:=$ $-log_2P(t_n | t_{n-1}, ..., {t_0})$
  - High surprisal $\Leftrightarrow$ Low probability
  - Between $0$ and $\infty$

<div style="font-family: monospace; float:right; margin-top:-90px">
<pre>
The cat eats the  <b>mouse.</b>
-   8.8 7.2  1.7  <b>4.1</b>
<br>The cat eats the  <b>car.</b>
-   8.8 7.2  1.7  <b>15.1</b>

</pre>
</div>


# Human Reading Time

- How much time is spent per word while reading?
- Different metrics: *First Pass*, *Go Past*, etc.
- Generally: Predictable word ~ short reading time
  - We read over words that are predictable
  - We get stuck at words that are unexpected
- Measured in different ways, e.g. eye tracking

<img src="readingtime.png" width=99%>


# Local Syntactic Coherences

<div style="font-size:110%">

The coach chided the player tossed the frisbee by the opposing team.
The coach chided <u>the player tossed the frisbee</u> ***by*** the opposing team.

</div>

- Conflict between local and global parsing<sup class="ref">*Tabor et al. 2004*</sup>
- Increased reading time at subsequent word
- Not just syntactical, influenced by context
  - Including visual & textual<sup class="ref">*Konieczny et al. 2009, Müller et al. 2019*</sup>


# Context influences LSC-Effect

<div class="row" style="font-size:75%">
<div class="column">

Mit **(langweiligen Anekdoten | spannenden Geschichten)** überzieht der erste Redner sein Zeitlimit. Das Publikum hört ihm dabei **(gähnend | gespannt)** zu. Nach dem dreistündigen Vortrag hat er keine Energie mehr und übergibt an den nächsten Redner.

<i></i>
</div>
<div class="column" style="margin-left:25px;color:#bbbbbb;">

The first speaker exceeds his time limit with **(boring anecdotes | exciting stories)**. The audience listens to him **(yawning | attentively)**. After the three-hour talk, he has no more energy, and hands over to the next speaker.

</div>
</div>

<div class="row" style="font-size:75%">
<div class="column">

Der nächste Redner ärgert sich über alle Maßen,<br>als ihm der erste Redner **müde** das Publikum überlässt.

OR

Der nächste Redner ärgert sich über alle Maßen,<br>als ihm <u>der erste Redner **ermüdet** das Publikum</u> ***überlässt***.
</div>
<div class="column" style="margin-left:25px;color:#bbbbbb">

The next speaker is annoyed beyond measure, as the first speaker **(tiredly | tires)** leaves the audience to him.

</div>
</div>


# Reading Time ~ Surprisal ?

- Dataset: short German texts<sup class="ref">*from Müller et al. 2019 & Müller 2019*</sup>
- Reading times via eye tracking
- GPT-3.5 surprisals via OpenAI API
- Yes! ✨


# LSC-Effect in NNs?

<div class="row">
<div style="float:left;width:60%;">

- In RNNs: Yes<sup class="ref">*Konieczny 2005, Konieczny et al. 2009*</sup>
- In Transformers: No ✨
  - LSCs only mildly affect surprisal
  - No modulation due to context 
  - Explanation (?):
  Attention mechanism has no
  intrinisic local preference

</div>
<div style="float:left;width:40%;">

<img src="gpt_no_lsc.png" height=60%>

</div>
</div>

# Conclusion

- LLM Surprisals predict human reading times 
- But LLMs aren't fooled by local syntactic coherences
- 💡 LLM Surprisal as quantitative research tool
- ⚠️ Limits of LLMs as models of human language processing

<hr>

- **AMLAP Poster:** http://dx.doi.org/10.13140/RG.2.2.15402.39363/2
- **Slides at:** https://github.com/Garbaz/IICCSSS2023