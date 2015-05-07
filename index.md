---

layout: bright

style: |

    #Cover h2 {
        margin:30px 0 0;
        color:#FFF;
        text-align:center;
        font-size:70px;
        }
    #Cover p {
        margin:10px 0 0;
        text-align:center;
        color:#FFF;
        font-style:italic;
        font-size:20px;
        }
        #Cover p a {
            color:#FFF;
            }
    #Picture h2 {
        color:#FFF;
        }
    .image {
        width:32em;
        }
    .note {
        font-size:16px
    }
    .logo {
        margin-left: auto;
        margin-right: auto;
        width: 180px;
        height: 44px;
        background: url("http://www.le.ac.uk/images/hp/logo-sprite.png") no-repeat scroll 0% 0% / 100% auto transparent;
    }
    .slide pre code {
        font-size:18px;
        white-space: pre-wrap;
    }
---

# Calculus Toolbox {#Cover}

*Samuel Balco, 8 May 2015, [ALCOP 2015](http://www.appliedlogictudelft.nl/alcop-2015/)  
joint work with Giuseppe Greco and Alexander Kurz*
<br>
<br>

<div class="logo"></div>


## What is the Calculus Toolbox?

+   ...A set of parametric scripts, Isabelle theory files and Scala code
+   ...A tool for semi-automatic code generation of Isabelle theories
+   ...Scala UI for easy manipulation of the structures defined within the calculus

## **Motivation for the toolbox**

## **Parametric encoding in Isabelle...**

## **Verbose encoding...**

## **$p \vdash p$**

## $p \vdash p$


:--------------------------------|:---------------------------------------
...LaTeX                         | ...`p \vdash p`
...No&nbsp;sugar                 | ...`Sequent (Structure_Formula (Formula_Atprop (Atprop ''p''))) (Structure_Formula (Formula_Atprop (Atprop ''p'')))`
...Isabelle&nbsp;IDE&nbsp;&nbsp; | ...<code>((Atprop ''p'') <sub>F</sub>) <sub>S</sub> ⊢ ((Atprop ''p'') <sub>F</sub>) <sub>S</sub></code>


## **Rule encoding**


## Structural Rules

<img class="image" src="https://rawgit.com/goodlyrottenapple/alcop2015/gh-pages/files/structural1.svg">

## Structural Rules

<img class="image" src="https://rawgit.com/goodlyrottenapple/alcop2015/gh-pages/files/structural2.svg">

## Display Postulates

<img class="image" src="https://rawgit.com/goodlyrottenapple/alcop2015/gh-pages/files/display.svg">

## Grishin Rules

<img class="image" src="https://rawgit.com/goodlyrottenapple/alcop2015/gh-pages/files/grishin.svg">

## Operational Rules

<img class="image" src="https://rawgit.com/goodlyrottenapple/alcop2015/gh-pages/files/op1.svg">

## Operational Rules

<img class="image" src="https://rawgit.com/goodlyrottenapple/alcop2015/gh-pages/files/op2.svg">


## **109 in total**

## Rule encoding

<table>
    <tr class="next">
        <td>Isabelle:&nbsp;&nbsp;</td>
        <td><pre><code>"ruleRuleStructAct x RuleStructAct.FS_A_L = ((ActS<sub>S</sub> (forwA<sub>S</sub>) (?<sub>Act</sub> ''a'') (B<sub>S</sub> (?<sub>S</sub> ''Y'') (→<sub>S</sub>) (?<sub>S</sub> ''Z''))) ⊢ (?<sub>S</sub> ''X'')) ⟹RD (λx. Some [((B<sub>S</sub> (ActS<sub>S</sub> (forwA<sub>S</sub>) (?<sub>Act</sub> ''a'') (?<sub>S</sub> ''Y'')) (→<sub>S</sub>) (ActS<sub>S</sub> (forwA<sub>S</sub>) (?<sub>Act</sub> ''a'') (?<sub>S</sub> ''Z''))) ⊢ (?<sub>S</sub> ''X''))])"</code></pre></td>
    </tr>
    <tr class="next">
        <td>JSON*: </td>
        <td><pre class="code"><code>"FS_A_L" : ["forwA Act?a (?Y >> ?Z) |- ?X", 
"(forwA Act?a ?Y) >> (forwA Act?a ?Z) |- ?X"]</code></pre></td>
    </tr>
</table>

 
## A sample proof tree

<pre markdown="1"><code>(((((Atprop ''p'') \&lt;^sub>F) \&lt;^sub>S) \&lt;turnstile>\&lt;^sub>S (B\&lt;^sub>S (((Atprop ''p'') \&lt;^sub>F) \&lt;^sub>S) (;\&lt;^sub>S) (((Atprop ''q'') \&lt;^sub>F) \&lt;^sub>S))) \&lt;Longleftarrow> PT (RuleDisp (ImpR_comma_disp2)) [(((B\&lt;^sub>S (((Atprop ''p'') \&lt;^sub>F) \&lt;^sub>S) (\&lt;rightarrow>\&lt;^sub>S) (((Atprop ''p'') \&lt;^sub>F) \&lt;^sub>S)) \&lt;turnstile>\&lt;^sub>S (((Atprop ''q'') \&lt;^sub>F) \&lt;^sub>S)) \&lt;Longleftarrow> PT (RuleStruct (W_impR_L)) [(((((Atprop ''p'') \&lt;^sub>F) \&lt;^sub>S) \&lt;turnstile>\&lt;^sub>S (((Atprop ''p'') \&lt;^sub>F) \&lt;^sub>S)) \&lt;Longleftarrow> PT (RuleZer (Id)) [])])])
</code></pre>
{: .code}


## A sample proof tree

<pre><code>(Atprop ''p'' <sub>F</sub> <sub>S</sub> ⊢<sub>S</sub> B<sub>S</sub> Atprop ''p'' <sub>F</sub> <sub>S</sub> ;<sub>S</sub> Atprop ''q'' <sub>F</sub> <sub>S</sub>) ⟸ PT  RuleDisp ImpR_comma_disp2  
[(B<sub>S</sub> Atprop ''p'' <sub>F</sub> <sub>S</sub> →<sub>S</sub> Atprop ''p'' <sub>F</sub> <sub>S</sub> ⊢<sub>S</sub> Atprop ''q'' <sub>F</sub> <sub>S</sub>) ⟸ PT  RuleStruct W_impR_L
[(Atprop ''p'' <sub>F</sub> <sub>S</sub> ⊢<sub>S</sub> Atprop ''p'' <sub>F</sub> <sub>S</sub>) ⟸ PT  RuleZer RuleZer.Id  []]]</code></pre>
{: .code}


## A sample proof tree

<div style="font-size:46px">
$$\frac{\displaystyle \frac
{p \vdash p}
{p > p \vdash q} }
{p \vdash p ; q}$$
</div>


## __Demo__

## Links

Code: [github.com/goodlyrottenapple/calculus-toolbox](https://github.com/goodlyrottenapple/calculus-toolbox/)

Docs: [goodlyrottenapple.github.io/calculus-toolbox](https://goodlyrottenapple.github.io/calculus-toolbox/)

## __Thank You.__
