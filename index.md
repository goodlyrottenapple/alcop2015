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

*Samuel Balco, 8 May 2015, [ALCOP 2015](http://www.appliedlogictudelft.nl/alcop-2015/)*

<br>

<div class="logo"></div>


## What is the Calculus Toolbox?

+   ...A set of parametric scripts, Isabelle theory files and Scala code
+   ...A tool for semi-automatic code generation of Isabelle theories
+   ...Scala UI for easy manipulation of the structures defined within the calculus

## **Motivation for the toolbox**

## Minimal Calculus

+   ...Derived from a bigger D.EAK calculus, however
    +   ...contains fewer rules
    +   ...and Nullary/Unary/Binary connectives 
+   ...Initially used to test out the encoding of a display calculus in Isabelle, including
    +   ...a shallow and deep embedding
    +   ...proofs of equality between SE and DE

## Minimal Calculus Terms

Formulas  
$F:= ap \in \mathsf{AtProp} \mid F \land F \mid F \rightarrow F$  
Structures  
$S:= F \mid \mathsf{Id} \mid S \,; S \mid S > S$  
Sequents  
$S \vdash S$

## Minimal Calculus SE

~~~isabelle
type_synonym atProp = string

datatype formula = Atprop atProp
                 | And_F formula formula  (infix "∧F" 570)
                 | ImpR_F formula formula (infix "→F" 550)

datatype structures = Form formula
                    | Neutral ("I") 
                    | Comma structures structures (infix ";" 450)
                    | ImpR structures structures (infix ">>" 430)
~~~

## **Limitation of the SE...**

## **proof trees not first class citizens**

## Minimal Calculus DE

~~~isabelle
datatype Atprop = Atprop string | Atprop_Freevar string

datatype Formula_BinOp = Formula_And | Formula_ImpR
datatype Formula = Formula_Atprop Atprop
                 | Formula_Bin Formula Formula_BinOp Formula
                 | Formula_Freevar string
~~~

{: .note}
_Note that the sugar notation, similar to the one used in SE, has been omitted in this code snippet_

## Minimal Calculus DE 2

~~~isabelle
datatype Structure_ZerOp = Structure_Neutral
datatype Structure_BinOp = Structure_Comma | Structure_ImpR
datatype Structure = Structure_Formula Formula
                   | Structure_Zer Structure_ZerOp
                   | Structure_Bin Structure Structure_BinOp Structure
                   | Structure_Freevar string
 
datatype Sequent = Sequent_Structure Structure 
                 | Sequent Structure Structure
~~~

## **Limitation of DE...**

## **verbose encoding...**

## **$p \vdash p$**

## $p \vdash p$

Encoding                    |
:---------------------------|:---------------------------------------
LaTeX                       | `p \vdash p`
No sugar                    | `Sequent (Structure_Formula (Formula_Atprop (Atprop ''p''))) (Structure_Formula (Formula_Atprop (Atprop ''p'')))`
Isabelle&nbsp;DE&nbsp;&nbsp;| `((Atprop ''p'') \<^sub>F) \<^sub>S \<turnstile> ((Atprop ''p'') \<^sub>F) \<^sub>S`


## **Another problem...**

## A sample proof tree

~~~
((Atprop ''p'') \<^sub>F) \<^sub>S \<turnstile> B\<^sub>S ((Atprop ''p'') \<^sub>F) \<^sub>S ;\<^sub>S ((Atprop ''q'') \<^sub>F) \<^sub>S
\<Longleftarrow> PT (ImpR_comma_disp2) [
    B\<^sub>S ((Atprop ''p'') \<^sub>F) \<^sub>S \<rightarrow>\<^sub>S ((Atprop ''p'') \<^sub>F) \<^sub>S \<turnstile> ((Atprop ''q'') \<^sub>F) \<^sub>S 
\<Longleftarrow> PT (W_impR_L) [
    ((Atprop ''p'') \<^sub>F) \<^sub>S \<turnstile> ((Atprop ''p'') \<^sub>F) \<^sub>S \<Longleftarrow> PT (Id) []]]
~~~
{: .code}


## A sample proof tree

<div style="font-size:46px">
$$\frac{\displaystyle \frac
{p \vdash p}
{p > p \vdash q} }
{p \vdash p ; q}$$
</div>


## __[Demo]__
